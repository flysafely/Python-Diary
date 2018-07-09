
## 自定义模板标签后设置变量值

很多时候设置一个模板变量而非返回值也很有用

要在上下文中设置变量，在 render() 函数的context对象上使用字典赋值。 这里是一个修改过的 CurrentTimeNode ，其中设定了一个模板变量 current_time ，并没有返回它：
* 节点定义和渲染定义

```python
class CurrentTimeNode2(template.Node):
    def __init__(self, format_string):
        self.format_string = str(format_string)

    def render(self, context):
        now = datetime.datetime.now()
        context['current_time'] = now.strftime(self.format_string)
        return ''
```

* 函数定义和注册

```python
@register.tag(name = 'do_current_time2')
def do_current_time2(parser, token):
    try:
        tag_name, arg = token.split_contents(None, 1)
    except ValueError:
        msg = '%r tag requires arguments' % token.contents[0]
        raise template.TemplateSyntaxError(msg)
    return CurrentTimeNode2(arg)
```

* 注意 render() 返回了一个空字符串。 render() 应当总是返回一个字符串，所以如果模板标签只是要设置变量， render() 就应该返回一个空字符串。

你应该这样使用这个新版本的标签：

```python
{% current_time2 "%Y-%M-%d %I:%M %p" %}
<p>The time is {{ current_time }}.</p>
```

* 但是 CurrentTimeNode2 有一个问题: 变量名 current_time 是硬编码的。 这意味着你必须确定你的模板在其它任何地方都不使用 {{ current_time }} ，因为 {% current_time2 %} 会盲目的覆盖该变量的值。

一种更简洁的方案是由模板标签来指定需要设定的变量的名称，就像这样：

```python
{% get_current_time "%Y-%M-%d %I:%M %p" as my_current_time %}
<p>The current time is {{ my_current_time }}.</p>
```

为此，你需要重构编译函数和 Node 类，如下所示：

```python
import re

class CurrentTimeNode3(template.Node):
    def __init__(self, format_string, var_name):
        self.format_string = str(format_string)
        self.var_name = var_name

    def render(self, context):
        now = datetime.datetime.now()
        context[self.var_name] = now.strftime(self.format_string)
        return ''

def do_current_time(parser, token):
    # This version uses a regular expression to parse tag contents.
    try:
        # Splitting by None == splitting by spaces.
        tag_name, arg = token.contents.split(None, 1)
    except ValueError:
        msg = '%r tag requires arguments' % token.contents[0]
        raise template.TemplateSyntaxError(msg)

    m = re.search(r'(.*?) as (\w+)', arg)
    if m:
        fmt, var_name = m.groups()
    else:
        msg = '%r tag had invalid arguments' % tag_name
        raise template.TemplateSyntaxError(msg)

    if not (fmt[0] == fmt[-1] and fmt[0] in ('"', "'")):
        msg = "%r tag's argument should be in quotes" % tag_name
        raise template.TemplateSyntaxError(msg)

    return CurrentTimeNode3(fmt[1:-1], var_name)
 ```
现在 do_current_time() 把格式字符串和变量名传递给 CurrentTimeNode3 。
