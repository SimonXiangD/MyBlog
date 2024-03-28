---
title: 本地vs code c++环境配置
date: 2024-03-28 22:36:31
tags: c++
---

# Windows系统 本地 VS Code 配置 C++ 环境

# 本地配置的目的

看到这个博客肯定就有人要问了：德同学你何苦要本地vs code配置c++环境呢？如果是大项目，好好的visual studio不用来用vs code，如果就是写点简单算法题，力扣网站直接刷不好吗，非要自讨麻烦。

实际上我以前就是这么想的，但是今天发现本地配置还是有意义的————因为要面试，然后发现可能要在本地跑代码，而visual studio每次打开都要不少时间，挺麻烦的，相比之下vs code好很多。而面试的时候可能并不会同意让你打开力扣当c++环境。

配置过程也不长，十五分钟的事。所以不妨配置一个，写起代码手感不得不说远超干巴巴的leetcode网页版。但之前就故意为了练这个没配...

# 配置过程

## 下载MINGW

首先下载 MINGW， 看[这个帖子](https://stackoverflow.com/questions/46455927/mingw-w64-installer-the-file-has-been-downloaded-incorrectly)里有图片的赞数最多的那个回答就够了。

实际上就是下载压缩包（[地址](https://github.com/brechtsanders/winlibs_mingw/releases/download/11.2.0-10.0.0-ucrt-r1/winlibs-x86_64-posix-seh-gcc-11.2.0-mingw-w64ucrt-10.0.0-r1.7z)），解压后放到一个目录里，然后系统变量加一下。

搞完以后，cmd试试

``` h

gcc --version

```

输出没问题就是安装好了。

## 配置VS Code

其实配置VS code的部分有一篇文章我觉得很好，那就是[这篇](https://zhuanlan.zhihu.com/p/87864677)。它虽然讲安装的部分有些过时，但配置vs code的部分没有，直接参考它就行了。

概括而言，就是安装c++插件，配置编译器环境。

## 引入头文件

正常来说我们已经可以跑c++程序了，比如最简单的Hello World：

``` h
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello World" << endl;
    return 0;
}

```

但是，当我们敲出vector, unordered_map, priority_queue等常用数据结构的时候发现底下都是红线，因为没有引入对应的依赖。于是我们稍作改动：

``` h

#include <bits/stdc++.h>
using namespace std;

int main()
{
    cout << "Hello World" << endl;
    return 0;
}


```

现在我们就看可以自由使用各种数据结构了，面试时也可以直接打开vs code写c++。