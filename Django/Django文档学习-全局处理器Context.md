* 旧版的
```python
render_to_response()
```
不再使用,除非想手写
```python
context_instance=RequestContext(request,processer='xxx')
```
* 新版直接用
```python
render(request, templateName, context)
```
注意:render()在新版中始终是强制使用RequestContext来传递参数的，包括默认和自定义context处理器中的全局参数
例如:
```python
方法1：
def index(request):
    return render_to_response('index.html', context_instance=RequestContext(request))
方法2：
def index(request):
    return render(request, 'index.html')

效果是一样的，但是第一种明显很啰嗦。
```

* 关于新版Django中的render()还有一个值得一提的是

1.CSRF功能的默认使用

上面例子提到的render会自动将request和相应的默认或者自定义context处理器里面定义的参数
通过RequestContext来传递给模板。

2.可以理解为：RequestContext在传递上下文参数的时候会把csrf_token的值一并传过去，
如果不使用这种方式(render(),或者render_to_response('index.html', context_instance=RequestContext(request))
则模板{% csrf_token %}就没有值，也就没有正确启动csrf功能。
