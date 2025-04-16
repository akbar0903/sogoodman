---
title: Hexo Markdown语法
date: 2025-04-13 20:17:12
sticky: 100
tags: ['Markdown', 'Hexo', 'Butterfly']
categories: 'Markdown 语法'
cover: https://blog-ultimate.oss-cn-beijing.aliyuncs.com/article-image/20250413202233995.png
---

# 新建
hexo中有三种模板：
- post：文章
- draft：草稿
- page：页面

新建一个（文章，草稿，页面）命令：
```shell
hexo new [模板，比如post] ["title，比如:优秀项目学习"] --path [指定路径，比如:vue/优秀项目学习]
```

# 页面配置
> butterfly官方文档：https://butterfly.js.org/posts/dc584b87/

## Page Front-matter

```yml
---
title:                # 【必需】页面标题
date:                 # 【必需】页面创建日期
updated:              # 【可选】页面更新日期
type:                 # 【必需】标签、分类和友情链接三个页面需要配置
comments:             # 【可选】显示页面评论模块 (默认 true)
description:          # 【可选】页面描述
keywords:             # 【可选】页面关键字
top_img:              # 【可选】页面顶部图片
mathjax:              # 【可选】显示 mathjax (当设置 mathjax 的 per_page: false 时，才需要配置，默认 false)
katex:                # 【可选】显示 katex (当设置 katex 的 per_page: false 时，才需要配置，默认 false)
aside:                # 【可选】显示侧边栏 (默认 true)
aplayer:              # 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的音乐 配置
highlight_shrink:     # 【可选】配置代码框是否展开 (true/false) (默认为设置中 highlight_shrink 的配置)
random:               # 【可选】配置友情链接是否随机排序（默认为 false）
limit:                # 【可选】配置说说显示数量
  type:               # 【可选】配置说说显示数量的类型 （date 或者 num）
  value:              # 【可选】配置说说显示数量的值
---
```

## Post Front-matter
```yml
---
title:                    # 【必需】文章标题
date:                     # 【必需】文章创建日期
updated:                  # 【可选】文章更新日期
tags:                     # 【可选】文章标签
categories:               # 【可选】文章分类
sticky:                   # 【可选】是否置顶文章，比如sticky：100排在最上面，sticky：99排在100的下面
keywords:                 # 【可选】文章关键字
description:              # 【可选】文章描述
top_img:                  # 【可选】文章顶部图片
comments:                 # 【可选】显示文章评论模块(默认 true)
cover:                    # 【可选】文章缩略图(如果没有设置 top_img,文章页顶部将显示缩略图，可设为 false/图片地址/留空)
toc:                      # 【可选】显示文章 TOC(默认为设置中 toc 的 enable 配置)
toc_number:               # 【可选】显示 toc_number(默认为设置中 toc 的 number 配置)
toc_style_simple:         # 【可选】显示 toc 简洁模式
copyright:                # 【可选】显示文章版权模块(默认为设置中 post_copyright 的 enable 配置)
copyright_author:         # 【可选】文章版权模块的文章作者
copyright_author_href:    # 【可选】文章版权模块的文章作者链接
copyright_url:            # 【可选】文章版权模块的文章连结链接
copyright_info:           # 【可选】文章版权模块的版权声明文字
mathjax:                  # 【可选】显示 mathjax(当设置 mathjax 的 per_page: false 时，才需要配置，默认 false )
katex:                    # 【可选】显示 katex (当设置 katex 的 per_page: false 时，才需要配置，默认 false )
aplayer:                  # 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的音乐 配置
highlight_shrink:         # 【可选】配置代码框是否展开(true/false)(默认为设置中 highlight_shrink 的配置)
aside:                    # 【可选】显示侧边栏 (默认 true)
abcjs:                    # 【可选】加载 abcjs (当设置 abcjs 的 per_page: false 时，才需要配置，默认 false )
noticeOutdate:            # 【可选】文章过期提醒 (默认为设置中 noticeOutdate 的 enable 配置)
---
```

# 标签外挂

## CodeBlock
### 使用三重反引号
**语法：**
```markdown
``` [language] [title]```
```

**比如（注意，双引号""你不用写）：**
```markdown
"```javascript javascript 示例代码
console.log("hello world")
```"
```

```javascript javascript 示例代码
console.log("hello world")
```

### 使用hexo的标签外挂
**语法：**
```markdown
{% codeblock [lang:language] [title] [mark:number] %}
code snippet
{% endcodeblock %}
```
| 参数       | 解释                                                                                |
| --------- | ----------------------------------------------------------------------------------|
| lang:language       | 语言，比如lang:javascript                          |
| title               | 代码块标题                                         |
| line_number         | 显示行号，默认true                                  |
| mark:number         | 突出显示特定的行，每个值用逗号分隔。 使用破折号指定数字范围例如： mark:1,4-7,10 将标记第1、4至7和10行                                 |

