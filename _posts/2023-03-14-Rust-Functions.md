---
layout: post
title:  "Rust的世界"
date:   2023-03-14
author: Easyfun
categories: Rust
cover:  "/assets/cover-thumb.png"
---

## 函式

main函式是入口點，fn關鍵字來宣告新的函式。

Rust是使用snake case式作為函式與變數名稱的慣例。所有字母都是小寫，並用底線區隔單字。

{% highlight rust %}

fn main() {
  println!("Hiiii");

  another_function();
}

fn another)function() {
  println!("HIIIII");
}

{% endhighlight %}

Rust定義函式是從fn開始，再加上函式名稱和一組括號，大括號告訴編譯器函式本體開始與結束。

程式碼會按照main函式中的順序。首先Hiiii會先顯示出來，再來才會呼叫another_function並印出他的訊息。

## 參數

我們可定義函式成擁有參數(parameters)的，這是函式簽名(signatures)中特殊的變數。

如果要定義多個參數時，會用逗號區隔開來:

{% highlight rust %}

fn main() {
  print_labeled_measurement(5, 'h');
}

fn print_labbeled_measurement(value: i32, unit_label: char) {
  println!("測量值為: {value}{unit_label}");
}

{% endhighlight %}

我們呼叫函數時，將5給了value且將'h'給了unit_label，程式輸出就會包含這些數值。

### 陳述式與表達式

函式本體是由一系列的陳述式(statements)並在最後可以選擇加上表達式(expression)來組成。

🧿 陳述式(Statements)是進行一些動作的指令，且不回傳任何數值。

🧿 表達式(Expressions)式計算並產生數值。

    fn main() {
      let y = 6;
    }

此函式定義也是陳述式，整個範例就是一個陳述式。

陳述式不會回傳數值，因此無法將let陳述式賦值給其他變數。

     fn main() {
      let x = (let y = 6);
     }

{% highlight rust %}

error: expected expression, found `let` statement
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:3:16
  |
3 |       let x = (let y = 6);
  |                ^^^

error: expected expression, found statement (`let`)
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:3:16
  |
3 |       let x = (let y = 6);
  |                ^^^^^^^^^
  |
  = note: variable declaration using `let` is a statement

error[E0658]: `let` expressions in this position are unstable
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:3:16
  |
3 |       let x = (let y = 6);
  |                ^^^^^^^^^
  |
  = note: see issue #53667 <https://github.com/rust-lang/rust/issues/53667> for more information

warning: unnecessary parentheses around assigned value
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:3:15
  |
3 |       let x = (let y = 6);
  |               ^         ^
  |
  = note: `#[warn(unused_parens)]` on by default
help: remove these parentheses
  |
3 -       let x = (let y = 6);
3 +       let x = let y = 6;
  |

error: aborting due to 3 previous errors; 1 warning emitted

For more information about this error, try `rustc --explain E0658`.

{% endhighlight %}

let y = 6陳述式不回傳數值，所以x得不到任何數值。像是C或Ruby，他們的賦值仍能回傳所得到的值。在那些語言你可以==x = y = 6==同時讓x與y都取得6但在Rust就不行。


