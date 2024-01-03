---
title: Liunx问题总结
date: 2021-07-22
description: 解决GitLab内存消耗大的问题
keywords: GitLab内存消耗大的问题|内存消耗
tags:
  - F&Q 
  - Liunx
categories:
  - Liunx
top_img: false
cover: false
---
  
## sed和awk有啥区别
sed是流编辑器，而awk是文本格式化工具，报告生成器
如果文件是格式化的，即由分隔符分为多个域的，优先使用awk
awk适合对文件的抽取整理，sed适合对文件的编辑。
awk适合按列（域）操作，sed适合按行操作
sed：每次读入一行来处理的，sed 适合简单的文本替换和搜索，sed读取一行，以行作为单位，进行处理。
awk：每次读入一行来处理的（同sed），但awk读取一行，切割成字段，以字段（列）为单位，进行细节处理。

## Liunx问题总结

[解决GitLab内存消耗大的问题](https://blog.csdn.net/ouyang_peng/article/details/84066417?utm_term=gitlab%E5%86%85%E5%AD%98%E4%B8%8D%E8%B6%B3&utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduweb~default-0-84066417&spm=3001.4430)

