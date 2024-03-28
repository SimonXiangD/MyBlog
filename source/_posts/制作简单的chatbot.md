---
title: 制作简单的chatbot
date: 2024-2-15 22:18:33
tags: chatbot
---

# 制作简单的 Chatbot

# Chatbot 是什么

Chatbot，聊天机器人。有各种各样的聊天机器人，用于不同的场景，比如网站上的机器客服就是一个例子。我最近还看到一个新闻，一个公司裁了 700/3000 人工客服并使用 AI 克服替换，便是 Chatbot 的应用。

而我们也可以搭建各种各样的 Chatbot，比如搭建虚拟伴侣等。这篇文章中，我们便以搭建虚拟助手为例，搭建一个 chatbot 助手。

# Chatbot 的结构

Chatbot 的结构很简单，前端展示，后端服务，算法接口。

前端展示便是对话框，语音播放框之类的，可以使用 React 这样的框架实现；

后端服务便是前端调取的接口，负责业务逻辑，同时需要连接算法接口，可以使用 SpringBoot 或者 Python Flask 等实现；

算法接口，这个是最难的，但是我们先不考虑自己训练 AI 模型，我们采用简单一些的办法，那就是调用一些付费或者开源的大模型接口，并采用 prompt engineering 来生成指令。

本篇文章出于方便，就直接使用 python gradio 搭建 chatbot 了，它可以直接调用代码生成前端网页，gradio 库也有 chatbot 的组件，支持文字，语音等。我们的后端逻辑用 python 写也非常方便。

而算法接口，我们就使用 GPT3.5。当然 GPT4 之类的也行，不过这些区别不大，就是配置里改一行代码的事。

# 需要条件

一台可以连接全世界互联网的并且能写代码的电脑（用 VPN 也行）

openai 账号，有 1$ 以上的余额

python 和命令行基础

# 引入依赖

首先我们需要下载一些库。使用 pip 下载，或者 pycharm 里设置 interpreter 下载也行。

# Chabot 代码

懒得把我的成品代码再扒开重新从一开始写了，直接参考文档吧。。。与其看我一大堆话不如直接看文档代码来的方便

