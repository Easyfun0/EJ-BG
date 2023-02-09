---
layout: post
title:  "Ruby的慣用法"
date:   2023-02-09
author: Easyfun
categories: Ruby
tags:	jekyll welcome
cover:  "/assets/ror.jpeg"
---


## empty!和empty?

在Ruby中，方法名可以驚嘆號或問號結尾。

判斷方法會根據條件的變回返回true或false。

### a || b

求表達式 a || b的值時，先求a的值。 如果a的值不是false或nil，則停止求值，回傳a:否則回傳b。

當需要為變量設置默認值時，經常會採用這種方式，只要變量的值還未設置，就會回傳變量的默認值。

### a ||= b

Ruby支持 a op= b的方式  a op=b等於a = a op b。

{% highlight javascript %}
count += 1           # 等於 count = count + 1
price *= discount    #  price = price * discount
count ||= 0          # count = count || 0
{% endhighlight %}

因此對於count || = 0 如果count原來的值是nil或是false那復職後的他的值會變為0

