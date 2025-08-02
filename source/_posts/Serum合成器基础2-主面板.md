---
title: Serum合成器基础2-主面板
date: 2024-03-30 15:12:42
tags: 电子音乐制作
---

# Serum合成器教程系列

在介绍完serum基础，和产生声音的源头振荡器后，本篇介绍serum主面板上其他的功能，比如sub，noise这两个独特的音源，以及env和lfo这类合成器中的“函数”，以及一些其他功能。

当然，本篇还是没有讲完主面板中的全部内容，比如warp和filter。它们会在之后出现。

### sub 振荡器

1. sub 技术上就是一个振荡器，不过有更少的可选参数
2. 可用于给 bass 铺底
3. DIRECT OUT：如果开启，就是不经过各种 filter fx 等直接输出，比如铺地可能就想要它单独铺出来

### noise 振荡器

1. 是一个采样器
2. 可以将 wav 拖入 audio track，使用 ctrl e 做切割处理，然后切割好后保存新的 wav，再拖入 noise 的 wav，然后频率可能得改下防止变声
3. 箭头：是否确定为 one-shot phase：起始点 random： phase 随机程度 pitch：音调 钢琴：是否跟着钢琴变调 如果钢琴被选中，那么 pitch 变化是 semitone；否则则是 percentage， 12% 是一个 octave

### Filter

1. cutoff 控制频率 res 控制频率处形状 pan 左右 drive 和 fat 都是加音量 但是 drive 是 pre-filter saturation，fat 没有做 saturation，不会改变频率的（感觉？） 反正现在不太懂这是什么 之后再说吧 mix 也不太懂，还没学过混音 之后再说吧

### Envelope 1

1. 它（和其他下半板块的模块）本身不产生声音，但是对声音产生影响
2. 是音量的结构
3. env1 负责整个 serum 的声音，由 adsr 控制
4. adsr 分别是什么？ a 是 attack，声音到最大的时长；d 是最高点下降到持续的时长；s 是下降并维持的音高；r 是释放后的停止时间 除此之外 serum 还有个 hold，代表最高处维持时间。其中 ahdr 都是横坐标的时长，s 是纵坐标的音高
5. 拉曲线时还可以改变曲线形状

### Envelope 2, 3

1. env2 和 3 不控制整体音量，需要将它们 assign 到具体的 knob 才有影响
2. 据 au5 说，他用 env1 基本只控制整体音量而不控制其他的
3. 拉到 knob 上时，可以调控影响的 range，shift alt 点击 knob 切换成对称控制， 如果是负的则是逆时针（从指针开始到最远处），如果是对称，方向则根据 shift alt 对称前的方向（正 or 负）决定走向
4. 一个 env 最多控制 32 个 knob，3 个 env 似乎是不太够的，于是之后还会有 lfo

### LFO

1. LFO 的最高点和最低点便是 lfo 的范围两端点，方向正负控制和上一节提到的控制方法一样

### LFO 控制器

1. rate 控制 lfo 周期时长
2. rise 渐进式的 lfo 启动 delay 时长结束再启动 lfo
3. smooth
4. bmp 跟着 daw 的 bpm 走还是跟着独立的数字频率
5. anchor 保证 rate 改变时 phase 也跟着改，为了确保 rate 变动时 lfo stay sync with beat 说实话这里没太懂
6. trip 在 rate 中添加更多的 subdivision 选择
7. dot 同上
8. off 每次新的开始地点都是上次的结尾
9. trig 总是从 lfo 最左边开始
10. env 让 lfo 不循环而只运行一次，像 envelope 一样
11. 最多可以有 8 个 lfo
12. 在曲线上双击增加点，可以拉曲线
13. 按住 shift 直接画横线
14. grid 控制横线单元格数量
15. 按住 alt shift，y 坐标也变成离散的
16. lfo 也可以读取和保存 preset
17. lfo rate 拉到最右 fast 速率是多少？ 据 au5 说可能是 512

### Macro 和 mod

1. 可以将 mod 的 knob 拉到别的上面，然后控制 mod 就是控制一大堆 knob
2. 目的是将一大堆参数整合成一个 package 来做 mod
3. 可以用键盘控制 mod

### Voicing

1. mono 只能弹一个键
2. poly 可以同时弹的数量（超过的话取最近弹的三个） unison 的也算，不过 unison 变大，poly 上限也会变大 unison 拉满时最多是 1088
3. porta 音不够时转变的速率 curve 转变曲线
4. always 如果开了，那么 mono 下哪怕两个不同的音分开，它们也会连续转变；scaled 如果开了那么跳 2 个 sacle 时间比跳一个 scale 更长
5. legato 如果开了那么各种 lfo，env，mod 都会继续而非重新被 trigger

### Pitch bend 和右键选项

1. pitch bend 翻译是弯音
2. 两个上下界调整范围，大小没有要求上大下小，上小下大也可以
3. ctrl 左键 一个 knob 可以让它初始化 或者右键选择 reset control 也行
4. 右键选择 mod source 可以避免 drag 因为有的可能是拖不到的比如 lfo 到另一个 lfo 的参数

### UI

1. 可以选择皮肤 不同皮肤带来的不同感觉可能真的会对创作有影响
2. 可以放大 放大后分辨率提高还挺细致的