[https://www.gradio.app/guides/creating-a-custom-chatbot-with-blocks](https://www.gradio.app/guides/creating-a-custom-chatbot-with-blocks)

使用参考文档中的代码可以实现最基础的 chatbot，我直接贴上我的代码了。

``` python

import gradio as gr
import random
import time

from gptApi import simple_text_api_character 
# 下面一个模块，将调用接口部分的代码就是gptApi.py


from t2a import text2audio 
# 这个是自定义的语音接口，函数形式如下：
# def text2audio(text):
#     return "aaa.wav"
# 我是加了一层语音合成，但是你可以直接返回一个wav文件就行。


import os
import json
import datetime

now = datetime.datetime.now()
logName = "Day " + str(now)[:10]
logName += '.json'
# print(logName)

logPath = "./talkLog/" + logName
loaded = {}

WRITE_INTO_LOG = True
GENERATE_SOUND = True

def generate_from_text(message):
    text = message;
    return [
        (None, api_audio(message=text, useTextApi=False)),
        (None, format_respond_message(text)),
    ]

def get_audio(message):
    text = api_text(message=message)
    return [
        (None, api_audio(message=text, useTextApi=False)),
        (None, format_respond_message(text)),
    ]

def get_image(message):
    return [
        (None, api_image(message=message)),
        (None, format_respond_message(message)),
    ]

def get_text(message):
    return [
        (None, format_respond_message(api_text(message=message)))
    ]

def api_audio(message, useTextApi = True):
    text = message
    if useTextApi:
        text = api_text(message=text)
    audio_name = text2audio(text)
    return (audio_name,)

def api_image(message):
    return ("ri.png",)

def api_text(message):
    # time.sleep(5)
    # return "早上好！"
    print(message)
    return simple_text_api_character(message=message)

def format_respond_message(message):
    return f"回复：{message}"

def appendJson(newContent):
    if WRITE_INTO_LOG:
        if os.path.exists(path=logPath):
            with open(logPath, "r", encoding='utf-8') as f:
                loaded = json.load(f)
                loaded.append(newContent)
        else:
            loaded = [newContent]
        with open(logPath, 'w', encoding='utf-8') as f:
            json.dump(loaded, f, ensure_ascii=False,indent=4)

with gr.Blocks() as demo:
    chatbot = gr.Chatbot()
    msg = gr.Textbox()


    def request(chat_history, message):
        print(chat_history)
        chat_history = chat_history + [(message, None)]

        curTime = str(datetime.datetime.now())[:19]

        newContent = {"content": [[(message, None)]], "send_type": "request", "send_time": curTime}

        appendJson(newContent)

        return chat_history, message

    def respond(chat_history, message):

        interactOptions = [get_audio, get_image, get_text]
        interactOptions = [get_audio]
        interactOptions = [get_text]
        if GENERATE_SOUND:
            interactOptions = [get_audio]

        GENERATE_FROM_GIVEN_TXT = False

        if message[:5] == "test:" :
            GENERATE_FROM_GIVEN_TXT = True
            message = message[5:]
        # print(message)

        if GENERATE_FROM_GIVEN_TXT:
            interactOptions = [generate_from_text]

        resContent = random.choice(interactOptions)(message=message)

        curTime = str(datetime.datetime.now())[:19]
        newContent = {"content": [], "send_type": "response", "send_time": curTime}

        for pa in resContent:
            chat_history = chat_history + [pa]
            newContent["content"] += [pa]
            
        appendJson(newContent=newContent)
        
        return chat_history, ""

    msg.submit(request, [chatbot, msg], [chatbot, msg], show_progress='hidden').then(
        respond, inputs=[chatbot, msg], outputs=[chatbot, msg], show_progress='hidden'
    )

demo.launch(share=True)

```

注意，实际需要的代码比我的简单，我写这么多，除了 chatbot 外，还实现了额外的功能，比如日志系统，接口封装等等。但是我懒得重新写一遍简单版了，于是就直接复制过来了。。。

下一步写算法接口，实际上就是调用 openai 接口，查看 openai 官方文档和示例即可。

# 远程接口调用

python 发送请求可以用这个库，requests。

下面是我连接 gpt3.5 接口的代码

``` python

import requests
import os
import sys
sys.stdout.reconfigure(encoding='utf-8')

# 使用时记得开vpn,我的代理端口设置如下
http_proxy  = "http://127.0.0.1:33210"
https_proxy = "http://127.0.0.1:33210"

proxies = { 
              "http"  : http_proxy, 
              "https" : https_proxy, 
              "all_proxy": "socks5://127.0.0.1:33211",
            }

# 连通性测试
# response = requests.get('https://api.github.com',
#                          proxies=proxies, 
#                          verify=True,
#                          )


# 记得在系统环境变量里设置api key，具体查看openai的文档
headers = {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + os.getenv('OPENAI_API_KEY', ''),
}

# 实验prompt
# json_data = {
#     'model': 'gpt-3.5-turbo',
#     'messages': [
#         {
#             'role': 'system',
#             'content': "你需要扮演为一个可爱的猫娘，可以用可爱的语气和人对话"
#         },
#         {
#             'role': 'user',
#             'content': '你好！',
#         },
#     ],
#     'temperature': 0.7,
# }

def character_temp_character(message, character):
  json_template = {
    'model': 'gpt-3.5-turbo',
    'messages': [
        {
            'role': 'system',
            'content': f"你需要扮演为一位{character['role']}，会用{character['nature']}的语气和我对话"
        },
        {
            'role': 'system',
            'content': f"你的名字是助手A，简称为A，你是我的得力助手，帮我解决了很多问题"
        },
        {
            'role': 'system',
            'content': f"你和我聊天时，可以用'XXX'称呼我"
        },
        {
            'role': 'user',
            'content': f"{message}",
        },
    ],
    'temperature': 0.7,
  }
  return json_template

def simple_text_api_character(message, 
                              character = {
                                "nature": "温和",
                                "role": "商业助手",
                                }
                              ):
      
  json_data = character_temp_character(message=message,character=character)
  res = requests.post('https://api.openai.com/v1/chat/completions', 
                          headers=headers, 
                          json=json_data,
                          proxies=proxies,
                          verify=False
                          )

  # print(res)
  # print(res.json())
  # print(res.json()["choices"][0]["message"]["content"])
  return res.json()["choices"][0]["message"]["content"]


```

其中有几个注意点。

1. 如果是国内使用，会被 gfw 卡住。所以需要配置代理，具体的端口看你的 vpn 设置，比如 33210 是我的端口配置，你自己 vpn 什么端口你就要改成对应的
2. 如果调用失败，可以试试用 request 做简单的 get，访问一些网站，看看是 openai 接口掉错了，还是网络问题导致的调用失败。
3. 如果调用失败，还可以试试直接 bash（windows 用的 git bash）里 curl 一下 openai 的接口，如果没问题那就是代理没配好。
4. prompt 中是我们希望 chatbot 办理的角色

#_, 启动！

在命令行中输入

``` h
python launch.py
```

（如果报错了可能是路径问题，cd 一下；或者不是 python 而是 python3 之类的）

然后出现了这样一个界面，就可以正常交流了。

![](/img/U79VbOPSloo0gExs6kfcNx1unAd.png)

我改了下 prompt，并添加了语音合成功能。都不是很复杂！如果你对语音合成感兴趣，可以查一下 vits，然后自己训练模型就可以实时合成了。

视频演示在这里：[Demo](https://www.bilibili.com/video/BV1QG411e7nQ/?spm_id_from=333.999.0.0)