**比如：**
```markdown
{% codeblock lang:typescript typescript代码示例 line_number:false mark:1 %}
console.log("hello world")
{%endcodeblock%}
```
{% codeblock lang:typescript typescript代码示例 line_number:false mark:1 %}
console.log("hello world")
{%endcodeblock%}

### 代码差异
**记得去掉双引号""**
```markdown
"```diff
function hello() {
-  return "world";
+  return "Hexo";
}
```"
```

```diff
function hello() {
-  return "world";
+  return "Hexo";
}
```

## Note
### simple
**语法：**
```markdown
{% note simple %}
默认 提示块标签
{% endnote %}

{% note default simple %}
default 提示块标签
{% endnote %}

{% note primary simple %}
primary 提示块标签
{% endnote %}

{% note success simple %}
success 提示块标签
{% endnote %}

{% note info simple %}
info 提示块标签
{% endnote %}

{% note warning simple %}
warning 提示块标签
{% endnote %}

{% note danger simple %}
danger 提示块标签
{% endnote %}
```
**效果：**
{% note simple %}
默认 提示块标签
{% endnote %}

{% note default simple %}
default 提示块标签
{% endnote %}

{% note primary simple %}
primary 提示块标签
{% endnote %}

{% note success simple %}
success 提示块标签
{% endnote %}

{% note info simple %}
info 提示块标签
{% endnote %}

{% note warning simple %}
warning 提示块标签
{% endnote %}

{% note danger simple %}
danger 提示块标签
{% endnote %}

### modern
**语法：**
```markdown
{% note modern %}
默认 提示块标签
{% endnote %}

{% note default modern %}
default 提示块标签
{% endnote %}

{% note primary modern %}
primary 提示块标签
{% endnote %}

{% note success modern %}
success 提示块标签
{% endnote %}

{% note info modern %}
info 提示块标签
{% endnote %}

{% note warning modern %}
warning 提示块标签
{% endnote %}

{% note danger modern %}
danger 提示块标签
{% endnote %}
```
**效果：**
{% note modern %}
默认 提示块标签
{% endnote %}

{% note default modern %}
default 提示块标签
{% endnote %}

{% note primary modern %}
primary 提示块标签
{% endnote %}

{% note success modern %}
success 提示块标签
{% endnote %}

{% note info modern %}
info 提示块标签
{% endnote %}

{% note warning modern %}
warning 提示块标签
{% endnote %}

{% note danger modern %}
danger 提示块标签
{% endnote %}

### flat
**语法：**
```markdown
{% note flat %}
默认 提示块标签
{% endnote %}

{% note default flat %}
default 提示块标签
{% endnote %}

{% note primary flat %}
primary 提示块标签
{% endnote %}

{% note success flat %}
success 提示块标签
{% endnote %}

{% note info flat %}
info 提示块标签
{% endnote %}

{% note warning flat %}
warning 提示块标签
{% endnote %}

{% note danger flat %}
danger 提示块标签
{% endnote %}
```
**效果：**
{% note flat %}
默认 提示块标签
{% endnote %}

{% note default flat %}
default 提示块标签
{% endnote %}

{% note primary flat %}
primary 提示块标签
{% endnote %}

{% note success flat %}
success 提示块标签
{% endnote %}

{% note info flat %}
info 提示块标签
{% endnote %}

{% note warning flat %}
warning 提示块标签
{% endnote %}

{% note danger flat %}
danger 提示块标签
{% endnote %}

### disabled
**语法：**
```markdown
{% note disabled %}
默认 提示块标签
{% endnote %}

{% note default disabled %}
default 提示块标签
{% endnote %}

{% note primary disabled %}
primary 提示块标签
{% endnote %}

{% note success disabled %}
success 提示块标签
{% endnote %}

{% note info disabled %}
info 提示块标签
{% endnote %}

{% note warning disabled %}
warning 提示块标签
{% endnote %}

{% note danger disabled %}
danger 提示块标签
{% endnote %}
```
**效果：**
{% note disabled %}
默认 提示块标签
{% endnote %}

{% note default disabled %}
default 提示块标签
{% endnote %}

{% note primary disabled %}
primary 提示块标签
{% endnote %}

{% note success disabled %}
success 提示块标签
{% endnote %}

{% note info disabled %}
info 提示块标签
{% endnote %}

{% note warning disabled %}
warning 提示块标签
{% endnote %}

{% note danger disabled %}
danger 提示块标签
{% endnote %}

### no-icon
**语法：**
```markdown
{% note no-icon %}
默认 提示块标签
{% endnote %}

{% note default no-icon %}
default 提示块标签
{% endnote %}

{% note primary no-icon %}
primary 提示块标签
{% endnote %}

{% note success no-icon %}
success 提示块标签
{% endnote %}

{% note info no-icon %}
info 提示块标签
{% endnote %}

{% note warning no-icon %}
warning 提示块标签
{% endnote %}

{% note danger no-icon %}
danger 提示块标签
{% endnote %}
```
**效果：**
{% note no-icon %}
默认 提示块标签
{% endnote %}

