---
layout: post
title:  "Data Types"
date:   2023-03-09
author: Easyfun
categories: Rust
cover:  "/assets/cover-thumb.png"
---



## 資料型別

Rust每個值都有其確切的數據類型，分為兩種資料型別子集:純量(scalar)與複合(compound)

Rust是靜態型別語言，代表他必須在編譯時知道所有變數的型別。

Rust編譯器很聰明，可以根據變數的值上下文中的使用方式來自動推導出變數的值，同時他也在某些情況下，無法推導出變數類型。

  let guess = "30".parse().expect("Not a number!");

## 純量型別

純量型別代表單一數值。

Rust有四種主要的純量型別:整數,浮點數,布林及字元。

### 整數型別

整數是沒有小數點的點數。

Rust中的整數型別


| 長度      | 帶號 |    非帶號     |
| :---:       |    :----:   |    :---:      |
| 8位元      | i8       | u8   |
| 16位元   | i16        | u16      |
| 32位元 | i32 | u32 |
| 64位元 | i64 | u64 |
| 123位元 | i128 | u128 |
| 系統架構 | isize | usize |

每個變體都可以是帶號或非帶號，並有明確大小。帶號與非帶號的區別是數字能不能有負數，換句話說就是數字能否帶有正負符號，如果沒有的話就只會出現正整數。

每一帶號變體可以儲存數字範圍包含從-(2n - 1) 到 2n - 1 - 1 以內的數字，n就是該變體佔用的位元大小。

所以一個==ib==可以儲存的數字範圍就是從-(27) 到 27 - 1，也就是-128到127。而非帶號可以儲存的數字範圍則是從0到2n - 1，所以==u8==可以儲存的範圍是從0到28 - 1，也就是 0 到 255。

isize與usize型別則是依據你程式運算電腦架構來決定大小，所以上表才用「系統架構」來表示長度:如果你在64位元架構上的話就是64位元;如果是32位元架構的話就是32位元。

Rust中的整數字面值

| 數字字面值 | 範例 |
| 十進制 | 98_222 |
| 十六進制 | 0xff |
| 八進制 | 0o77 |
| 二進制 | 0b1111_0000 |
| 位元組(僅限u8) | b'A' |

你該用到哪些整數型別呢，如果不確定的話，Rust預設的型別是很好的起始點:整數型別預設是i32。而你會用到isize或usize的主要時機是作為某些集合的索引。

#### 整數溢位

假設你有個變數型別是==u8==可以儲存0到255的數值。如果想要改變變數的值超出這個範圍的話，比方256，那麼就會發生整數溢位，這會產生兩種不同的結果。如果是除錯模式編譯的話，Rust會包含整數溢位的檢查，造成程式執行時恐慌(panic)。Rust使用恐慌來表示程式因錯誤而結束。

當你在發佈模式下用--release來編譯，Rust則不會加上整數溢位的檢查而造成恐慌。相反如果發生整數溢位的話，Rust會做出二補數包裝的動作。超出最大值的數值可以被包裝成該型別的最低數值。以==u8==為例的話，256會變成0,257會變成1以此類推。程式不會恐慌，但是該變數可能會得到一個不是你原本預期的數值。通常依靠整數溢位的行為仍然會被視為邏輯錯誤。

要顯示處理可能的溢位的話，你可以使用以下標準函式庫中基本型別提供一系列方法:

  ⛵ 將所有操作用==wrapping_*==方法包裝，像是==wrapping_add==。
  ⛵ 使用==checked_*==方法，如果有溢位的話其會回傳==None==數值。
  ⛵ 使用==overflowing_*==方法，其會回傳數值與一個布林值來顯示是否有溢位發生。
  ⛵ 屬於==saturating_*==，讓數值溢位時保持在最小或最大值。


### 浮點數型別

Rust還有針對小數點的浮點數提供兩種基本型別:f32和f64，分別佔有32位元與64位元的大小。而預設的型別為f64，現代處理速度幾乎和f32一樣卻還能擁有更高的精準度。所有的浮點數型別都是帶號的(signed)。

{% highlight rust %}

fn main() {
  let x = 2.0;  // f64
  let y: f32 = 3.0; // f32
}

{% endhighlight %}

浮點數是依照IEEE-754所定義的，f32型別是單精度浮點數，而f64是倍精度浮點數。

### 數值運算

Rust支援你所想到的數值型別基本運算:加法,減法,除法和取餘。整數除法會取最接近零的下界數值。

{% highlight rust %}

fn main() {
  // 加法
  let sum = 5 + 10;

  // 減法
  let difference = 95.5 - 4.3;

  // 乘法
  let product = 4 * 30;

  // 除法
  let quotient = 56.7 / 32.2;
  let truncated = -5 / 3;  // 結果為-1

  // 取餘
  let remainder = 43 % 5;
}

每一個陳述式中的表達式都使用了一個數學運算符號並計算出一個數值出來，賦值給該變數。

### 布林型別

Rust中的布林型別有兩個值:true和false。布林值大小為一個位元組。要在Rust中定義布林型別的話:

{% highlight %}

fn main() {
  let t = true;

  let f:bool - false; // 型別詮釋的方式
}

{% endhighlight %}

布林值最常使用的方式之一是作為條件判斷，像是在if表達式中使用。

### 字元型別

Rust的char型別是最基本的字母型別。

{% highlight rust %}

fn main(){
  let c = 'z';
  let z: char = 'Z'; // 明確標註型別的寫法
  let heart_eyed_cat = '😺';
}

{% endhighlight %}

注意到char字面值是用單引號賦值，宣告字串字面值時才是用雙引號。Rust的char型別大小為四個位元組並表示為一個Unicode純量數值，代表他能擁有的字元比ASCII還來得多。標音字母(Accented letters),中文,日文,韓文,表情符號以及零長度空格都是Rust==char==的有效字元。

Unicode純量數值的範圍包含從==U+0000==到==U+E000==以及==U+E000==到==U+10FFFF==。但一個「字元」並不是真正的Unicode概念，對於什麼是一個「字元」的看法可能會和Rust的char不一樣。

### 複合型別

複合型別可以組合數個數值為一個型別，Rust有兩個基本複合型別:元組(tuples)和陣列(arrays)。

#### 元組(Tuple)型別

元組是個將許多不同型別的數值合成一個復合型別的方法。元組擁有固定長度:一旦宣告好後，他們就無法增長或縮減。

建立一個元組的方法是寫一個用括號囊括起來的數值列表，每個值再用逗號分隔開來。元組的每一格都是一個獨立型別，不同數值不必事相同型別。

{% highlight rust %}

fn main() {
  let tup = (500, 6.4, 1);

  let (x, y, z) = tup;

  println!("y的數值為: {y}");
}

{% endhighlight %}

此式是建立了一個元組然後賦值給tup，接著用模式配對和let將tup拆成三個個別的變數x,y,z。這就是解構(destructuring)，因它將單一元組拆成了三個部分。最後將y的值印出來，也就是6.4。

我們也可用句號(.)再加上數值的索引來取得元組內的元素。

{% highlight rust %}

fn main() {
  let x: (i32, f64, u8) = (500, 6.4, 1);

  let five_hundred =  x.0;

  let six_point_four = x.1;

  let one = x.2;
}


{% endhighlight %}

此建立了元組x，然後用他們個別的索引來存取元組的元素。和多數語言一樣，元組的第一個索引是0。

沒有任何數值的元組有一種特殊名稱叫做單元型別(Unit)，其數值與型別都寫作()，代表一個空的數值或空的回傳型別。表達式要是沒有回傳任何數值的話，他們就會隱式回傳單位型別。


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



