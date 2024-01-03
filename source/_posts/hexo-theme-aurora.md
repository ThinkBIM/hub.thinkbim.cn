---
title: Aurora 主题
date: 2021-05-20 12:00:00
description: 基于hexo-theme-aurora 主题
keywords: Hexo|Themes|aurora|主题
tags:
  - Themes
  - Hexo
  - Aurora
categories:
  - Hexo
top_img: false
cover: false
---

基于Hexo框架开发，使用 Aurora 主题。
[Aurora](https://github.com/auroral-ui/hexo-theme-aurora) 是使用极光颜色和 UI 元素的下一代主题。它给你平滑流畅的色彩和未来感。



- [Hexo](https://hexo.io/) 框架
- [hexo-theme-aurora](https://aurora.tridiamond.tech/zh/guide/) 主题



## 安装

### 主题&主题配置
```shell
# npm安装主题
npm install hexo-theme-aurora --save
# 主题配置模板
cp -rf ./node_modules/hexo-theme-aurora/_config.yml ./_config.aurora.yml
```





### 修改 _config.yml
```shell
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://username.github.io/project
permalink: /post/:title.html
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
  
  
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: aurora
```

### 运行环境

```shell
hexo clean & hexo g & hexo server
```

## 写作
- 推荐文章 feature: true
```shell
---
title: Article Title
date: 2020-08-15 18:49:36
tags:
  - Tag
categories:
  - Cate
cover: https://domo.png
feature: true
---
```

- 分类和标签
```shell
categories:
 - Diary
tags:
 - PS3
 - Games

# 此时这篇文章同时包括三个分类： PlayStation 和 Games 分别都是父分类 Diary 的子分类，同时 Life 是一个没有子分类的分类。
categories:
 - [Diary, PlayStation]
 - [Diary, Games]
 - [Life]
```


:::tip Tip
Tip容器
:::

:::warning Warning
Warning 容器
:::

:::danger Danger
Danger 容器
:::

:::details 点击查看

Fusce rutrum venenatis eros in hendrerit. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nullam eget risus egestas, aliquet ipsum sed, volutpat tortor. Proin finibus tortor ac mauris finibus rutrum. Nullam tincidunt arcu eu urna ullamcorper, eu ultricies turpis ornare. Morbi id sollicitudin orci. Proin lobortis vehicula nibh a ornare. Cras sodales eu ligula quis fermentum. Proin eu ultrices leo, quis iaculis justo. Sed dictum, nulla sit amet imperdiet commodo, libero sapien semper justo, ut lobortis elit nunc vitae ante. Nullam lobortis odio quam, ac condimentum elit posuere vitae. Sed ornare, odio et rutrum varius, lorem eros gravida urna, in pharetra sapien justo non magna.

- details content
- details new line

```javascript
console.log('hello world')
```

:::


## FAQ

1. 主题官网未说明 主题更改。例如 theme: aurora
2. node-14 版本兼容问题，建议使用 node-12


