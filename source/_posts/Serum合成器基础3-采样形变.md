---
title: Serum合成器基础3-采样形变
date: 2024-03-30 15:18:06
tags: 电子音乐制作
---

# Serum合成器教程系列

本文标题的采样形变，指的是对波形进行直接变换。不同于减法合成，我们直接对波形进行变化。除了一些复制，翻转，缩变，我们还可以使用fm和am方法。

这部分的原理挺复杂的，特别是FM，我觉得可以去youtube找几个视频看一看，或者上reddit，比如有一些链接可以参考。（我自己之前看了几遍都没看懂…最近主业稍微可以闲一下，抱着好心情去认真看才看懂一些）如果暂时看不懂，很正常，以后心情好了再来看就行了。

[reddit回答帖](https://www.reddit.com/r/edmproduction/comments/5vdmc5/can_anyone_help_me_understand_fm_synthesis/)

[带声音示范的文章](https://synthesizeracademy.com/fm-synthesis/)

### Sync

1. sync no window 调整波形 看上去和频率调控很类似，区别在于 pitch 是直接改变波形音调，而 sync 是强制在频率里每次刷新重新播放波形，比如 2.5 的 110hz 的 A 就是每分钟刷新 110 次，每次里先两次波形再一次半波形
2. sync 1/2 window 对边缘做平滑 听起来更加 blurred 比如说没有一些呲呲的电子杂音
3. sync window 整个做平滑

### Bend 和 PWM

1. bend 扭曲波形，加是让函数（取绝对值后）向两边靠，减是向中间
2. bend 让低频高频都能听到，用来做 bass 好像很好
3. PWM 控制波形宽度 不过这玩意有啥用。。。

### Asym 和 Flip

1. asym 反对称 类似 bend，但是 bend 是中间向两边，asym 是一边向另一边 au5 说自己更喜欢 asym 相对于 bend
2. flip 上下翻转 flip 范围内的波形 到中间完全反转 到最右边返回初始

### Mirror 和 Quantize

1. mirror 中间做对称 处于中间时正好是原本波形对称 向左右时是拉伸对称部分
2. quantize 是降采样 有点类似马赛克滤镜，给人 pixel 的感觉 或者说 99 game boy 的感觉（另一个课程 instructor 的评价）

### FM AM RM

1. fm 频率调控
2. am 是调控波形的音量 负的就是减声
3. rm 如果正中间就是 am 如果拉满则是负数对应反转

### Remap

1. 自己画图来做 fm/am，实验时可以拿 saw（波形是直线的 basic shape）来做，更直观一些
2. 初始时，斜率为 1，代表没有任何变化
3. remap 1，2，3，4 实质上差不多，数字代表 sync 数
4. remap 的 x 轴对应波形表的 x 轴，导数对应区间内频段的宽度

