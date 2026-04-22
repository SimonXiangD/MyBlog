---
title: 如何自定义你的无限制AI Chat Agent
date: 2026-04-18 22:16:08
tags: 技术分享
---

### 简介 
我们现在每天都会使用LLM，学习、生活、工作、娱乐。Gemini, Claude, ChatGPT本身都会有不错的表现。但是，有一些事情它们无法解决，或者太过人机。

### 为什么不直接使用chatgpt之类的原生app/网页

比如，对无限制内容的生成。和Gemini聊天，偶尔聊着聊着就会忽然跳出来说"I cannot fulfill this request"。虽然情况很少，但是其他模型比如Claude, Deepseek会有更多的这种道德或政治审查。虽然影响不大，但是莫名奇妙来一次还是挺烦的。

其次，系统内置prompt写的太死，自己的prompt影响甚微。比如我用Gemini优化ai绘画的prompt，大部分情况除非特殊说明，它都呆呆地调用nano banana和super intelligence帮我画图而不是帮我优化prompt，这让我很无语。

还有，它们不支持多个模式多种自定义prompt的chat agent。比如我想在chat 1里快速读书，需要助手有批判性思维和很高总结能力，但是我在chat 2里只是需要写一篇很短的文章，那么我写的系统prompt里的批判性思维就会在chat 2里用力过猛。或者我在chat 3里只是单纯吐槽一下，结果还要非常严肃地给我扯一大堆，很无趣。我没法一个chat写一个系统prompt，哪怕开头写了一堆，之后还可能会忘记，并且开新的chat就会要重新抄一次。

所以，在这片文章里，我将介绍如何自定义你的无限制AI chat agent。没有道德审查，没有写死的内置prompt，没有限制颇多无法轻易切换的自定义总体prompt。

### 为什么不用Skills等技术
如果说MCP是一个提升agent广度的协议，那么Skills就是提升agent深度的技术。它们的用处更多是给全自动agent流提供新的工具接入让agent能自动化做一些事，而我分享的是ai chat agent的体验优化，是对chat agent做提升，而不是做新的工具。我这个适合需要很多互动和用户输入的纯对话场景，比如改善绘画prompt。

### 需要什么

必须：
一台电脑，能访问世界互联网的网络。

可选：
llm api key（推荐deepseek，便宜好用，方便获取）

### 技术框架
使用到的技术很简单，酒馆。酒馆有点类似character.ai的开源版，但是它有很多的自定义功能，也有一些很好的社区提供很强的相关数据资料。核心思想就是，先把酒馆在本地部署了，然后搞一个好的破限预设。

它更多是用来玩文字角色扮演游戏的；但是我发现它也适合当一个无限制，可高度自定义的ai chat agent。


### 酒馆下载
参考[酒馆Github](https://github.com/SillyTavern/SillyTavern)。按照里面的下载指南走，本地部署就行。


### 预设获取

如果你没有破除道德审查的需求，可以忽略这一步。

加入[discord的类脑社区](https://discord.com/invite/odysseia)，可以读一遍里面的新手指南，然后在资源区找一个对应你使用的llm api的破限预设。

### 自定义agent

在酒馆里创建新角色并分配它的功能。比如，我创建了一个助手，它的功能就是帮我优化绘画prompt。

### 设置api key
在酒馆里设置你使用的api key。比如Deepseek，可以参考[视频](https://www.bilibili.com/video/BV1guNWeXERg)



### 总结
如果你有问题可以通过邮箱联系我。


