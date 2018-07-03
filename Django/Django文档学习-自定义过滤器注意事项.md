* 不管是在app里面新建还是单独放在一个app里面，都要新建一个名叫templatetags的包
* 之所以是包，就是一定要在这个文件夹里面放一个__init__.py文件
# 自定义过滤器文件
* 在这个templatetags包里面存放过滤器的python文件，例如:

```python
from django import template

register = template.Library()

@register.filter(name = 'cut')
def cut(value, arg):
    "Removes all values of arg from the given string"
    return value.replace(arg, '#')
```
# 注册自定义过滤器app
* 单独放在一个独立的app里面的过滤器需要在setting.py的INSTALLED_APPS中添加这个app
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'mysite.books',
    'filterApp',
]
```
# 模板中应用

* 在模板中如果需要使用自定义的过滤器，需要添加{% load poll_extras_app %}，这里是引用这个过滤器py文件名称，

{% load %} 标签检查 INSTALLED_APPS 中的设置，仅允许加载已安装的Django应用程序中的模板库。 这是一个安全特性；
它可以让你在一台电脑上部署很多的模板库的代码，而又不用把它们暴露给每一个Django安装
