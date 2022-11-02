---
title: Butterfly 主题
date: 2022-11-02
description: 基于hexo-theme-butterfly主题，部署自己个博客系统
keywords: Hexo|Themes|butterfly|主题
tags:
  - Themes
categories:
  - Hexo
---

基于Hexo框架开发，使用 [Butterfly](https://github.com/jerryc127/hexo-theme-butterfly) 主题。




- [Hexo](https://hexo.io/) 框架
- [hexo-theme-butterfly](https://butterfly.js.org/) 文档



## 安装

### 主题&主题配置
```
# npm安装主题
npm install hexo-theme-butterfly --save
# 主题配置模板
cp -rf ./node_modules/hexo-theme-butterfly/_config.yml ./_config.butterfly.yml
```





### 修改 _config.yml
```
theme: butterfly
```

### 运行环境

```shell
hexo clean & hexo g & hexo server
```

## 写作

### 页面

|                  | 解释                                                        |
|------------------|-----------------------------------------------------------|
| title            | 【必需】页面标题                                                  |
| date             | 【必需】创建日期                                                  |
| type             | 【必需】标签、分类和友情链接需要配置                                        |
| updated          | 【可选】页面更新日期                                                |
| description      | 【可选】页面描述                                                  |
| keywords         | 【可选】页面关键字                                                 |
| comments         | 【可选】显示页面评论模块(默认 true)                                     |
| top_img          | 【可选】页面顶部图片                                                |
| mathjax          | 【可选】显示mathjax(当设置mathjax的per_page: false时，才需要配置，默认 false) |
| katex            | 【可选】显示katex(当设置katex的per_page: false时，才需要配置，默认 false)     |
| aside            | 【可选】显示侧边栏 (默认 true)                                       |
| aplayer          | 【可选】在需要的页面加载aplayer的js和css,請參考文章下面的音樂 配置                  |
| highlight_shrink | 【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)      |

### 文章


| 写法	                   | 解释                                                         |
|-----------------------|------------------------------------------------------------|
| title                 | 	【必需】文章标题                                                  |
| date                  | 	【必需】文章创建日期                                                |
| updated               | 	【可选】文章更新日期                                                |
| tags                  | 	【可选】文章标题                                                  |
| categories            | 	【可选】文章分类                                                  |
| keywords              | 	【可选】文章关键字                                                 |
| description           | 	【可选】文章描述                                                  |
| top_img               | 	【可选】文章顶部图片                                                |
| cover                 | 	【可选】文章缩略图(如果沒有设置top_img,文章頁顶部将显示缩略图，可设为false/图片地址/留空)     |
| comments              | 	【可选】显示文章评论模块(默认 true)                                     |
| toc                   | 	【可选】显示文章TOC(默认为设置中toc的enable配置)                           |
| toc_number            | 	【可选】显示toc_number(默认为设置中toc的number配置)                      |
| toc_style_simple      | 	【可选】显示 toc 简洁模式                                           |
| copyright             | 	【可选】显示文章版权模块(默认为设置中post_copyright的enable配置)               |
| copyright_author      | 	【可选】文章版权模块的文章作者                                           |
| copyright_author_href | 	【可选】文章版权模块的文章作者链接                                         |
| copyright_url         | 	【可选】文章版权模块的文章连接链接                                         |
| copyright_info        | 	【可选】文章版权模块的版权声明文字                                         |
| mathjax               | 	【可选】显示mathjax(当设置mathjax的per_page: false时，才需要配置，默认 false) |
| katex                 | 	【可选】显示katex(当设置katex的per_page: false时，才需要配置，默认 false)     |
| aplayer               | 	【可选】在需要的页面加载aplayer的js和css,請參考文章下面的音樂 配置                  |
| highlight_shrink      | 	【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)      |
| aside                 | 	【可选】显示侧边栏 (默认 true)                                       |


## FAQ