{% note default no-icon %}
default 提示块标签
{% endnote %}

{% note primary no-icon %}
primary 提示块标签
{% endnote %}

{% note success no-icon %}
success 提示块标签
{% endnote %}

{% note info no-icon %}
info 提示块标签
{% endnote %}

{% note warning no-icon %}
warning 提示块标签
{% endnote %}

{% note danger no-icon %}
danger 提示块标签
{% endnote %}

## Button
| 参数       | 解释                                                                                |
| --------- | ----------------------------------------------------------------------------------|
| url       | 【必须】链接地址                                                                    |
| text      | 【必须】按钮文字                                                                    |
| icon      | 【可选】图标                                                                         |
| color     | 【可选】按钮背景顔色（默认 style 时）按钮字体和边框顔色(outline 时)配置： default/blue/pink/red/purple/orange/green               |
| style     | 【可选】按钮样式 默认实心配置： outline/留空                                                |
| layout    | 【可选】按钮佈局 默认为 line配置： block/留空                                          |
| position  | 【可选】按钮位置 前提是设置了 layout 为 block 默认为左边配置： center/right/留空         |
| size      | 【可选】按钮大小配置： larger/留空                                                          |

```markdown
{% btn 'https://butterfly.js.org/',Butterfly %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right %}
{% btn 'https://butterfly.js.org/',Butterfly,,outline %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,larger %}
```
{% btn 'https://butterfly.js.org/',Butterfly %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right %}
{% btn 'https://butterfly.js.org/',Butterfly,,outline %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,larger %}

---

```markdown
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block center larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block right outline larger %}
```
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block center larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,block right outline larger %}

---

```markdown
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,blue larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,pink larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,red larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,purple larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,orange larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,green larger %}
```
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,blue larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,pink larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,red larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,purple larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,orange larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,green larger %}

---

```markdown
<div class="btn-center">
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline blue larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline pink larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline red larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline purple larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline orange larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline green larger %}
</div>
```
<div class="btn-center">
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline blue larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline pink larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline red larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline purple larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline orange larger %}
{% btn 'https://butterfly.js.org/',Butterfly,far fa-hand-point-right,outline green larger %}
</div>

## Label
{% note warning modern %}
建议 不要 在段落开头使用 label 标签外挂
{% endnote %}

**语法：**
```markdown
{% label text color %}
```
| 参数       | 解释                                                                                |
| --------- | ----------------------------------------------------------------------------------|
| text       | 文字                                                                   |
| color      |【可选】背景颜色，默认为 defaultdefault/blue/pink/red/purple/orange/green                                          |

**比如：**
```markdown
臣亮言：{% label 先帝 %}创业未半，而{% label 中道崩殂 blue %}。今天下三分，{% label 益州疲敝 pink %}，此诚{% label 危急存亡之秋 red %}也！然侍衞之臣，不懈于内；{% label 忠志之士 purple %}，忘身于外者，盖追先帝之殊遇，欲报之于陛下也。诚宜开张圣听，以光先帝遗德，恢弘志士之气；不宜妄自菲薄，引喻失义，以塞忠谏之路也。
宫中、府中，俱为一体；陟罚臧否，不宜异同。若有{% label 作奸 orange %}、{% label 犯科 green %}，及为忠善者，宜付有司，论其刑赏，以昭陛下平明之治；不宜偏私，使内外异法也。
```
臣亮言：{% label 先帝 %}创业未半，而{% label 中道崩殂 blue %}。今天下三分，{% label 益州疲敝 pink %}，此诚{% label 危急存亡之秋 red %}也！然侍衞之臣，不懈于内；{% label 忠志之士 purple %}，忘身于外者，盖追先帝之殊遇，欲报之于陛下也。诚宜开张圣听，以光先帝遗德，恢弘志士之气；不宜妄自菲薄，引喻失义，以塞忠谏之路也。
宫中、府中，俱为一体；陟罚臧否，不宜异同。若有{% label 作奸 orange %}、{% label 犯科 green %}，及为忠善者，宜付有司，论其刑赏，以昭陛下平明之治；不宜偏私，使内外异法也。

## Flink
> 可以呈现类似友情链接列表效果，还可以作为网页链接

**语法：**
```markdown
{% flink %}
xxxxxx
{% endflink %}
```
**比如：**
```markdown
{% flink %}
- class_name: 友情链接
  class_desc: 那些人，那些事
  link_list:
    - name: JerryC
      link: https://jerryc.me/
      avatar: https://jerryc.me/img/avatar.png
      descr: 今日事,今日毕
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、简单且强大的网志框架

- class_name: 网站
  class_desc: 值得推荐的网站
  link_list: 
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中国最大社交分享平台 
{% endflink %}
```
{% flink %}
- class_name: 友情链接
  class_desc: 那些人，那些事
  link_list:
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、简单且强大的网志框架

- class_name: 网站
  class_desc: 值得推荐的网站
  link_list: 
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中国最大社交分享平台 
{% endflink %}
