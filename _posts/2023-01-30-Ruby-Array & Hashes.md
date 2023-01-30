---
layout: post
title:  "Ruby-Arrays and Hashes"
date:   2023-01-30
author: Easyfun
categories: Ruby
tags:	jekyll welcome
cover:  "/assets/ror.jpeg"
---


## Array & Hashes

Ruby中的Arrays和雜湊都是有索引的集合。

這兩個集合保存都是對象。數組中可以同時包含整數,字符串,浮點數。

    a = [1, 'cat', 3.14]

可以使用a = Array.new 來建立

    a = Array.new        #=> []

    Array.new(3)         #=> [nil, nil, nil]

    Array.new(3, true)   #=> [true, true, true]

創建一個單獨的數組，可以傳遞一個區塊。

這個方法可安全地用在可變對象例如:hashes,strings or other arrays

{% highlight ruby %}
Array.new(4) {Hash.new}    #=> [{}, {}, {}, {}]

Array.new(4) {|i| i.to_s}  #=>["0", "1", "2", "3"]
{% endhighlight %}

### 萬物即物件

在 Ruby 裡，萬物皆物件。所有的資訊與程式碼，都給傳遞給物件擁有的屬性（properties）與行為（actions）。物件導向程式設計中稱屬性為實體變數（ instance variables ）而行為稱為方法（ methods ）。從下列程式碼中看到 Ruby 能夠給 “數字（number）” 賦予 “行為（actions）” 這特點來看，足以證明 Ruby 是個純物件導向的語言。


許多的語言裡，數字與其他的原生資料型態（primitive types）都不是物件。 而 Ruby 受到了 Smalltalk 語言讓所有的資料型態都可賦予方法與產生實體變數的影響。更進而讓這規則適用於 Ruby 中所有物件。

### Ruby 的靈活性

<!-- {% highlight ruby %}  -->
  Ruby 是個相當靈活的語言，可以讓使用者自由的去改變語言的各個部分。 Ruby 的本質部份也可以隨意地被移除或重新定義。現有的部份也可以繼續添加內容。Ruby 試著不去限制程式設計人員。
<!-- {% endhighlight %} -->

### Code Snippets

You can use [highlight.js][highlight] to add syntax highlight code snippets:

Use the [Liquid][liquid] `{% raw %}{% highlight <language> %}{% endraw %}` tag to add syntax highlighting to code snippets.

For instance, this template...
{% highlight html %}
{% raw %}{% highlight javascript %}    
function demo(string, times) {    
  for (var i = 0; i < times; i++) {    
    console.log(string);    
  }    
}    
demo("hello, world!", 10);
{% endhighlight %}{% endraw %}
{% endhighlight %}

...will come out looking like this:

{% highlight javascript %}
function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);
{% endhighlight %}

Syntax highlighting is done using [highlight.js][highlight]. You can change the active theme in [head.html](https://github.com/bencentra/centrarium/blob/2dcd73d09e104c3798202b0e14c1db9fa6e77bc7/_includes/head.html#L15).

### Images

Lightbox has been enabled for images. To create the link that'll launch the lightbox, add <code>data-lightbox</code> and <code>data-title</code> attributes to an <code>&lt;a&gt;</code> tag around your <code>&lt;img&gt;</code> tag. The result is:

<a href="//bencentra.com/assets/images/falcon9_large.jpg" data-lightbox="falcon9-large" data-title="Check out the Falcon 9 from SpaceX">
  <img src="//bencentra.com/assets/images/falcon9_small.jpg" title="Check out the Falcon 9 from SpaceX">
</a>

For more information, check out the [Lightbox][lightbox] website.

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
[liquid]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
