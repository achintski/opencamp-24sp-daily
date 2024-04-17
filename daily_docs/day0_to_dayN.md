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

* 初学一门新语言，通常可以采用孟岩老师提倡的“快速掌握一个语言最常用的50%”方法，快速入门
* 但注意到rust语言的特殊性以及接下来rCore的开发的复杂性，我们必须还要通过阅读系统而权威的大部头书籍来全面深入地学习
* 同时，一些特别细节的点在入门资料和书籍中未必涉及，需要我们查阅[官方文档](https://doc.rust-lang.org/stable/std/all.html)

因此我穿插查阅/参考了如下资料：
* 快速入门：
    * [菜鸟教程](https://www.runoob.com/rust/rust-tutorial.html)
    * [《Rust语言圣经》](https://course.rs/about-book.html)
* 官方文档：
    * [The Rust Standard Library](https://doc.rust-lang.org/stable/std/index.html)
    * [《The Rust Reference》](https://doc.rust-lang.org/stable/reference/)
    * [《Rust By Example》](https://doc.rust-lang.org/rust-by-example/index.html)
* Slides:
    * [thu 程序设计训练（Rust）](https://lab.cs.tsinghua.edu.cn/rust/)
    * [2024春夏季训练营课程资料](https://opencamp.cn/os2edu/camp/2024spring/stage/1)
* Books：
    * [《The Rust Programming Language, 2nd Edition》](https://www.amazon.com/Rust-Programming-Language-2nd-dp-1718503105/dp/1718503105/ref=dp_ob_title_bk)

并通过穿插完成`rustlings`作业进行巩固练习

### 2.1 rust语法
#### 2.1.0 前言
注意：第一次学一个概念时一定要打好基础，不要为了追求进度而忽略质量
#### 2.1.1 常见内容
* HelloWorld
* 类型
    *原生类型
        * 布尔 bool：两个值 true/false。
        * 字符 char：用单引号，例如 'R'、'计'，是 Unicode 的。
        * 数值：分为整数和浮点数，有不同的大小和符号属性。
            * i8、i16、i32、i64、i128、isize
            * u8、u16、u32、u64、u128、usize
            * f32、f64
            * 其中 isize 和 usize 是指针大小的整数，因此它们的大小与机器架构相关。
            * 字面值 (literals) 写为 10i8、10u16、10.0f32、10usize 等。
            * 字面值如果不指定类型，则默认整数为 i32，浮点数为 f64。
        * 数组 (arrays)、切片 (slices)、str 字符串 (strings)、元组 (tuples)
        * 指针 & 引用
        * 函数
        * 闭包
    * 组合类型
        * 结构体（逻辑与）
        * 标签联合（逻辑或）
* 条件
* 循环
* 结构化数据
* IO
#### 2.1.2 特殊内容
Q：任何行为背后都有动机，Rust特性这样设计的动机是什么呢？

* 变量绑定--`let`
* 不可变变量 vs 常量
* 语句 vs 表达式
* 所有权 & 生命周期
    * 在所有权模型下：堆内存的生命周期，和创建它的栈内存的生命周期保持一致
    * copy/move
    * borrow（借用）
        * 借用`&`与可变借用`&mut`
        * 借用规则
    * 函数的参数和返回值与变量绑定的规则相同


### 2.2 rustlings
大致步骤：终端输入命令`rustlings watch`、修改代码、删掉注释并自动跳转下一题
注意：后两个资料中概念介绍顺序和习题涉及概念顺序一致
技巧：学会分析编译器提示，有的题目是语法错误，有的是考虑不周导致测试过不去
* vec2
* enums3
* strings3&strings4
    * into
* hashmaps2
    * `HashMap`的`get()`方法只能返回值的引用
    * 解引用操作`*`也需要转移所有权
* quiz2
    * match中模式绑定的值，如：`Command::Append(n) => {}` 中的n是&usize类型，可以使用`for i in 0..*n`完成遍历
    * 对于`不可变引用的string`，要想修改需要先将其`clone`给一个可变变量
* options1
    * 可用`match`，也可以用`if`
* options2
    * 注意`Options枚举`的本质目的：解决`Rust`中变量是否有值的问题，因此第二个任务中需要两层嵌套的`Some`
    * `if let` / `while let`本质上是`match`
    * `match`中匹配后的绑定
* options3
    * 在 `Some(p) => println!("Co-ordinates are {},{} ", p.x, p.y)` 处，value partially moved here；而在最后返回值`y`处，value used here after partial move
    * 因此需要：borrow this binding in the pattern to avoid moving the value
    * 区分`ref`和`&`
* errors2
    * 对于返回结果是`Result`的函数，一定要显式进行处理
    * `?`操作符（本质是宏，同时可以链式调用）
        * 作用：提前传播错误
        * 场合：返回值是 Result 或者 Option 函数中
        * 对于 Result 类型，
            * 如果是 Err 则提前返回，当前函数立即返回该错误。
            * 否则，从 Ok 中取出返回值作为 ? 操作符的结果。
        * 对于 Option 类型，
            * 如果是 None 则提前返回，当前函数立即返回 None。
            * 否则，从 Some 中取出返回值作为 ? 操作符的结果。
    * 本题既可以使用`?`操作符，也可以使用`match`
* errors3
    * `?`操作符只能在返回值为`Result` / `Option` 的函数中使用
    * 需要修改三处：
        * `use std::error::Error;`
        * 给`main`函数增加返回值 ` -> Result<(), Box<dyn Error>>`
        * 末尾返回 `Ok(())`
    * 也可以用`match` / `if else`
* errors4
    * 法一：利用`match guard`
    * 法二：`if` & `else`
* errors6
    * impl
        * rust中对象定义和方法定义是分开的
        * 一个/多个`impl`模块
    * 闭包
    * map_err()
        * 用来处理Err类型的变量
        * 参数是函数/闭包
    * `PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)`仅可以用来处理x<=0的情况，而x非数字的情况无法处理
        * `?`操作符：`Err` / `None` 类型直接立即结束，提前返回；否则从`Ok` / `Some` 中取出返回值作为`?`操作符的结果
        * 或者用match平替