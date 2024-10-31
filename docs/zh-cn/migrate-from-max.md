# 从 3ds MAX 迁移

本文主要给熟练使用 3ds MAX（以下简称 max） 制图的制图者阅读，为了方便他们快速了解 max 与 blender 制图过程中的不同，并快速熟悉 blender 中的操作。

## 差异比较

虽然大体是相同的，都需要制图者创建地图模型，但 Blender 与 max 在部分操作和特性上略有不同，详见下表：

|操作|Max|Blender|
|-|-|-|
|归组|利用命名规则和 Virtools 脚本归组|直接在 Blender 中归组|
|构建赛道|预置在文件内的预置件|直接填写参数创建或使用资产库|
|自动UV|通过叠修改器支持|原生支持、插件支持|
|软件版本|受限于导出插件，仅支持古早版本|目前已支持至最新版（4.2 LTS）|

表中的差异项会在下文逐一阐述。

## Max 对齐工具

BallanceBlenderPlugin 提供了一套对齐工具，位于3D视图的 `Ballance` - `3ds Max Align`。该工具与 max 中的对齐工具相似。具体用法见BBP的[传统对齐文档](https://yyc12345.github.io/BallanceBlenderHelper/zh-cn/legacy-align/)。

除了传统对齐方式，我们强烈推荐使用 Blender 中的吸附功能。具体请查看[吸附功能详解](./blender/snapping.md)。

## 地图文件的迁移

如果您已经在 max 中制作了一张自制地图，或半成品地图，可以考虑以下两种迁移方式：

- 先借助插件将关卡导出至 nmo，并借助 max 制图模板中的归组模板赋予其归组信息，然后直接将 nmo 文件导入至 blender。此方法无需重新归组，后续也可直接导出 nmo。
- 直接将模型导出至现代化的3D模型格式，例如 fbx、glTF 等，然后导入 blender。此操作将丢失您的归组信息，目前需要您在 blender 中手动或利用自动归组功能重新归组。