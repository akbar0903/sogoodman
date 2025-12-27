---
title: 跨资源共享（CORS）
date: 2025-12-27 16:43:16
tags: [前端, HTTP]
categories: 前端
cover: https://www.bing.com/th?id=OHR.ReindeerFinland_ZH-CN6822163943_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

# 什么是跨资源共享（Cross-Origin Resource Sharing，CORS）

简单来说，CORS 是一种安全机制。它的存在是为了“打破”浏览器的同源策略（Same-Origin Policy）。

1. **核心概念：什么是“源（Origin）”？**

在深入 CORS 之前，必须明确什么是“同源”。如果两个 URL 的 协议（Protocol）、主机（Host） 和 端口（Port） 都相同，它们就是同源的。
- http://example.com/a.js 和 http://example.com/b.js → 同源
- http://example.com 和 https://example.com → 跨源（协议不同）
- http://example.com 和 http://api.example.com → 跨源（主机不同）

2. **为什么需要 CORS？**

默认情况下，浏览器为了安全，不允许 JavaScript 脚本读取跨源接口的响应。但在现代 Web 开发中，前端（如 localhost:3000）调用后端 API（如 api.myapp.com）是常态，CORS 就是那把“合法的钥匙”，让服务器告诉浏览器：“我允许这个源访问我的数据”。

3. **三种主要的请求场景：**

根据 MDN 的描述，浏览器会将跨源请求分为几类处理：

**①简单请求：** 
某些请求不会触发 CORS 预检请求。如果请求满足以下条件，浏览器会直接发出请求，并在响应头中检查权限：
**方法**：GET、HEAD 或 POST。
**Content-Type**：仅限于 text/plain、multipart/form-data 或 application/x-www-form-urlencoded。
**流程：**浏览器直接发请求 → 服务器返回结果（带上 Access-Control-Allow-Origin）→ 浏览器检查该头，匹配则通过，不匹配则报错。

② 预检请求（Preflight Requests）
对于可能对服务器数据产生副作用的请求（如 DELETE、PUT 或 Content-Type 为 application/json），浏览器会先发一个 OPTIONS 请求进行“探路”。

流程：
**浏览器发 OPTIONS：**询问“我可以发 POST 吗？可以带自定义 Header 吗？”
**服务器响应：**返回允许的方法、头信息和有效期（Access-Control-Max-Age）。
**浏览器发实际请求：**只有预检通过，才会发送真正的业务请求。

③ 附带身份凭证的请求（Credentialed Requests）
如果你需要跨域发送 Cookie 或 Authorization 标头：
前端必须设置 withCredentials: true (XHR) 或 credentials: 'include' (Fetch)。
关键限制：服务器的响应头 Access-Control-Allow-Origin 不能设为通配符 *，必须指明具体的域名。此外，还必须返回 Access-Control-Allow-Credentials: true。

4. **常见的关键 HTTP 响应头**

- Access-Control-Allow-Origin：指定允许访问资源的域名，或使用 * 允许所有域。
- Access-Control-Allow-Methods：指定允许的 HTTP 方法，如 GET、POST、PUT 等。
- Access-Control-Allow-Headers：指定允许的请求头。
- Access-Control-Allow-Credentials：是否允许发送 Cookie 和 HTTP 认证信息。
- Access-Control-Max-Age：预检请求的结果可以缓存多长时间。

5. **常见的坑点**

- **控制台报错：**即使服务器返回了 200 OK，如果没带正确的 CORS 头，浏览器依然会拦截数据，并在控制台报 CORS error。
- **通配符与凭证冲突：**使用通配符 * 时，不能携带凭证（Cookie）。必须指定具体域名。
- **预检请求失败：**如果服务器没有正确响应 OPTIONS 请求，实际请求将不会发送。

# 后端配置 CORS

因为 CORS 是服务器告诉浏览器“允许访问”的机制，所以需要在后端进行配置。以下是一些常见后端框架的 CORS 配置示例：

## Java (Spring Boot)

```java
package com.akbar.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class WebMVCConfiguration implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://127.0.0.1:5500") // 允许的域名，可以使用通配符 "*"
                .allowedMethods("*")
                .allowedHeaders("*");
    }
}
```

