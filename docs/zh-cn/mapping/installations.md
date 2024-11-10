# 工具安装与配置

!!! note "下载资源"
    为了方便新手统一下载本文所述资源，除了 Blender 软件本身，其它的插件、资产库等都可以前往 [Ghomist 的个人网盘](http://ghostmisser.ysepan.com/) 的 **【最新 Ballance 制图工具合集】** 目录进行下载。

## Blender

Blender 是一款自由和开源的三维计算机图形软件，它可以用于创建和渲染三维模型、动画、游戏、视觉效果等。它的功能十分强大，使用也颇为复杂，但好在用于 Ballance 制图时，我们只需要使用其很小一部分功能就足矣。

Blender 安装一般而言有三个途径：

- [从官网下载安装](https://www.blender.org/download/)
- 从 Steam 等第三方平台安装
- Linux 从包管理器安装

我们推荐大家从官网下载安装，目前的最新 **LTS 版本** 为 **4.2.x**。因为 Steam 下载的版本会自动更新（或者提示需要更新），更新后可能需要重新配置，且需要熟悉新特性，较为繁琐。

## BBP_NG

BBP_NG（全称 BallanceBlenderPlugin NextGeneration）是由 [yyc12345](https://github.com/yyc12345) 开发的一款 Blender 插件，专用于 Ballance 制图，并且也可提供通用的 Virtools 格式导入导出。插件开源地址：<https://github.com/yyc12345/BallanceBlenderHelper>

关于插件的安装与配置，请查看其[安装文档](https://yyc12345.github.io/BallanceBlenderHelper/zh-cn/install-plugin/)与[配置文档](https://yyc12345.github.io/BallanceBlenderHelper/zh-cn/configure-plugin/)。本文不作过多赘述。

## 制图资产库

资产库是一个后缀为 `blend` 的文件，其中包含了制图常用的固定物体及其资源，如：盘点路面、风扇底座、各种木板、灯柱装饰等。同时，该资产库也包含了对应的贴图信息以及归组信息，可以直接拖放使用，无需更多配置。

<!-- TODO: 添加资产库下载地址 -->

需要注意的是，该资产库并不像 max 制图流程中的“制图模板”，制图模板需要用 max 打开，并且在该模板的基础上进行制作。而资产库只需要添加至用户资产库当中，随后可以在任意新文件中使用其中的资产。

安装资产库的方法如下：

- 打开 Blender，找到 `编辑` - `偏好设置` - `文件路径` - `资产库`。
- 点击右侧的加号，添加一个资产库文件夹。该步骤会需要您选择一个文件夹或新建一个文件夹。建议将该文件夹命名为 `BallanceAssets`。
- 在路径下方将导入方法设置为 **追加（重用数据）**。关于 _导入方法_ 的更多介绍可以查看 [Blender 资产相关问题](../trouble-shooting/blender-assets.md)。
- 将下载好的资产库 blend 文件放入该文件夹中即可。

资产库的使用方法也很简单，只需打开一个“资产浏览器”视图，找到您刚刚创建的资产库，将其中的物体拖入3D视图即可。

我们推荐把 Blender 默认视图中底部的 **时间线** 视图更改为 **资产浏览器** 视图。因为在 Ballance 制图中不需要用到时间线，并且底部视图可以在需要时拖出来，不需要时收起来，类似于抽屉，方便取用素材。

## 其它常用插件推荐

- [Simple Lattice](https://github.com/BenjaminSauder/SimpleLattice)：快速晶格插件。在 Ballance 制图中主要用于制作坡面。
