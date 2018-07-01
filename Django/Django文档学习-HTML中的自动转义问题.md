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