## Node.js (原生 HTTP 模块)

```javascript
const http = require('http')

const server = http.createServer(function (request, response) {
  // 设置CROS头
  response.setHeader('Access-Control-Allow-Origin', '*')
  response.setHeader(
    'Access-Control-Allow-Methods',
    'GET, POST, PUT, DELETE, OPTIONS',
  )
  response.setHeader(
    'Access-Control-Allow-Headers',
    'Content-Type, Authorization',
  )

  // 处理预检请求
  if (request.method === 'OPTIONS') {
    response.writeHead(204)
    response.end()
    return
  }

  // 处理实际请求
  if (request.url === '/hello' && request.method === 'GET') {
    response.writeHead(200, { 'Content-Type': 'text/plain' })
    response.end('Hello, World!\n')
  } else {
    response.writeHead(404, { 'Content-Type': 'text/plain' })
    response.end('Not Found\n')
  }
})

// 监听端口3000
server.listen(3000, function () {
  console.log('HTTP server running at http://localhost:3000/')
})
```

## Node.js (Express 框架)

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// 场景 A：全开放（类似你那段 Spring Boot 代码）
app.use(cors());

// 场景 B：精细化配置（生产环境推荐）
const corsOptions = {
    origin: 'http://localhost:3000', // 只允许你的前端项目访问
    methods: 'GET,POST',             // 只允许 GET 和 POST
    allowedHeaders: ['Content-Type', 'Authorization'],
    credentials: true,                // 允许跨域带 Cookie
    maxAge: 86400                     // 预检请求结果缓存 24 小时
};

app.use(cors(corsOptions));

app.get('/api/user', (req, res) => {
    res.json({ name: "Gemini" });
});
```

# 通过代理解决 CORS

在开发环境中，前端项目通常会通过代理服务器来绕过 CORS 限制。这样，浏览器认为请求是同源的，从而避免了跨域问题。
我们知道，现在的前端脚手架（如 Vite、Webpack）就是一个nodejs环境下的开发服务器，它有自己的端口（如 localhost:3000），而后端服务器通常也有自己的端口（如 localhost:8000）。这时，如果后端不配合开启 CORS，前端就会遇到跨域问题。

解决方案就是：让前端开发服务器做代理，转发请求到后端服务器。这样，浏览器只和前端开发服务器通信，避免了跨域问题。

例如，在 Vite 中，可以在 vite.config.js 中配置代理：

```javascript
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
  plugins: [vue()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8000', // 后端服务器地址
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    },
  },
});
```

**整个过程如下：**

- 前端发起请求：你的 Vue 代码请求 http://localhost:5173/api/users。注意，这个 URL 的协议、域名、端口和你的页面完全一致！所以浏览器认为这是同源请求，直接放行。
- Vite 服务器拦截：Vite 发现请求路径以 /api 开头，它并不会去自己的静态资源里找文件，而是根据你的配置，把请求“转发”给 http://localhost:9090。
- Vite 扮演客户端：Vite 的 Node.js 环境发起一个请求到 9090。对于后端（Spring Boot 或 Node.js）来说，它只看到一个普通的服务器请求，于是返回数据。
- Vite 返回数据：Vite 拿到数据后，再转手交给浏览器里的 Vue 代码。

**一个非常重要的“坑”**

生产环境怎么办？ 由于 Vite 的 server.proxy 只在开发阶段运行（它是 Vite 开发服务器的一部分）。当你执行 npm run build 将代码部署到 Nginx 或 Tomcat 时，这个代理就不存在了！

这时，如果后端没有正确配置 CORS，浏览器就会报跨域错误。解决方案有两个：
1. **后端配置 CORS**：这是最推荐的方式。让后端服务器支持 CORS，允许你的前端域名访问。
2. **生产环境也使用代理服务器**：在生产环境中，可以使用 Nginx 作为反向代理服务器，配置类似的代理规则，将请求转发到后端服务器。

nginx 配置示例：

```nginx
server {
    listen 80;
    server_name my-app.com;

    # 前端页面
    location / {
        root /var/www/html;
    }

    # 后端接口转发(代理)
    location /api/ {
        proxy_pass http://localhost:9090/; 
    }
}
```