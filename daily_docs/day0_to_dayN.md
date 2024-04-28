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

注意：配置ssh后，git push到github时若仍然提示输入密码，可修改.git/config文件中的url，从HTTPS https://github.com/achintski/opencamp-24sp-daily.git 更新为SSH git@github.com:achintski/opencamp-24sp-daily.git

## 2 rust语法学习及rustlings
### 2.0 前言

* 初学一门新语言，通常可以采用孟岩老师提倡的“快速掌握一个语言最常用的50%”方法，快速入门
* 但注意到rust语言的特殊性以及接下来rCore的开发的复杂性，我们必须还要通过阅读系统而权威的大部头书籍来全面深入地学习
* 同时，一些特别细节的点在入门资料和书籍中未必涉及，需要我们查阅[官方文档](https://doc.rust-lang.org/stable/std/all.html)

因此我穿插查阅/参考了如下资料：
* 快速入门：
    * [菜鸟教程](https://www.runoob.com/rust/rust-tutorial.html)
    * [《Rust语言圣经》](https://course.rs/about-book.html)(最推荐，整合了很多其他的经典资料)
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
    * 高级语言 `Python/Java` 等往往会弱化堆栈的概念，但是要用好 `C/C++/Rust`，就必须对堆栈有深入的了解，原因是两者的内存管理方式不同：前者有 `GC` 垃圾回收机制，因此无需你去关心内存的细节。
    * 在所有权模型下：堆内存的生命周期，和创建它的栈内存的生命周期保持一致
    * `copy` / `move`
    * `borrow`（借用）
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
    * `into()`
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
        * rust中**对象定义和方法定义是分开的**
        * 一个/多个`impl`模块
        * `self`、`&self`和`&mut self`及所有权
            * `self`表示`实现方法的结构体类型的实例`的所有权转移到该方法中，这种形式用的较少
            * `&self`表示该方法对`实现方法的结构体类型的实例`的不可变借用
            * `&mut self`表示可变借用
    * 闭包
        * 可以看做匿名函数
        * ||中间放参数
    * map_err()
        * 用来处理Err类型的变量
        * 参数是函数/闭包
    * `PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)`仅可以用来处理x<=0的情况，而x非数字的情况无法处理
        * `?`操作符：`Err` / `None` 类型直接立即结束，提前返回；否则从`Ok` / `Some` 中取出返回值作为`?`操作符的结果
        * 或者用match平替
* generics1
    * `&str` vs `String`
    * 也可以用`_`来让编译器自动推断
* generics2
    * 泛型可以类比多态
    * 结构体中的泛型 & 方法中使用泛型
    * 例如（from Rust Course）：
        ```rust
        struct Point<T> {
            x: T,
            y: T,
        }

        impl<T> Point<T> {
            fn x(&self) -> &T {
                &self.x
            }
        }

        fn main() {
            let p = Point { x: 5, y: 10 };
            println!("p.x = {}", p.x());
        }
        ```
        * 使用泛型参数前，依然需要提前声明：`impl<T>`
        * 上述代码中，`Point<T>`不再是泛型声明，而是一个完整的结构体类型，因为我们定义的结构体就是 `Point<T>`而不再是`Point`
        * 除了结构体中的泛型参数，我们还能在该结构体的方法中定义额外的泛型参数，就跟泛型函数一样
        * 对于`Point<T>`类型，你不仅能定义基于`T`的方法，还能针对特定的具体类型，进行方法定义
* *trait(特征)*
    * `impl Trait for Type`：为Type类型实现Trait特征
    * 特征定义与实现的位置(孤儿规则)
    * 方法的默认实现 vs 重载
    * `impl Trait`
        * 作为函数参数
            * `impl Trait`此时为语法糖,可用`特征约束`写出完整版
            * `多重约束`：`impl T1 + T2`
        * 作为函数返回值（只能返回某一种类型）
* quiz3
    * restricting type parameter `T`：`impl<T: std::fmt::Display> ReportCard<T> {...}`（根据编译器help提示）
* lifetims1
    * 标记的生命周期只是为了取悦编译器，告诉编译器多个引用之间的关系，当不满足此约束条件时，就拒绝编译通过；并不会改变任何引用的实际作用域
    * 和泛型一样，使用生命周期参数，需要先声明 `<'a>`
    * 本题中：把具体的引用传给`longest`时，那生命周期`'a`的大小就是`x`和`y`的作用域的重合部分，换句话说，`'a`的大小将等于`x`和`y`中较小的那个
    * 编译器提示：
    ```bash
        help: consider introducing a named lifetime parameter
        |
    13  | fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
        |           ++++     ++          ++          ++
    ```
* lifetimes2
    * 在`longest`函数中，`string2`的生命周期也是`'a`，由此说明`string2`也必须活到 println! 处，可是`string2`在代码中实际上只能活到内部语句块的花括号处`}`，小于它应该具备的生命周期`'a`，因此编译出错（编译器没法知道返回值没有用到`string2`）
    * hint：
    Remember that the generic lifetime 'a will get the concrete lifetime that is equal to the smaller of the lifetimes of x and y. 
    You can take at least two paths to achieve the desired result while keeping the inner block:
        1. Move the string2 declaration to make it live as long as string1 (how is result declared?)
        2. Move println! into the inner block
* lifetimes3
    * 结构体中生命周期标注：
        * 对结构体本身类似泛型：`<'a>`
        * 对结构体成员：`&'a`
    * 结构体成员引用的生命周期要大于等于结构体
* lifetime others
    * 输入生命周期 & 输出生命周期
    * 生命周期的消除
    * 方法中的生命周期（类似泛型参数语法）
        * `impl`中必须使用结构体的完整名称，包括`<'a>`，因为生命周期标注也是结构体类型的一部分！
        * 方法签名中，往往不需要标注生命周期，得益于生命周期消除的第一和第三规则
    * 静态生命周期
* tests4
    * `#[should_panic]`：The test passes if the code inside the function panics; the test fails if the code inside the function doesn’t panic.
<!-- * tests5（自动进行时这个被跳过了，直接到了迭代器）
    * unsafe函数：
        * 使用`unsafe fn`来进行定义
        * 这种定义方式是为了告诉调用者：当调用此函数时，你需要注意它的相关需求，因为Rust无法担保调用者在使用该函数时能满足它所需的一切需求
        * 因此在使用`unsafe`声明的函数时，一定要看看相关的文档，确定自己没有遗漏什么 -->
* iterators1
    * Rust的迭代器是指实现了`Iterator trait`的类型
    * 最主要的一个方法：`next()`
        * 对迭代器的遍历是消耗性的
        * 返回的是`Option<Item>`类型，当有值时返回`Some(Item)`，无值时返回`None`
        * 手动迭代必须将迭代器声明为`mut`可变，因为调用`next`会改变迭代器其中的状态数据（当前遍历的位置等），而`for`循环去迭代则无需标注`mut`，因为它会帮我们自动完成
* iterators2
    * `iter()`
        * `Iterator adapters`（*迭代器适配器*）
            * Adapters operate on an iterator and return a new iterator
            * 是*惰性接口*：iterators are lazy and do nothing unless consumed
            * 常见的有：`map()`、`filter()`、`take()`、`zip()`、`rev()`
            * 需要一个*消费器*来收尾，例如：`collect()`、`sum()`、`any()`
        * 注：如果集合里的类型是非`Copy`类型，消费者在取得每个值后，在迭代器被清除后，集合里的元素也会被清除。集合会只剩“空壳”，当然剩下的“空壳”也会被清除
        * 迭代器是*可组合的*
    * 一个例子：
        ```rust
        let v1: Vec<i32> = vec![1, 2, 3];
        v1.iter().map(|x| x + 1);
        ```
        map 函数的闭包并没有获得迭代器的所有权。具体解释如下：
        * `v1.iter()`创建了一个针对`v1`中元素的迭代器。这个迭代器是对`v1`的不可变引用，也就是说，它拥有对`v1`中元素的借用权，但并不拥有所有权。
        * `map(|x| x + 1)`是对上述迭代器应用的一个闭包。闭包内部的`|x| x + 1`表示对迭代器产生的每个元素`x`加上 1。在这个过程中，闭包接收的是`x`的不可变引用，同样没有获取`x`或迭代器的所有权。

        综上所述，闭包并未获得迭代器的所有权。它只是在`map`函数执行期间，对迭代器提供的每个元素借用并进行计算。一旦`map`函数结束，闭包对元素的借用也随之结束，不会影响到`v1`或其迭代器的所有权状态。
        ...
        如果您想让闭包返回的新值形成一个新的集合（如 Vec<i32>），您需要调用 collect() 方法来完成这一过程：
        ```rust
        let incremented_values: Vec<i32> = v1.iter().map(|x| x + 1).collect();
        ```
        在这里，`collect()`方法会消费`map`返回的迭代器，并将其内容收集到一个新的`Vec<i32>`中。然而，即使如此，闭包本身仍然没有获得迭代器的所有权，而是`collect()`函数在处理过程中获取了所有权并完成了数据的转移。
* iterators3
    * 从容器创造出迭代器一般有三种方法：
        * `iter()` takes elements by reference.
        * `iter_mut()` takes mutable reference to elements.
        * `into_iter()` takes ownership of the values and consumes the actual type once iterated completely. The original collection can no longer be accessed.
    * `collect()`会根据函数返回值自动调整格式
* iterators4
    * 这不让用那不让用，那自然是得用自带的工具咯
    * (1..=num).product()
* iterators5
    * 一点思考：
        ```rust
        fn count_for(map: &HashMap<String, Progress>, value: Progress) -> usize {
            let mut count = 0;
            for val in map.values() {
                // 此处为什么不是*val == value呢？
                // 下面这中方式中，实际上是在比较两者对应的实体是否相同
                if val == &value {
                    count += 1;
                }
            }
            count
        }
        ```
    * *扁平化（Flatten）*
        ```rust
        fn count_collection_iterator(collection: &[HashMap<String, Progress>], value: Progress) -> usize {
            collection.iter() // Iterate over the slice of hashmaps
                .flat_map(|map| map.values()) // Flatten the values of each hashmap into a single iterator
                .filter(|val| **val == value) // Filter values equal to the target value
                .count() // Count the filtered values
        }
        ```
    * 在上述实现中：
        * 首先使用 `collection.iter()` 创建一个迭代器，它遍历 `collection` 中的每一个 `HashMap` 引用。
        * 然后对每个 `HashMap` 应用 `flat_map(|map| map.values())`，将每个 `HashMap` 的值迭代器扁平化为单个包含所有 `HashMap` 值的迭代器。
        接着使用 `filter(|val| *val == value)`，筛选出与目标 `value` 相同的 `Progress` 枚举值。
        * 最后，通过 `count()` 方法计算筛选后的元素数量，即符合条件的 `Progress` 枚举值的总数，返回这个计数值作为函数结果。
* smart_pointers（*智能指针*）
    * 前言
        * 相比其它语言，Rust 堆上对象还有一个特殊之处---它们都拥有一个所有者，因此受所有权规则的限制：当赋值时，发生的是所有权的转移（只需浅拷贝栈上的引用或智能指针即可）
        * 例如以下代码：
            ```rust
            fn main() {
                let b = foo("world");
                println!("{}", b);
            }

            fn foo(x: &str) -> String {
                let a = "Hello, ".to_string() + x;
                a
            }
            ```
        * 在 `foo` 函数中，`a` 是 `String` 类型，它其实是一个智能指针结构体，该智能指针存储在函数栈中，指向堆上的字符串数据。当被从 `foo` 函数转移给 `main` 中的 `b` 变量时，栈上的智能指针被复制一份赋予给 `b`，而底层数据无需发生改变，这样就完成了所有权从 `foo` 函数内部到 `b` 的转移。
    * 在 `Rust` 中，凡是需要做资源回收的数据结构，且实现了 `Deref`/`DerefMut`/`Drop`，都是`智能指针`
* arc1
    * 使用 `let shared_numbers = Arc::new(numbers);` ：将 `numbers` 向量封装在一个 `Arc<Vec<u32>>` 中。
    * `Arc` 允许多个线程同时拥有对同一数据的访问权，且其内部的引用计数机制确保数据在所有持有者都不再需要时会被正确释放。这样，`numbers` 可以在多个线程间共享而无需复制整个向量，既节省了内存，又保证了线程安全性
    * 使用 `let child_numbers = Arc::clone(&shared_numbers);` ：创建 `shared_numbers` 的克隆（实际上是增加其引用计数）。每个线程都获得一个指向相同底层数据的独立 `Arc` 
    * `thread::spawn`创建一个线程
    * `move`关键字：指示闭包在捕获外部变量时采取“所有权转移”策略，而非默认的借用策略
    * `join()` 方法会阻塞当前线程，直到指定的线程完成其任务。`unwrap()` 处理 `join()` 返回的 `Result`，在没有错误时提取出结果（这里没有错误处理，因为假设所有线程都能成功完成）。这样，`main()` 函数会等待所有子线程计算完毕后再继续执行
* cow1
* threads1
    * 如果你想创建新线程，可以使用`thread::spawn`函数并传递一个闭包，在闭包中包含要在新线程 执行的代码。
    * 默认情况下，当主线程执行结束，所有子线程也会立即结束，且不管子线程中的代码是否执行完毕。极端情况下，如果主线程在创建子线程后就立即结束，子线程可能根本没机会开始执行。
    * 为避免上述情况的发生，我们可以通过阻塞主线程来等待子线程执行完毕。这里所说的阻塞线程，是指阻止该线程工作或退出。
    * `Rust`标准库提供的`thread::JoinHandle`结构体的`join`方法，可用于把子线程加入主线程等待队列，这样主线程会等待子线程执行完毕后退出。
    * `unwrap()`
* threads2
    * Mutex确保在某一时刻只有一个thread可以更新jobs_completed
    * thread闭包中，使用lock()上锁
    * 注意：
        ```rust
        println!("jobs completed {}", status.lock().unwrap().jobs_completed);
        ```
        如果放到循环内，就是输出10次`jobs completed x`，`x`的值有时候全是10，有时候有一部分是10；放到循环外就是一次`jobs completed 10`
* threads3
    * 报错内容：
        ```bash
           |
        29 | fn send_tx(q: Queue, tx: mpsc::Sender<u32>) -> () {
           |                      -- move occurs because `tx` has type `Sender<u32>`, which does not implement the `Copy` trait
        ...
        34 |     thread::spawn(move || {
           |                   ------- value moved into closure here
        ...
        37 |             tx.send(*val).unwrap();
           |             -- variable moved due to use in closure
        ...
        42 |     thread::spawn(move || {
           |                   ^^^^^^^ value used here after move
        ...
        45 |             tx.send(*val).unwrap();
           |             -- use occurs due to use in closure
        error: aborting due to 1 previous error
        ```
    * 分析：`tx`变量`move`到第一个闭包后，已经无法在该闭包外获取了，而在第二次进程创建仍然尝试`move`。通过为每个变量创建`tx`的`clone`，我们确保了每个闭包都拥有其独立的`sender`，从而避免了`use after move`错误
* macros4
    * 每个macro规则后面加;
* clippy1
    * 根据编译器提示修改
    * const PI: f32 = std::f32::consts::PI;
* clippy3
    * 已经通过 `is_none()` 检查确保了 `my_option` 是 `None`，因此接下来不应该再尝试调用 `unwrap()`
    * `Vec::resize` 方法用于改变已有向量的长度，如果新的长度大于当前长度，则填充指定的默认值。
        * 但是，你的用法存在一些问题。首先，你试图创建一个空向量（通过将大小更改为0），但直接使用 `resize(0, 5)` 并不是正确做法，因为这会让人们以为你要填充默认值5到一个空向量中，而实际上你是从一个非空向量开始的。
        * 如果你想从 `vec![1, 2, 3, 4, 5]` 起始，然后得到一个空向量，你应该直接使用 `clear` 方法，而不是 `resize`。