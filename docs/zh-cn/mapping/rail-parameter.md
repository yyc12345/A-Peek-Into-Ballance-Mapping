# 钢轨参数

Ballance 中的钢轨看起来是圆形，但实际上其截面是八边形，建模时切勿随意选择边数。

单轨截面的半径为`0.35`。双轨两根钢轨之间的间距是`3.75`（这似乎不是精确值，是大家都在用的所谓约定值）。单双轨结合处，单轨相对于双轨中心在Z轴上下降`0.61707`（由失衡之梦计算，取玩家球半径为2）。

普通侧轨倾斜角度`79.563°`，与此同时双轨之间的间距要改为`3.864`（由BallanceBug提供）。螺旋轨两层之间的间距为`5`（从Level 10测量）。侧边螺旋轨两层之的间距（实际上是每一次迭代的上升高度，因为侧边螺旋轨的轨道为两层共用的）为`3.6`（由Level 13结尾，Level 9开头测量）。