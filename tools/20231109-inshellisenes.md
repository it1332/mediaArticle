<!--
 * @Author: 钱巍
 * @Date: 2023-11-09 15:14:34
 * @LastEditTime: 2023-11-09 16:20:30
 * @LastEditors: 钱巍
 * @Description: Shell 的小插件：Inshellisense
 * @FilePath: \v2-testd:\wei.qian\projectCode\MyMedia\mediaArticle\tools\20231109-inshellisenes.md
 * @git：https://github.com/microsoft/inshellisense
 * 没有理想，何必远方。
-->

# 提升你的代码编辑效率：Microsoft InShellisense插件 

> 发布两周Stars：2K

如果你使用 `fig` 就会感觉非常亲切，因为它就是把 `fig` 底层的 `autocomplete` 单独拿出来做了一个 native runtime，支持 600 个命令。而且InShellisense也是完全开源的，这意味您不仅可以自由使用它，还可以对其进行修改和改进。

优点：

1. 支持 `Windows`、`Linux` 和 `MacOS` 
2. 没有`fig`的花里胡哨，更加简洁

缺点：

1. 需要`node >= 16.x`版本 
2. 目前只支持以下 `shell`
   - bash
   - zsh
   - fish
   - pwsh
   - powershell (Windows Powershell)

安装：

使用npm全局安装：
`npm install -g @microsoft/inshellisense`

使用：

以下以bash为例，说明如何使用InShellisense：

首先，需要设置当前窗口提示什么。在命令行中输入以下命令：

```bash
# inshellisense --shell <shell>
inshellisense --shell bash
```
设置后 看到如下界面 例如输入`git`命令就会提示相应的命令和命令简介

![inshellisense](https://cdn.jsdelivr.net/gh/it1332/mediaArticleImages@main/tools/1699516548012.png)

小伙伴们这样是不是很方便了很多呢？

附git地址：https://github.com/microsoft/inshellisense

>写在最后

**更多资源、文章请关注：IT1332**

![二维码](https://cdn.jsdelivr.net/gh/it1332/mediaArticleImages@main/wx-gzh/it1332_wx-login_b.png)












