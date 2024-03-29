---
layout: post
title:  "Cargo"
date:   2023-03-07
author: Easyfun
categories: Rust
cover:  "/assets/cover-thumb.png"
---



## Cargo是什麼？

Cargo提供了一系列的工具，從項目的建立,構建到測試,運行直至部署，為Rust提供盡可能完整的手段。也與Rust語言及其編譯器rustc緊密結合。

## 創建專案

創建專案就跟Rails一樣

{% highlight rust %}

$ cargo new new_demo

$ cd new_demo

{% endhighlight %}

會看到創建的結構

$ tree

```
├── .git
├── .gitignore
├── Cargo.toml
└── src
    └── main.rs
```

## 運行方式

有兩種方式可以運行項目:

1.cargo run

2.手動編譯和運行項目

run運行後:
> cargo run

```
  Compiling new_demo v0.1.0 (/Users/huangyingjie/Rprojects/new_demo)

  Finished dev [unoptimized + debuginfo] target(s) in 2.62s

  Running `target/debug/new_demo`

Hello, world!
```

在這個狀態是debug模式，代碼的編譯速度會非常快，但運行的速度就慢了，在debug模式下，Rust編譯器不會做任何的優化，讓你的開發流程更加順暢。

高性能的方法:

🔍cargo run --release

🔍cargo build --realease

### Cargo check

cargo check是我們在程式碼開發過程中最常用指令，它可以快速的檢查一下程式碼能否編譯通過。因此該
命令速度會非常快，能節省大量的編譯時間。

> cargo check

    Checking new_demo v0.1.0 (/Users/huangyingjie/Rprojects/new_demo)

    Finished dev [unoptimized + debuginfo] target(s) in 2.23s

### Cargo.toml 和 Cargo.lock

Cargo.toml和Cargo.lock是cargo的核心文件，主要是基於兩者:

🪒 Cargo.toml是cargo特有的項目數據描述文件。它存了項目的所有原配置信息，如果Rust開發者希望Rust項目能夠依照期望的方式進行建構,測試和運行，那必須按照合理的方式構建Cargo.toml。

🪒 Cargo.lock文件是cargo工具根據同一項目的toml文件生成的項目依賴詳細清單，因此我們一般不用修改它，只需要對著Cargo.toml文件就行了。

### package配置

package中記錄了項目的描述信息如:

{% highlight rust %}

[package]
name = "world_hello"
version = "0.1.0"
edition = "2021"

{% endhighlight %}

name定義了項目名稱，version定義當前版本，新項目是0.1.0，edition字段定義了我們使用的Rust大版本。

### 定義項目依賴

使用cargo工具最大優勢在於，能夠對該項目的各種依賴項進行方便,統一和靈活的管理。

在Cargo.toml中，主要通過各種依賴段落來描述該項目的各種依賴項:

🛡 基於Rust官方crates.io，通過版本來書名描述

🛡 基於項目源代碼的git，通過url來描述

🛡 基於本地項目的絕對路徑或者相對路徑，通過對Unix模式路徑來描述

這三種具體寫法:

```
  [dependencies]
    rand = "0.3"
    hammer = { version = "0.5.0"}
    color = { git = "https://github.com/bjz/color-rs" }
    geometry = { path = "crates/geometry" }
```



