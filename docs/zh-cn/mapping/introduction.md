# 自制地图概述

## 制图工具链

本文档仅推荐唯一的制图工具链/工作流：

- [Blender](https://www.blender.org/download/)
- [BallanceBlenderPlugin](https://github.com/yyc12345/BallanceBlenderHelper)

这套工作流的优势在于：不涉及自制图内嵌脚本时，可以完全摆脱对 Virtools 的依赖。可以说这套工作流就是目前最舒服的 Ballance 制图流程。

地图（也叫关卡）在文件系统中通常被保存为一个 nmo 文件。该文件类型原本只能借助专用工具 Virtools 打开及编辑，但 Virtools 过于古老，难以使用，且对模型不提供编辑能力，需要借助 Blender / 3dsMAX 这样的工具建模后导入 Virtools 中，过程中又涉及到各类导入导出插件（max 导出 nmo 的插件仅支持非常古老的 max 版本），非常繁琐且兼容性较差。

BallanceBlenderPlugin 则很好地解决了上述问题，提供了直接对 nmo 文件的读写能力，使 Blender 能够直接导入、导出 nmo 文件，摆脱了 Virtools 的限制，也摆脱了老旧 3dsMAX 的限制，能够使用更现代化的 Blender 进行制图，大大提高了制图效率。

具体安装与配置请查看[工具安装与配置](./installations.md)。

## 关卡内容总览

一张 Ballance 地图中通常包括以下物体：

- 道路与轨道
- [机关与道具](#机关如何生效)
- 检查点与重生点
- 终点飞船
- 其它自定义装饰物

道路与轨道在 Ballance 中文社区的术语称为路面与钢轨。该部分需要制图者通过建模软件手动构建，特殊情况下还需要手动为物体上材质、调整UV。目前暂不存在所谓“简单拖动、画线就能生成复杂道路、轨道”的方法，但借助 Blender 及 BallanceBlenderPlugin 我们能够达到类似的操作。

而机关、检查点等，它们中的大多数在 Blender 中都只需要简单摆放至正确位置并正确[归组](#何为归组)即可，Ballance 会根据归组信息自动将其替换为真实的游戏内机关。

自定义装饰物可以是携带任意贴图的任意模型。默认情况下它不会与物理世界发生交互，可以通过归入路面组让其具有路面的物理特性。关于外置贴图的保存可以查看[贴图文件的保存格式](./texture-option.md)。

## 关卡基本要素

在 Blender 中，一个基本的 Ballance 关卡至少需要包括：

- 一个开头的四火焰盘点（注意是火焰，不是底部路面，路面不是必须的）。
- 一个重生点（第一小节的）。
- 一个飞船。

如果不包含以上物体，即使导出了关卡，Ballance 也会拒接加载。

此外，对于只有一小节的地图，Ballance 在渲染开头的四盘点火焰的时候会出现 Bug，表现为火焰粒子呈现为不自然的三角形。这就是所谓的“一小节关卡 Bug”。为了避免这种情况，请添加第一小节的检查点（两火焰盘点）和第二小节的重生点，让关卡小节数变为2。我们不建议制作只有一小节的关卡，尽管它玩起来没有任何问题。

## 何为归组

组是 Ballance 关卡中的重要概念。地图中的任何模型，只有归入相应的组中，才会具有相应的功能。

例如，一个可行走的路面应当归入以下组中：

- `Phys_Floors`：使路面物理化，否则无法与玩家球发生碰撞。
- `Sound_HitID_01`：玩家与该组物体碰撞时会发出水泥地面的碰撞音效。
- `Sound_RollID_01`：玩家球在该组物体滚动时会发出水泥地面的滚动音效。
- `Shadow`：玩家球在该组物体上方一定距离内时会投射出影子。

具体的归组信息与规则可以在 Ballance Wiki 的[归组页面](https://ballance.jxpxxzj.cn/wiki/%E5%BD%92%E7%BB%84)查询到，本文档不予赘述。

在 Blender 当中，由插件生成的物体、制图资产库中的物体，均已经归好组，除非特殊需求，一般无需做过多调整。具体操作请查看[归组](./grouping.md)章节。

## 机关如何生效

机关与普通物体的归组略有不同。Ballance 地图中所有的机关都没有贴图，这表示它们只是一个占位符，它们将会在游戏运行时根据组别被游戏自动替换成有功能、真正的机关。你完全可以用一个道具球的占位符，然后把它归入风扇组，那么在游戏中，这些道具球模型就会被替换成风扇，而不是道具球。

这意味着这些占位符的 Mesh 不重要。甚至于你可以直接使用一个空白 Mesh，它也会被游戏正常替换，只要归组正确，但这样对于制图来说不够直观和方便，占位符就是为了方便观察这个机关的作用范围才存在的。

那么 Ballance 是如何知道机关应该被替换在哪里呢，答案就是这些机关的原点。准确地说是在运行时先存储这些机关占位符的位移，旋转，缩放，然后把这些占位符删除，然后将真正的机关导入进来，再把之前存储的位移，旋转，缩放信息赋予给它。因此，机关的原点很重要。

基于上述原因，**机关的原点和机关的形状之间的位置关系不能被改变**，也就是机关的原点绝对不可以改变。也就意味着你绝对不可以对机关的占位符使用 Blender 右键菜单中的设置原点中的任意一项。如果擅自移动机关的原点，所导致的后果包括但不限于机关错位等。

## 死亡区

死亡区是 Ballance 游戏中的一种特殊物体，当玩家球碰到它的时候就会死亡，回到重生点。

死亡区的判定是按照其 Bounding Box（碰撞盒）来判断的，只要进入其碰撞盒，就判断和死亡区接触。死亡区并不是指物体触碰到死亡区的面才产生效果的，不要有这样的误解。也因此不要把死亡区本身塑造成歪七扭八的，并指望它能工作。相反，应该用多个死亡区来达成相同效果。这也就是我们为什么通常使用 Cube（立方体）来作为死亡区的模型，因为 Cube 的碰撞盒就是其本身形状，简单直观，且死亡区不会在游戏里显示，因此没有贴图也没关系。

死亡区是可以有缩放的，这与那些需要物理化的物体不同。但旋转死亡区可能带来意料之外的效果（旋转后的死亡区的碰撞盒不再是死亡区形状本身了，不方便观察），不要那么做。

死亡区需要隐藏，不然会在游戏里显示，很难看。在 Blender 里隐藏就是在 Virtools，以及地图中隐藏了，二者隐藏属性是相通的。

## 开始制作

了解到上述关于 Ballance 关卡的基本知识后，您就可以开始着手制作自己的自制地图了。
