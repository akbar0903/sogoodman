---
title: knife4j接口文档生成工具
date: 2025-06-22 19:46:11
tags: ['Java', '接口文档', 'Spring']
categories: 'Java'
cover: https://www4.bing.com//th?id=OHR.SeaTurtleBrazil_ZH-CN6907161064_1920x1080.jpg&rf=LaDigue_1920x1080.jpg&pid=hp
---

> knife4j的官方文档写了好多个版本的使用方法，感觉很混乱，尤其是像我没怎么使用过swagger的人来说，完全不知道使用哪个版本。下面是spring-boot2.7使用knife4j使用笔记，我是跟着黑马老师写的，一切功能都正常。

# 导入maven依赖

```xml
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>knife4j-spring-boot-starter</artifactId>
    <version>3.0.2</version>
</dependency>
```

# 配置

然后写一个配置文件，进行swagger（或者说knife4j）的配置:

```java
package com.akbar.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurationSupport;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;

@Configuration
public class WebMvcConfiguration extends WebMvcConfigurationSupport {

    /*
    * knife4j生成接口文档
    * */
    @Bean
    public Docket docket() {
        ApiInfo apiInfo = new ApiInfoBuilder()
                .title("苍穹外卖项目接口文档")
                .version("1.0")
                .description("苍穹外卖项目接口文档")
                .build();

        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo)
                .select()
                .apis(RequestHandlerSelectors.basePackage("com.akbar.controller"))
                .paths(PathSelectors.any())
                .build();
    }

    /*
    * 设置静态资源映射
    * */
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        // 访问doc.html就就可以看到api文档
        registry.addResourceHandler("/doc.html")
                .addResourceLocations("classpath:/META-INF/resources/");
        registry.addResourceHandler("/webjars/**")
                .addResourceLocations("classpath:/META-INF/resources/webjars/");
    }
}
```

配置信息解释（chatgpt回答）：

*   `Docket`：Knife4j/Swagger 的核心配置类，用来设置 API 文档的生成规则。
*   `apiInfo`：定义 API 文档的一些基本信息，例如标题、版本和描述。
*   `select()`：用于选择 API 的控制器类，这里使用 `RequestHandlerSelectors.basePackage("com.akbar.controller")` 来指定扫描 `com.akbar.controller` 包下的所有控制器类。
*   `paths(PathSelectors.any())`：表示扫描所有路径下的接口。
*   `DocumentationType.SWAGGER_2`：指定使用 Swagger 2 类型来生成文档。

# 常用注解

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250622195101329.webp)

# 在控制器中使用

```Java
package com.akbar.controller.admin;

import com.akbar.dto.EmployeeLoginDTO;
import com.akbar.entity.Employee;
import com.akbar.result.Result;
import com.akbar.service.EmployeeService;
import com.akbar.vo.EmployeeLoginVO;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/admin/employee")
@Slf4j
@Api(tags = "用户管理接口") //接口分组
public class EmployeeController {

    @Autowired
    private EmployeeService employeeService;

    /*
    * 员工登录
    * */
    @PostMapping("/login")
    @ApiOperation(value = "用户登录")  //接口描述，value可以省略
    public Result<EmployeeLoginVO> login(@RequestBody EmployeeLoginDTO employeeLoginDTO) {
        log.info("员工登录：{}", employeeLoginDTO);

        Employee employee =  employeeService.login(employeeLoginDTO);

        EmployeeLoginVO employeeLoginVO = EmployeeLoginVO.builder()
                .id(employee.getId())
                .userName(employee.getUsername())
                .name(employee.getName())
                .token(null)
                .build();

        return Result.success(employeeLoginVO);
    }
}
```

在类和类属性上面使用注解：

```java
package com.akbar.dto;

import io.swagger.annotations.ApiModel;
import io.swagger.annotations.ApiModelProperty;
import lombok.Data;

import java.io.Serializable;

@Data
@ApiModel(description = "员工登录时传递的数据模型")
public class EmployeeLoginDTO implements Serializable {

    @ApiModelProperty("用户名")
    private String username;

    @ApiModelProperty("密码")
    private String password;
}
```

# 访问api文档

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250622194850333.webp)

![](https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250622194918325.webp)
