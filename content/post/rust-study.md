---
title: Rust Study
abbrlink: rust-study
date: 2021-11-25 20:51:36
tags: [Rust]
categories: Code
---

[Rust](https://www.rust-lang.org) 学习记录

<!--more-->

# Rust 介绍

# Rust 环境搭建

## 安装 Rust 编译工具

https://www.rust-lang.org/zh-CN/tools/install
打开以上链接下载 [rustup-init.exe（64位）](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe) ，如果你是 32 位的，则下载32位的。

如果不想安装在 C 盘，那么在安装之前，按照以下步骤设置：

新建系统变量![image.png](https://i.loli.net/2021/11/25/pYQsl4zNEgm7Tva.png)

变量名 `CARGO_HOME`，变量值设置为你自己想要安装的目录![image.png](https://i.loli.net/2021/11/25/ZIStCB7TPv5jkza.png)

变量名 `RUSTUP_HOME`，变量值设置为你自己想要安装的目录![image.png](https://i.loli.net/2021/11/25/osAnMwEkzS6eLxN.png)

右键以管理员运行刚刚下载的 Rust 安装程序![image.png](https://i.loli.net/2021/11/25/xd5NJfiXzOK63L1.png)

可看到设置的目录生效，现在直接回车进行安装即可，若是速度很慢就[换源](https://zhuanlan.zhihu.com/p/126204128)，或者开代理![image.png](https://i.loli.net/2021/11/25/zTbYAiJvCGRrtEh.png)

安装完成后，cmd 中输入 `rustc -V` 和 `cargo -V` 验证安装![image.png](https://i.loli.net/2021/11/25/FjSoWPl1dQNxLpO.png)

如果以上两个命令能够输出安装的版本号，就是安装成功了。 

## 搭建 Visual Studio Code 开发环境

VSCode 中安装 Rust 插件![image.png](https://i.loli.net/2021/11/25/lp1sBeEuPSTCLjo.png)

Rust 的开发环境就搭建好了 

# 第一个 Hello, world 程序

按照以下命令执行

```bash
mkdir first_rust_program # 新建一个文件夹
cd f* # 进入
touch main.rs # 新建 main.rs 文件
code . # 在 VSCode 中打开
```

编写代码

![image.png](https://i.loli.net/2021/11/25/xQNVDfBgKIbvsmM.png)

关键字 `fn` 定义函数；Rust 也和 C 语言类似，都是以 main 函数作为程序入口。
`println!` 是一个 Rust macro（宏），如果是函数的话，就没有 `!`

## 编译

运行 Rust 程序前得先编译，编译命令：`rustc <filename>`

```bash
rustc main.rs # 编译 
```

编译成功后，生成了一个二进制文件，在 Win 下还会生成 main.pdb，其中包含调试信息。

## 运行

```bash
./main # 运行编译好的程序
```

![image.png](https://i.loli.net/2021/11/25/iVSv4UwEFILjTgf.png)

当然，你也可以在 VSCode 中一键编译运行![image.png](https://i.loli.net/2021/11/25/QCsLl9vWKSpY1FI.png)

Rust 是 ahead-of-time 编译的语言 一 可以先编译程序，然后把可执行文件交给别人运行（无需安装Rust)。

rustc 只适合简单的 Rust 程序，大或者文件多的应使用 cargo。

# Cargo

Cargo 是 Rust 的构建系统和包管理器：：一构建代码、下载依赖的库、构建这些库。 

Rust 开发者常用 Cargo 来管理 Rust 工程和获取工程所依赖的库。

## Cargo 创建项目

终端中输入命令：`cargo new hello_rust`

```bash
$ cargo new hello_rust
     Created binary (application) `hello_rust` package
```

当前文件下下会构建一个名叫 hello_rust 的 Rust 工程目录，可以看到文件结构是这样的![image.png](https://i.loli.net/2021/11/25/XBtIQKhPjiRafwU.png)

## 编译运行

构建 Cargo 项目：
`cargo build` 用于创建可执行文件![image.png](https://i.loli.net/2021/11/25/xf9zu3SN6YU2mwE.png)

构建 和 运行 Cargo 项目：
`cargo run` 编译代码 + 执行![image.png](https://i.loli.net/2021/11/25/BjTZzd1wynReYoG.png)因为刚才已经编译过了，而源代码没有改变过，所以这里 cargo就不会再编译了。

`cargo check` 用于检查代码，确保能够编译通过，但不产生任何可执行文件。
cargo check 要比 cargo build 快得多 ― 编写代码的时候可以连续反复的使用cargo check检查代码，提高效率。

## 为发布构建

`cargo build --release` 编译时会进行优化。代码会运行的更快，但是编译时间更长。且会在 `target/release` 而不是 `target/debug` 生成可执行文件。

# 推荐资源

[Rust 官网](https://www.rust-lang.org) 

[The Rust Programming Language](https://doc.rust-lang.org/book/#the-rust-programming-language)

[Take your first steps with Rust - Microsoft](https://docs.microsoft.com/en-us/learn/paths/rust-first-steps/)

[好玩儿的 Rust 语言](https://www.bilibili.com/video/BV1564y1177A?share_source=copy_web)

未完待续（￣︶￣）↗　
持续更新中...
