---
layout: post
title:  "Rust的世界"
date:   2023-03-07
author: Easyfun
categories: Rust
cover:  "/assets/cover-thumb.png"
---



## Cargo是什麼？

Cargo提供了一系列的工具，從項目的建立,構建到測試,運行直至部署，為Rust提供盡可能完整的手段。也與Rust語言及其編譯器rustc緊密結合。

### 創建專案

創建專案就跟Rails一樣

{% highlight rust %}

$ cargo new new_demo

$ cd new_demo

{% endhighlight %}

會看到創建的結構

$ tree
.
├── .git
├── .gitignore
├── Cargo.toml
└── src
    └── main.rs


### 運行方式

有兩種方式可以運行項目:

1.cargo run

2.手動編譯和運行項目

run運行後:
> cargo run
   Compiling new_demo v0.1.0 (/Users/huangyingjie/Rprojects/new_demo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.62s
     Running `target/debug/new_demo`
Hello, world!
