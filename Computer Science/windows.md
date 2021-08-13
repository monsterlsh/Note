# WINDOWS

## 零碎技巧

### 解决xmind安装只能安装在c盘
[转载于此](https://blog.csdn.net/cc920095705/article/details/109111783)

#### 问题描述

> Xmind会默认安装在C盘，但我们为了解放C盘空间，会有在其他盘符统一管理安装程序的文件夹，那如何将Xmind安装在指定文件夹呢？

#### 解决步骤

1. `win` + `r` ：运行 `regedit`

2.  打开地址

`\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`

3. 在`CurrentVersion`下如上图可以看到，有两个路径配置。`Xmind`使用的是`ProgramFilesDir`这个配置项。所以修改此配置项。

4. `xmind`安装成功后记得改回默认值
