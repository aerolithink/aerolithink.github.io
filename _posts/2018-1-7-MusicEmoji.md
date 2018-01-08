---
layout:     post
title:      "Add CloudMusic to Your Jekyll Blog"
subtitle:   "给Jekyll博客添加网易云音乐"
date:       2018-1-7 12:00:00
author:     "Aaron"
header-img: "img/post-bg-JekyllCloudmusic.jpg"
header-mask: 0.2
multilingual: false
catalog: true
music: true
music-id: 458725076
tags:
    - Jekyll
    - 网易云音乐
    - HTML

---


> “音乐是有颜色的吧。”
>
> “废话……”


# 前言
完成了 **GitHub + Jekyll** 的个人博客搭建后，总觉得纯静态的页面有点单调，这时耳边正循环着 [better - Ｅｅｖｅｅ](http://music.163.com/#/song?id=458725076) ，灵感突现，想要better？先给博客加点音乐吧！

# 添加音乐
行动之前，考虑了两种可能实现网页页面添加音乐的解决方案：
- [ ] &nbsp;编写播放器控件，再加载到网页上
- &radic; &nbsp; 直接用现成的外链播放器，就像微信公众号上那些文章里的那样

第一种方法看起来很简单，网络上也有很多大神写好的播放器控件，可以直接载来改改用，但我不知道Jekyll的静态博客对这些控件的兼容性怎么样，目前也没有相关可以参考的教程。如果自己编写，以自己小白选手的能力估计无法完成，为了避免踩坑就果断地放弃了这个思路。

第二种方法直接调用音乐网站的API，以外链播放器的形式加载到自己的页面，对于前一种方法，这一方法毫无疑问更值得一试。

基于自身能力和以上的考虑，我最终选择了在博客里引入**网易云音乐模块**来添加音乐的解决方案。

下面来看方法吧 :)

#### 生成外链播放器
**网易云音乐**里每首歌都支持生成外链播放器（除了有些版权保护），具体方法是登入网页版的[网易云音乐](http://music.163.com/)，在右上角搜索框搜索想要的曲目，这里继续以 [better - Ｅｅｖｅｅ](http://music.163.com/#/song?id=458725076)为例。

<img src="/img/in-post/2018-1-7-MusicEmoji/search.png" width="350" height="100" />

---

![](/img/in-post/2018-1-7-MusicEmoji/find.png)

---

点击“生成外链播放器”

![](/img/in-post/2018-1-7-MusicEmoji/generate.png)

---

就会跳转到下图的页面

![](/img/in-post/2018-1-7-MusicEmoji/detail.png)

在上方选择“iframe插件”，马上下方就生成了现成的HTML代码！不得不说网易云音乐对开发者还是很友好的，在页面中部可以对播放器的尺寸、播放模式进行直接修改，中上部的播放器预览图和下方的HTML代码会相应的自动更新生成。

我们最终需要的就是底下的 &lt;iframe&gt; 代码，熟悉 HTML 内联框架的小伙伴也可以直接修改其中的参数。

```html
<iframe frameborder="no" border="0" marginwidth="0"
marginheight="0" width=330 height=86
src="//music.163.com/outchain/player?type=2&id=458725076&auto=1&height=66">
</iframe>
```

将 &lt;iframe&gt; 代码复制到 **post.html** 布局文件中，放在想要的位置。我希望大家一点开博文就能看到播放器和曲目，因此我把这段代码放在了正文 content 的上面，正如你进来时看到的那样。至此，外链播放器就可以开始工作了。

#### 自定义曲目
上面的步骤实现了外链播放器在页面的播放功能，但由于我们是将一首歌的外链放到了 **post.html** 布局文件中，会出现一个问题——所有的文章都只能播放这首 [better - Ｅｅｖｅｅ](http://music.163.com/#/song?id=458725076)（单曲循环功能哈哈哈），最好的情况是能够实现单独为每篇文章设定曲目。

先来研究下这段 &lt;iframe&gt; 代码的内容

```html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86
src="//music.163.com/outchain/player?type=2&id=458725076&auto=1&height=66">
</iframe>
```
跳过前面width，height等基础格式，我们会发现source地址内有 **id=458725076** 一项，实际上这就是对应歌曲的id号了。那么思路就有了，只需要更改id号就能控制播放的曲目。

要实现为每一篇博文定义曲目，只需要将 **id=458725076** 改为 **id={{ page.music-id }}** ，同时在markdown文档的头文件中添加 **music-id: XXXXX** 配置项，将曲面的外链中的id号复制进去，就可以轻松的为每一篇文章设置曲目了。

完整代码如下：
```html
<!-- CloudMusic -->
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86
src="//music.163.com/outchain/player?type=2&id={{ page.music-id }}&auto=1&height=66">
</iframe>
```

此外，外链中的 **“auto=1”** 可以控制自动播放与否，当值为 1 即打开网页就自动播放，值为 0 时需要访客手动点击播放。

# 更进一步

同样由于我们是将外链放到了 **post.html** 布局文件中，每篇文章就都必须配置一个 **music-id: XXXXXX** （必须有一首曲目），否则就会报错。可以在 **post.html** 布局文件中加一个 if 语句让播放器更智能一点：


```html
<!-- CloudMusic -->
{ % if page.music % }    <!-- 不知道什么bug得加个空格才显示，“{ %”之间的空格需要删除 -->
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86
src="//music.163.com/outchain/player?type=2&id={{ page.music-id }}&auto=1&height=66">
</iframe>
{ % endif % }    <!-- “{ %”之间的空格需要删除 -->
```

这样当 **music-id:** 参数为空时，播放器就会关闭（不加载）。

此外，还有很多玩法，比如编辑一个 _favoriteidlist_，再加一个 loop 语句来循环你的最爱曲目（哈哈哈前提是有人在你博客呆足够长的时间，或者是特地来听音乐的，不然就鸡肋了）。

再者，可以生成随机 id 来实现歌曲随机播放（没具体研究过网易云的曲目 id，我担心生成的 id 会没有对应曲目，那样的话还可以用爬虫爬取 id 来实现）。

结合以上两者实现随机播放最爱曲目好像会不错的样子。

# 小结

1 &nbsp;主要依靠[网易云音乐](http://music.163.com/)的外链播放器代码来实现网页播放器的插入。实际上，[虾米](http://www.xiami.com/)、[酷狗](http://www.kugou.com/)等网站也都可以生成外链，但还需要做一些转换工作，基本的方法大同小异，可以根据个人情况进行选择；

2 &nbsp;修改 id 对曲目进行更改；

3 &nbsp;将外链中的 **id=XXXXXX** 改为 **id={{ page.music-id }}** ，就可以单独对每篇博文中对 id 进行配置来自定义曲目;

4 &nbsp;还有很多可以折腾的，来点首歌吧。



<center>~&nbsp; Over &nbsp;~</center>
