---
layout:     post
title:      "Sublime Rapid Deployment with Cloud Synchronization between Multi-PC"
subtitle:   "多 PC 端配置环境同步实现 Sublime 快速部署"
date:       2018-1-13 12:00:00
author:     "Aaron"
header-img: "img/post-bg-CloudSublime.jpg"
header-mask: 0.6
multilingual: false
catalog: true
music: false
music-id: 16334007
tags:
    - Sublime
    - Nutstore
---

> In fact, nothing has changed, but only the differences you think.

# 前言
[Sublime Text 3](https://www.sublimetext.com/) (下面简称 Sublime ) 是一款十分优秀的代码文本编辑器，不仅可以秒开各种格式的文本文件，还自带了十分 Geek 的各种快捷键，使用者还可以方便的在系统的 ```Json``` 文件中进行各种天马行空的自定义，使用起来行云流水，可以说是十分可怕了。除此以外，使用者可以用 [Package Control](https://packagecontrol.io/) 插件对 Sublime 所支持的拓展包 (插件) 进行安装和管理，[Package Control](https://packagecontrol.io/) 里基本可以找到所有你所需要的拓展包，有能力的小伙伴甚至可以自己进行开发来实现需要的功能。

然而就算是集各种优势于一身的一款代码文本编辑器，还是难逃要被挑剔的我吐槽一番。最近由于主要在工作室的台式机办公，需要重新部署 Sublime ，那么问题就来了， Sublime 本身没有像 Google Chrome 那样的插件同步功能，我在思考是否有一劳永逸的方法能够在多台 PC 之间完成 Sublime 配置和环境的自动同步，免除繁琐的拓展包安装工作。


> **基本思路**
>
> 用网盘对 Sublime 主体文件进行同步。

思路很简单，实际尝试操作后发现还需要一些前提步骤。经过一小番折腾后完美实现这一功能，下面来看教程吧。


# 更改 Sublime **_Data_** 文件位置

Sublime 的配置文件和拓展包默认情况下会保存在 Windows 系统的 ```%appdata%``` 文件夹下，可以在 **运行 (Win + R)** 中输入 ```%appdata%``` 来方便地访问。

![winr](/img/in-post/2018-1-13-CloudSublime/winr.png)

![SDataAddress](/img/in-post/2018-1-13-CloudSublime/sDataAddress.png)

为了方便后面对 Sublime 进行整体同步，我们需要将默认的 **_Data_** 文件位置更改到 Sublime 的安装文件夹下。

从官网[下载 Sublime 安装包](https://www.sublimetext.com/3)，完成安装后先不要运行 (安装过程中的自动运行选项也需要取消勾选) ，一旦运行程序就会执行默认的 **_Data_** 文件位置。如果一不小心已经运行了，可以删除该目录下的 Sublime文件夹来弥补。到 Sublime 的安装文件夹 (```eg. D:\tools\Sublime Text 3\```) 下新建一个 **Data** 文件夹。

![NewSDAddress](/img/in-post/2018-1-13-CloudSublime/newsdaddress.png)

然后运行 Sublime ，并按照 [Package Control](https://packagecontrol.io/) 的官方 [Instalation 说明](https://packagecontrol.io/installation) 完成插件管理器 Package Control 的安装。到这一步就完成了 Sublime **_Data_** 文件位置的更改。


# Package 的安装或 **Data** 文件夹的备份迁移

完成上述 **_Data_** 文件位置的更改后，就可以进行拓展包的安装，安装的任何拓展包以及各种对 Sublime 进行自定义修改的配置文件都会保存到 ```Sublime Text 3\Data``` 文件夹下。

![NewDataFiles](/img/in-post/2018-1-13-CloudSublime/newdatafiles.png)

或者，还可以直接进行 PC 之间 **_Data_** 文件的迁移。以我个人的情况为例，就直接将笔记本电脑上 Sublime 的 **Data** 复制到台式机 ```Sublime Text 3\Data``` 文件夹中，就能轻松的完成备份迁移工作，实现快速部署和笔记本电脑上完全一样的 Sublime 配置环境。

这里需要特别注意一点，毕竟是直接复制，对于自定义的编译器地址等配置还需要相应手动修改一下。好啦，可以开始搞笑的工作啦 :)


# 多端同步

这里选用[坚果云 Nutstore](https://www.jianguoyun.com/) 对 Sublime 进行同步。同样需要注意的是对于涉及到引用地址的配置文件，不同电脑端可能不同，建议在第一次同步完成后用坚果云的 **选择性同步** 功能进行排除，并进行相应修改。这也是我选取坚果云作为同步工具的主要原因。

![jianguo](/img/in-post/2018-1-13-CloudSublime/jianguo.png)

![create](/img/in-post/2018-1-13-CloudSublime/create.png)

上传成功后可以在另一台电脑进行下载，实现多端同步。
![download](/img/in-post/2018-1-13-CloudSublime/download.png)

完成以上步骤后，各电脑端对 Sublime 的任何配置、添加拓展包等，都会实时同步，实现多端统一。


# 小结

1 &nbsp;依靠 [坚果云 Nutstore](https://www.jianguoyun.com/) 对 Sublime  进行同步来实现多端统一配置，至于网盘还是可以根据个人情况进行选择的；

2 &nbsp;同步前需要更改 Sublime 默认**_Data_** 文件位置到程序所在文件；

3 &nbsp;同步时需要排除涉及到引用地址的配置文件，建议在第一次同步完成后用坚果云的 **选择性同步** 进行排除，并手动修改；

4 &nbsp;建议对 Sublime 进行删除重装工作后再开始以上步骤，以得到一份纯净的版本来多端同步。

<center>- Boost -</center>
<center>- Over -</center>
