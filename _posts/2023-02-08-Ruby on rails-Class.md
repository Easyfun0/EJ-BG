---
layout: post
title:  "Ruby的世界"
date:   2022-04-20
author: Easyfun
categories: Ruby
tags:	welcome
cover:  "/assets/ror.jpeg"
---

Rails大量使用了類級聲明，在類定義的主體都是對類的斷言。

在定義方法時，給方法名加上前綴，所定義的是類方法。

類方法是可以直接在類上面調用的方法。

    to_collect = Order.find_all_unpaid


類的對象通過對實例變量保存狀態。

實例變量以@開頭，這些變量可以在類的實例方法中使用，每個對象都有自己一組實例變量。

{% highlight javascript %}
class Greeter
  def initialize(name)
    @name = name
  end

  def name
    @name
  end

  def name = (new_name)
    @name = new_name
  end

end

g = Greeter.new(Mike)

g.name    # => Mike
g.name = 'Easyfun'
g.name    # => Easyfun

{% endhightlight %}

Ruby提供的快捷方法:

{% highlight javascript %}
class Greeter
  attr_ancessor :name  #創建讀值方法和設置方法
  attr_reader   :greeting #只創建讀值方法
  attr_writer   :age   #只創建設值方法
end
{% endhighlight %}

### 類的公開方法

我們可以把實例方法定義為私有方法或受保護的方法。

{% highlight javascript %}
class MyClass      
    def m1      # 公開方法
    end
    protected
    def m2      # 受保護的方法
    end
    private
    def m3      # 私有方法
    end
end
{% endhighlight %}

private指令是最嚴格的，一個對象的私有方法只能用在這個對象中調用。

受保護的方法既可以在同一個對象中調用，也可以在同一個類及其子類的其他實例中調用。

類不是Ruby中唯一的組織結構，模組也是一種組織結構。

