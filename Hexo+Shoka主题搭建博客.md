---
title: Github Pages+Hexo搭建个人Blog
date: 2024-3-16 23:29:08
categories:
- 开发
tags:
- As Developers
---

# Github

1. Github账号
2. 创建Github仓
   - 仓库名`[username].github.io`
   - 仓库描述Description
   - ...
   - 其余保持原设置
3. 本地安装NodeJS，npm命令
4. 本地安装Git

# Hexo

`npm install -g hexo-cli`

`hexo -v`

`hexo init xh1xxhg`

`cd xh1xxhg`

`npm install`

**启动（本地测试）**

`hexo clean`该命令可以解决一些报错，比如说代码块显示不完整

[shoka主题搭建过程](https://blog.twinkling.top/2023/11/16/note/shoka%20%E4%B8%BB%E9%A2%98%E6%90%AD%E5%BB%BA%E8%BF%87%E7%A8%8B/)

`hexo g`

`hexo server`

# Shoka主题

https://github.com/amehime/hexo-theme-shoka

配置教学博客

https://shoka.lostyu.me/categories/computer-science/note/theme-shoka-doc/

`git clone https://github.com/amehime/hexo-theme-shoka.git ./themes/shoka`

# Plugins

**修改站点配置文件**

```yml
theme: landscape
=>
theme: shoka
```

**hexo-renderer-multi-markdown-it**

删除原markdown渲染器`npm un hexo-renderer-marked --save`

```
npm i hexo-renderer-multi-markdown-it --save
```

**autoprofixer**

```
npm install hexo-autoprefixer --save
```

**hexo-algoliasearch**

[Hexo集成Algolia实现搜索功能](https://blog.csdn.net/qq_45173404/article/details/122861321)

```
npm install hexo-algoliasearch --save
```

**hexo-symbols-count-time**

```
npm install hexo-symbols-count-time
```

**hexo-feed**

```
npm install hexo-feed --save-dev
```

# 根目录配置文件

在尝试中搞懂配置规则，可以将`Project/themes/shoka/example`目录下的文件copy到Hexo博客项目的根目录实现一键配置，加速对该主题建站模式的理解

## _config.yml

站点配置文件

其中对`category_map`的类别设置其实无关紧要，博客中的类别需要在书写markdown时对其进行设置

```yml
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Hexo
subtitle: subtitle
description: 描述123
keywords: 关键词1,关键词2 # edit for Theme.shoka
author: John Doe
language: zh-CN # 这里只可以选 zh-CN、zh-HK、zh-TW、ja、en 这几个格式
timezone: 'Asia/Shanghai'

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com
root: /
permalink: :title/ # edit for Theme.shoka
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link:
  enable: true # Open external links in new tab
  field: site # Apply to the whole site
  exclude: ''
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: false # edit for Theme.shoka
  line_number: true
  auto_detect: true
  tab_replace: ''
prismjs:
  enable: false # edit for Theme.shoka

# Category & Tag
default_category: uncategorized
category_map: # edit for Theme.shoka
  计算机科学: computer-science
  Java: java
  二进制杂谈: note
  零基础学Java语言-浙江大学-翁恺: course-1
  Theme Shoka Documentation: theme-shoka-doc
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: shoka # edit for Theme.shoka


# edit for Theme.shoka
autoprefixer:
  exclude:
    - '*.min.css'

markdown:
  render: # 渲染器设置
    html: false # 过滤 HTML 标签
    xhtmlOut: true # 使用 '/' 来闭合单标签 （比如 <br />）。
    breaks: true # 转换段落里的 '\n' 到 <br>。
    linkify: true # 将类似 URL 的文本自动转换为链接。
    typographer:
    quotes: '“”‘’'
  plugins: # markdown-it插件设置
    - plugin:
        name: markdown-it-toc-and-anchor
        enable: true
        options: # 文章目录以及锚点应用的class名称，shoka主题必须设置成这样
          tocClassName: 'toc'
          anchorClassName: 'anchor'
    - plugin:
        name: markdown-it-multimd-table
        enable: true
        options:
          multiline: true
          rowspan: true
          headerless: true
    - plugin:
        name: ./markdown-it-furigana
        enable: true
        options:
          fallbackParens: "()"
    - plugin:
        name: ./markdown-it-spoiler
        enable: true
        options:
          title: "你知道得太多了"

minify:
  html:
    enable: true
    stamp: false
    exclude:
      - '**/json.ejs'
      - '**/atom.ejs'
      - '**/rss.ejs'
  css:
    enable: true
    stamp: false
    exclude:
      - '**/*.min.css'
  js:
    enable: true
    stamp: false
    mangle:
      toplevel: true
    output:
    compress:
    exclude:
      - '**/*.min.js'

# algolia:
#   appId:
#   apiKey:
#   adminApiKey:
#   chunkSize: 5000
#   indexName:
#   fields:
#     - title #必须配置
#     - path #必须配置
#     - categories #推荐配置
#     - content:strip:truncate,0,4000
#     - gallery
#     - photos
#     - tags

feed:
    limit: 20
    order_by: "-date"
    tag_dir: false
    category_dir: false
    rss:
        enable: true
        template: "themes/shoka/layout/_alternate/rss.ejs"
        output: "rss.xml"
    atom:
        enable: true
        template: "themes/shoka/layout/_alternate/atom.ejs"
        output: "atom.xml"
    jsonFeed:
        enable: true
        template: "themes/shoka/layout/_alternate/json.ejs"
        output: "feed.json"
```

## package.json

```yml
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
  "hexo": {
    "version": "5.4.2"
  },
  "dependencies": {
    "hexo": "^5.0.0",
    "hexo-algoliasearch": "^0.4.2",
    "hexo-autoprefixer": "^2.0.0",
    "hexo-deployer-git": "^2.1.0",
    "hexo-feed": "^1.0.2",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-tag": "^1.0.0",
    "hexo-pagination": "^3.0.0",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-multi-markdown-it": "^0.1.5",
    "hexo-renderer-stylus": "^2.0.0",
    "hexo-server": "^2.0.0",
    "hexo-symbols-count-time": "^0.7.1",
    "hexo-util": "^2.4.0"
  }
}
```

## _config.shoka.yml

<root>/_config.shoka.yml路径下

```yml
alternate: Yume Shoka

# Assets
statics: / #//cdn.jsdelivr.net/gh/amehime/shoka@latest/

open_graph:
  #twitter_id:
  #google_plus:
  #fb_admins:
  #fb_app_id:

menu:
  home: / || home
  posts:
    default: / || feather
    archives: /archives/ || list-alt
    categories: /categories/ || th
    tags: /tags/ || tags
  friends: /friends/ || heart

# Social Links
# Usage: `Key: permalink || icon || color`
# Key is the link label showing to end users.
# Value before `||` delimiter is the target permalink,
# secend value is the name of Font icon.
social:
  github: https://github.com/amehime || github || "#191717"
  #google: https://plus.google.com/yourname || google
  twitter: https://twitter.com/amehime || twitter || "#00aff0"
  zhihu: https://www.zhihu.com/people/rurismzk || zhihu || "#1e88e5"
  music: https://music.163.com/#/user/home?id=12886823 || cloud-music || "#e60026"
  weibo: https://weibo.com/amehime || weibo || "#ea716e"
  about: https://about.me/amehime || address-card || "#3b5998"
  #email: mailto:yourname@mail.com || envelope || "#55acd5"
  #facebook: https://www.facebook.com/yourname || facebook
  #stackoverflow: https://stackoverflow.com/yourname || stack-overflow
  #youtube: https://youtube.com/yourname || youtube
  #instagram: https://instagram.com/yourname || instagram
  #skype: skype:yourname?call|chat || skype
  #douban: https://www.douban.com/people/yourname/ || douban

footer:
  # Specify the date when the site was setup. If not defined, current year will be used.
  since: 2010
  count: true

post:
  count: true


# ---------------------------------------------------------------
# Third Party Plugins & Services Settings
# ---------------------------------------------------------------

# Comments
# Valine
# For more information: https://valine.js.org, https://github.com/xCss/Valine
valine:
  appId: #这里不要忘了改
  appKey: #这里不要忘了改
  placeholder: ヽ(○´∀`)ﾉ♪ # Comment box placeholder
  pageSize: 10 # Pagination size
  lang: zh-CN
  tagMember:
    master:
      # - deea5a8d259d17182a53be1772e4c182
    friend:
      - deea5a8d259d17182a53be1772e4c182

# bgm
# audio:


# Dependencies: https://github.com/amehime/hexo-renderer-multi-markdown-it
pangu: true

# ---------------------------------------------------------------
# analytics & SEO Settings
# ---------------------------------------------------------------


# Disable Baidu transformation on mobile devices.
disable_baidu_transformation: true

# Automatically add external URL with Base64 encrypt & decrypt.
exturl: true

# 自动滚动上次浏览的位置
auto_scroll: true

# 夜间模式
darkmode: true

# 是否显示页面加载动画 loading-cat
loader:
  start: true # 当初次打开页面时，显示加载动画
  switch: true # tab 切换到其他页面时，显示加载动画
  
# 单机页面特效
fireworks:
  enable: true # 是否启用
  color: # 烟花颜色
    - "rgba(255,182,185,.9)"
    - "rgba(250,227,217,.9)"
    - "rgba(187,222,214,.9)"
    - "rgba(138,198,209,.9)"
    
# 加载谷歌字体
font:
  enable: true
  # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: x.x`. Use `em` as unit. Default: 1 (16px)

  # Global font settings used for all elements inside <body>.
  global:
    external: true
    family: Mulish
    size:

  # Font settings for alternate title.
  logo:
    external: true
    family: Fredericka the Great
    size: 3.5

  # Font settings for site title.
  title:
    external: true
    family: Noto Serif JP
    size: 2.5

  # Font settings for headlines (<h1> to <h6>).
  headings:
    external: true
    family: Noto Serif SC
    size:

  # Font settings for posts.
  posts:
    external: true
    family:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family: Inconsolata
```

# 发布到Github Pages

`npm install hexo-deployer-git --save`

修改根目录下的 `_config.yml`，配置 `GitHub` 相关信息

```
deploy:
  type: git
  repo: https://github.com/Xh1Xxhg/Xh1Xxhg.github.io.git
  branch: main
  token: ghp_xxxxxxxxxxxxxxxxxxx(自己生成)
```

token生成

![image-20240229150023484](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20240229150023484.png)

`hexo g -d`部署

直接访问即可

https://<yourname>.github.io/

# 发布文章

清空根目录/public目录所有文件，重新

`hexo g`

`hexo server`

`hexo g -d`