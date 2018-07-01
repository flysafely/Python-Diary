* Django 自动默认开启转义功能(指的是最后生成html文件里面的内容，如果遇到需要转义的符号，会自动转义)
* Django 单个模板变量，通过 |safe 关闭自动转义,例如:
```Python
This will be escaped: {{ data }}
This will not be escaped: {{ data|safe }}
```
* Django 特定部分转义控制，通过{% autoescape off %}...{% endautoescape %} 关闭，{% autoescape on %}...{% endautoescape %} 打开
```Python
Auto-escaping is on by default. Hello {{ name }}

{% autoescape off %}
    This will not be auto-escaped: {{ data }}.

    Nor this: {{ other_data }}
    {% autoescape on %}
        Auto-escaping applies again: {{ name }}
    {% endautoescape %}
{% endautoescape %}
```

* 浏览器最后渲染的结果和HTML中的生成内容是两个不同的概念，例如:
```html
<script>alert('hello')</script>
```
以上html内容通过打开浏览器渲染后，会出现弹窗提示！
```html
&lg;script>alert('hello')</script>
```
以上&lg; 是< 转义后，在html没有被渲染时候的内容，可以通过记事本打开查看源码。
但是通过浏览器打开，渲染后，浏览器会显示<script>alert('hello')</script>，并不会出现上面例子一样的弹窗。

* Django中如果没有特殊指定关闭转义，所有需要转义的字符都会被自动转义成对应的转义后显示在html中，然后通过浏览器渲染后再显示出来。
* 浏览器渲染的时候如果获取到的html中是转义后的符号，则会反转义成一个普通字符串后直接显示出来，并不会理解其深层前后组合后时候有其他含义。
* Django 在views.py从数据库中获取了一段字符串 <script>alert('hello')</script> 后，如果关闭转义直接生产HTML文件，交由浏览器，则会出现弹窗，此时，右键阅读源码，HTML源码也是显示的<script>alert('hello')</script>。但是这个的<>对于浏览器渲染是有特殊含义的。
* Django 在views.py从数据库中获取了一段字符串 <script>alert('hello')</script> 后，如果打开转义直接生产HTML文件，交由浏览器，则不会出现弹窗，此时，右键阅读源码，HTML源码是显示的&lt;script&gt;alert(&#39;hello&#39;)&lt;/script&gt;。但是这个的<>对于浏览器渲染是有特殊含义的。
