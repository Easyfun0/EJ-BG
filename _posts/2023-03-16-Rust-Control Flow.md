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

{% highlight javascript %}

數字可以被3整除

{% endhighlight %}

這樣的缺點是程式碼過亂，所以可以精簡的話就少用else if。

#### 在let陳述式中使用if

if式表達式，可以把let放在陳述式的右邊，將結果賦值給變數。

    fn main() {
      let condiction = true;
      let num = if condition { 5 } else  { 6 };
      println!("數字結果為: {num}");
    }

變數num會得到if表達式運算出的數值。

if表達式的值取決於哪段程式碼被執行。可代表成為最終的每一個if分支必須是要相同型別。

    fn main() {
      let condition = true;

      let num = if condition { 5 } else { "六" };

      println!("數字結果為: {num}");
    }

if和else分支型別不一致的錯誤。

{% highlight rust %}

error[E0308]: `if` and `else` have incompatible types
 --> /Users/huangyingjie/Rprojects/function/src/main.rs:4:43
  |
4 |       let num = if condition { 5 } else { "六" };
  |                                -          ^^^^ expected integer, found `&str`
  |                                |
  |                                expected because of this

error: aborting due to previous error

For more information about this error, try `rustc --explain E0308`.

{% endhighlight %}

if段落表達式算出整數，但else的區塊卻算出字串。

Rust提供了多種產生迴圈(loops)的方式。一個迴圈會執行一段程式碼區塊，在結束時馬上回到區塊起始位置繼續執行。

迴圈:loop, while, for。

#### 使用loop重複執行程式碼

loop關鍵字告訴Rust反覆不停的執行一段程式碼直到要他停下來。

    fn main() {
      loop {
        println!("Again");
      }
    }

執行後會一直不停的重複，直到手動停止。

#### 從迴圈回傳數值

如果有迴圈在迴圈之內的話，break和continue會用在該位置最內層的迴圈中。可以選擇在迴圈使用迴圈標籤(loop label)，然後使用break和continue加上那些迴圈標籤定義的關鍵字，而不是用在最內層迴圈。

    fn main() {
      let mut count = 0;
      'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
          println!("remaining = {remaining}");
          if remaining == 9 {
            break;
          }
          if count == 2 {
            break 'counting_up;
          }
          remaining -= 1;
        }
        count += 1;
      }
      println!("End count = {count}");
    }

外層迴圈有'counting_up的標籤，會從0數到2。內層沒有迴圈標籤的迴圈會從10數到9。第一個break沒有指定任何標籤只會離開內層迴圈。而陳述式break 'counting_up;會離開外層迴圈。

{% highlight rust %}

count = 0
remaining = 10
remaining = 9
count = 1
remaining = 10
remaining = 9
count = 2
remaining = 10
End count = 2

{% endhighlight %}

#### 使用while做條件迴圈

    fn main() {
      let mut num = 3;

      while num != 0 {
        println!("{num}!");

        num -= 1;
      }
      println!("GO");
    }

用while減少了loop,if,else和break會有的巢狀結構。當條件為true的就執行不然的話就離開迴圈。

#### 使用while遍歷集合

可以用while遍歷一個集合元素，像是陣列。

    fn main() {
      let a = [10, 20, 30, 40, 50];
      let mut index = 0;

      while index < 5 {
        println!("數值為: {}", a[index]);

        index += 1;
      }
    }

{% highlight rust %}

數值為: 10
數值為: 20
數值為: 30
數值為: 40
數值為: 50

{% endhighlight %}

五個元素都顯示在上。index會在某一刻達到5，但迴圈會再嘗試取得陣列第六個元素就停止。

用for迴圈可以更精簡這段。

    fn main() {
      let a = [10, 20, 30, 40, 50];

      for element in a {
        println!("數值為: {element}");
      }
    }

for迴圈的安全性與簡潔程度式Rust最常使用的結構。

這邊使用rev方法來反轉。

    fn main() {
      for num in (1..4).rev(){
        println!("{num}");
      }

      println!("GO");
    }


