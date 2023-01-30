---
layout: post
title:  "Ruby-Arrays and Hashes"
date:   2023-01-30
author: Easyfun
categories: Ruby
tags:	jekyll welcome
cover:  "/assets/ror.jpeg"
---


## Array

Ruby中的Arrays和雜湊都是有索引的集合。

這兩個集合保存都是對象。數組中可以同時包含整數,字符串,浮點數。

{% highlight ruby %}
a = [1, 'cat', 3.14]
{% endhighlight %}

可以使用a = Array.new 來建立

{% highlight javascript %}
a = Array.new        #=> []

Array.new(3)         #=> [nil, nil, nil]

Array.new(3, true)   #=> [true, true, true]
{% endhighlight %}

創建一個單獨的數組，可以傳遞一個區塊。

這個方法可安全地用在可變對象例如:hashes,strings or other arrays

{% highlight javascript %}
Array.new(4) {Hash.new}    #=> [{}, {}, {}, {}]

Array.new(4) {|i| i.to_s}  #=>["0", "1", "2", "3"]
{% endhighlight %}

可以使用Array#[]的方法檢索裡面的元素，他可以採用單個整數,一對參數或範圍，負索引從末尾開始計數，-1是最後一個元素。

{% highlight javascript %}
a = [1,2,3,4,5,6]  #=> 3
a = [100]          #=> nil
a = [-3]           #=> 4
a = [2,3]          #=> [3,4,5]
a = [1..4]         #=> [2,3,4,5]
a = [1..-3]        #=> [2,3,4]
{% endhighlight %}

訪問特定元素的另一個方法是用at

    arr.at(0)   #=>1

### Hashes

Ruby中的Hash與Array類似。差別在Array使用大括號而不是方括號。

Hash字面量每個元素都由兩對象組成，一個是key一個是value


{% highlight ruby %}
inst_section = {
  :cello     => 'string'
  :clarinet  => 'woodwind',
  :drum      => 'percussion',
  :oboe      => 'woodwind',
  :trumept   => 'brass',
  :violin    => 'string',
}
{% endhighlight %}

=>的左邊是key，右邊是value。

Hash中的key必須是唯一的，上述Hash中存在兩個:drum，那麼只有後面的會生效，Hash中的key和value可以是任意對象。

Hash使用符號的情況很常見，因此Ruby提供了特殊語法，減少重複的次數。

{% highlight ruby %}
inst_section = {
  :cello     'string'
  :clarinet  'woodwind',
  :drum      'percussion',
  :oboe      'woodwind',
  :trumept   'brass',
  :violin    'string',
}
{% endhighlight %}

