# DAY0-DAY?
## 0 前言
本篇内容为`基础阶段 - Rust编程`的总结，分为`环境配置`及`语言学习`两个板块。
因为语言学习涉及内容较为零散，故将DAY0-DAY?汇聚成一篇。

## 1 环境配置
### 1.0 前言
环境配置部分主要流程就是根据教程内容一步步安装，同时需要注意以下几点：
* 学会分析报错内容
* 学会利用搜索引擎/gpt解决报错问题
### 1.1 wsl+ubuntu22.04+vscode
之前在完成pintos时配置过，故省略

### 1.2 配置rust环境
按照LearningOS仓库中readme指定的[教程](https://rcore-os.cn/arceos-tutorial-book/ch01-02.html)一步步操作即可
注意没有`curl`需要先通过如下命令安装（其他同理）：
```bash
sudo apt install curl
```

### 1.3 配置git+github ssh并clone代码
之前配置过，故省略

## 2 rust语法学习及rustlings
### 2.0 前言

一般新语言的入门，通常可以采用孟岩老师提倡的“快速掌握一个语言最常用的50%”方法，但注意到rust语言的特殊性以及接下来rCore的开发的复杂性，我们必须还要通过阅读系统而权威的大部头书籍来全面深入地学习。因此我们依次阅读了如下资料：
* [菜鸟教程](https://www.runoob.com/rust/rust-tutorial.html)
* [Rust语言圣经](https://course.rs/about-book.html)
* [《The Rust Programming Language, 2nd Edition》](https://www.amazon.com/Rust-Programming-Language-2nd-dp-1718503105/dp/1718503105/ref=dp_ob_title_bk)
并通过完成rustlings作业进行巩固练习