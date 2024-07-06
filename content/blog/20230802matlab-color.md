---
title: "更换 MATLAB 编辑器配色"
date: 2023-08-02
slug: 2023/08/02/matlab-color
summary: 白色的 MATLAB 界面看久了，眼睛会很累，所以更换一下配色吧！这里有两种更换 MATLAB 编辑器配色的方式。
categories: 
  - Misc
---

## 方案 1：直接修改配色

[配色来源](https://blog.csdn.net/wayne6515/article/details/122530882)

{{<figure src="/contents/blog/20230802-1.png" caption="Figure 1">}}

{{<figure src="/contents/blog/20230802-2.png" caption="Figure 2">}}

{{<figure src="/contents/blog/20230802-3.png" caption="Figure 3">}}

{{<figure src="/contents/blog/20230802-4.png" caption="Figure 4">}}



## 方案 2：使用已有的配色

操作流程：

- 在 MATLAB 命令行中运行 prefdir， 获取 matlab.prf 文件所在路径并打开，找到 matlab.prf 文件， 作备份，命名为matlabdefault.prf，以便于后续换回默认配色方案

- [下载配色方案](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/scottclowe/matlab-schemes#monokai)

  - 解压后，打开文件夹内的 [README.md](http://readme.md/)，可以看到很多配色方案，选择喜欢的配色方案对应的.prf文件，将其重命名为 matlab.prf，然后复制到上述 matlabdefault.prf 所在的文件夹
  - 配色方案 Github 仓库地址 https://github.com/scottclowe/matlab-schemes#monokai

- 重启 MATLAB 后即可生效。