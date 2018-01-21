
# 前言
> 前段时间在给 Jekyll 博客加了音乐后，浏览文章确实舒服多了，但又感觉文章只能图文混排，没有图片的地方就像一片荒原没有一丝色彩，虽然不是处女座但还是不能忍。又研究了下如何在 markdown 编辑时加一些小表情。完成之后再看，这样总算感觉舒服多了。

# 添加 Emoji 表情

Jekyll pages does not support inserting Emoji, but it has a plugin system with hooks that allow you to create custom generated content specific to your site. You can run custom code for your site without having to modify the Jekyll source itself.

从这个思路切入，很自然地想到通过 Emoji 插件来实现 Jekyll 网页对 Emoji 的兼容。通过在 [RubyGems](https://rubygems.org/gems) 上对关键词 ```Emoji Jekyll``` 进行检索，发现已经有3个能够实现这一功能的插件。我试用了下载量大的 ```jemoji``` 和 ```Emoji for Jekyll``` ，都能够完美实现 Jekyll 对 Emoji 的兼容。下面以 [jemoji](https://rubygems.org/gems/jemoji) 为例，来看教程吧。

![relevent Emoji](releventEmoji.png)

![Emoji for Jekyll](emoji_for_jekyll.png)
Emoji for Jekyll: Seamlessly enable emoji for all posts and pages.
[Emoji for Jekyll](https://rubygems.org/gems/emoji_for_jekyll)

![jemoji](jemoji.png)
[jemoji](https://rubygems.org/gems/jemoji)

#### Emoji 插件安装配置

You have 2 recommanded options for installing plugins:

In your ```_config.yml``` file, add a new sentence with the key ```plugins``` (or ```gems``` for Jekyll < ```3.5.0``` ) and the values of the gem names of the plugins you’d like to use. An example:

```
# This will enable each of these plugins automatically.
plugins:
  - jekyll-gist
  - jekyll-coffeescript
  - jekyll-assets
  - another-jekyll-plugin
```




In your site source root, make a _plugins directory. Place your plugins here. Any file ending in *.rb inside this directory will be loaded before Jekyll generates your site.




However, some of the emoji codes are not super easy to remember, so here is a little cheat sheet.


<center>- &nbsp;:bird:&nbsp; -</center>
<center>- Over -</center>
