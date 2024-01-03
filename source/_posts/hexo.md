---
title: Butterfly主题相关文章标签使用实例
date: 2022-11-04
description: 
keywords: 
tags:
  - Hexo
  - Themes
categories:
  - Hexo
top_img: false
cover: false
---

Mermaid便签可以绘制Flowchart（流程图）、Sequence diagram（时序图 ）、Class Diagram（类别图）、State Diagram（状态图）、Gantt（甘特图）和Pie Chart（圆形图）
Gallery 相册、图库，Tag。 flink可以在任何界面插入类似友情链接列表


## Gallery相册图库
> [SMMS](https://sm.ms/) 图床上传工具是smms的一种,SMMS图床上传工具绿色版是一款相当出色的SMMS图床专用批量上传工具。
> [SMMS国内地址](https://smms.app/)

### 图库
```markdown
<div class="gallery-group-main">
{% galleryGroup name description link img-url %}
</div>
```
- name：图库名字
- description：图库名字描述
- link：连接到相册地址
- img-url：图库封面的地址

> Demo
<div class="gallery-group-main">
{% galleryGroup '壁紙' '收藏的一些壁紙' '404' https://i.loli.net/2019/11/10/T7Mu8Aod3egmC4Q.png %}
</div>

### 相册
```markdown
{% gallery %}
![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
![](https://i.loli.net/2019/12/25/ryLVePaqkYm4TEK.jpg)
![](https://i.loli.net/2019/12/25/gEy5Zc1Ai6VuO4N.jpg)
{% endgallery %}
```
> Demo

{% gallery %}
![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
![](https://i.loli.net/2019/12/25/ryLVePaqkYm4TEK.jpg)
![](https://i.loli.net/2019/12/25/gEy5Zc1Ai6VuO4N.jpg)
{% endgallery %}

### InlineImg

```markdown
我覺得很漂亮 {% inlineImg https://i.loli.net/2021/03/19/5M4jUB3ynq7ePgw.png 150px %}
```
> Demo

我覺得很漂亮 {% inlineImg https://i.loli.net/2021/03/19/5M4jUB3ynq7ePgw.png 150px %}




## Tag-hide

```markdown
{% hideToggle Butterfly安裝方法 %}
在你的博客根目錄裏
{% endhideToggle %}
```
> Demo

{% hideToggle Butterfly安裝方法 %}
在你的博客根目錄裏
{% endhideToggle %}

## Mermaid
> 使用mermaid便签可以绘制Flowchart（流程图）、Sequence diagram（时序图 ）、Class Diagram（类别图）、State Diagram（状态图）、Gantt（甘特图）和Pie Chart（圆形图），具体可以查看[文档](https://mermaid-js.github.io/mermaid/#/)

```markdown
{% mermaid %}
pie
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
{% endmermaid %}
```

> Demo

{% mermaid %}
flowchart LR
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{% endmermaid %}


## Tabs
```markdown
{% tabs test4 %}
<!-- tab 第一個Tab -->
**tab名字為第一個Tab**
<!-- endtab -->

<!-- tab @fab fa-apple-pay -->
**只有图标 沒有Tab名字**
<!-- endtab -->

<!-- tab 炸彈@fas fa-bomb -->
**名字+icon**
<!-- endtab -->
{% endtabs %}
```

> Demo

{% tabs test4 %}
<!-- tab 第一個Tab -->
**tab名字為第一個Tab**
<!-- endtab -->

<!-- tab @fab fa-apple-pay -->
**只有图标 沒有Tab名字**
<!-- endtab -->

<!-- tab 炸彈@fas fa-bomb -->
**名字+icon**
<!-- endtab -->
{% endtabs %}

## Label
> 高亮显示所需文字

```markdown
{% label text color %}
```
- text 文字
- color 颜色

> Demo

臣亮言：{% label 先帝 %}创业未半，而{% label 中道崩殂 blue %}。今天下三分，{% label 益州疲敝 pink %}，此诚{% label 危急存亡之秋 red %}也！然侍衞之臣，不懈于内；{% label 忠志之士 purple %}，忘身于外者，盖追先帝之殊遇，欲报之于陛下也。诚宜开张圣听，以光先帝遗德，恢弘志士之气；不宜妄自菲薄，引喻失义，以塞忠谏之路也。
宫中、府中，俱为一体；陟罚臧否，不宜异同。若有{% label 作奸 orange %}、{% label 犯科 green %}，及为忠善者，宜付有司，论其刑赏，以昭陛下平明之治；不宜偏私，使内外异法也。


## Timeline

```markdown
{% timeline 2022 %}
<!-- timeline 01-02 -->
這是測試頁面
<!-- endtimeline -->
{% endtimeline %}
```
> Demo

{% timeline 2022 %}
<!-- timeline 01-02 -->
這是測試頁面
<!-- endtimeline -->
{% endtimeline %}

## Flink

```markdown
{% flink %}
- class_name: 友情连接
  class_desc: 那些人，那些事
  link_list:
    - name: JerryC
      link: https://jerryc.me/
      avatar: https://jerryc.me/img/avatar.png
      descr: 今日事,今日畢
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、簡單且強大的網誌框架

- class_name: 网站
  class_desc: 值得推荐
  link_list:
    - name: Youtube
      link: https://www.youtube.com/
      avatar: https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png
      descr: 视频
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中國最大社交分享平台
    - name: Twitter
      link: https://twitter.com/
      avatar: https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png
      descr: 社交分享平台 
{% endflink %}
```
> Demo

{% flink %}
- class_name: 友情连接
  class_desc: 那些人，那些事
  link_list:
    - name: ThinkBIM
      link: https://hub.thinkbim.cn/
      avatar: https://s2.loli.net/2022/11/07/JutlITnLafkAc58.png
      descr: ThinkBIM个人网站
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、简单且强大的网志框架

- class_name: 网站
  class_desc: 值得推荐
  link_list:
    - name: Youtube
      link: https://www.youtube.com/
      avatar: https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png
      descr: 视频
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中國最大社交分享平台
    - name: Twitter
      link: https://twitter.com/
      avatar: https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png
      descr: 社交分享平台
{% endflink %}