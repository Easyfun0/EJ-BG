---
layout: post
title:  "Control Flow"
date:   2023-03-16
author: Easyfun
categories: Rust
cover:  "/assets/cover-thumb.png"
---

## 控制流程

在Rust中讓你控制執行流程的方法有if表達式及迴圈。

### if表達式

if能讓條件判斷對你的程式碼產生分支。

{% highlight rust %}

fn main() {
  let num = 3;

  if num < 5 {
    println!("條件為真");
  } else {
    println!("條件為否");
  }
}

{% endhighlight %}

此條件是判斷num是否小於5。條件符合時所要的程式碼區塊被放在條件之後的大括號。與if表達式條件相關的程式段落也被稱為分之(arms)。

可加上else表達式，讓條件不符合時可以去執行另一段程式。如果沒else表達式且條件為否，程式會直接略過if區塊，接著執行後的程式。

程式碼判斷條件必須是bool。如果不符合就會錯誤。

    fn main() {
      let num = 3;

      if num {
        println!("數字為3");
      }
    }

{% highlight rust %}

error[E0308]: mismatched types
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:4:8
  |
4 |     if num {
  |        ^^^ expected `bool`, found integer

error: aborting due to previous error

For more information about this error, try `rustc --explain E0308`.

{% endhighlight %}

這錯誤是說Rust收到bool但是拿到整數。跟Ruby不同，Rust不會自動將非布林值型別轉換成布林值。必須永遠顯示提供布林值給if作為他的條件判斷。

    fn main() {
      let num = 3;

      if num != 0 {
        println!("數字不為0");
      }
    }

#### 使用else if處理多重條件

想實現多重條件的話，將if和else組合成else if表達式。

    fn main() {
      let num = 6;

      if num % 4 == 0 {
        println!("數字可被4整除");
      } else if num % 3 == 0 {
        println!("數字可被3整除");
      } else if num % 2 == 0 {
        println!("數字可被2整除");
      } else {
        println!("數字無法被4,3,2整除");
      }
    }


