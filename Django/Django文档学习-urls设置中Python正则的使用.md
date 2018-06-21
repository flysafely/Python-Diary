* Django 2.0 后支持Python3,最好是3.5以上版本

* import 导入文件变动
django.urls.path 可以看成是 django.conf.urls.url 的增强形式。


1.X | 2.0 | 备注
------------ | ------------- | -------------
无 | django.urls.path | 新增，url的增强版
django.conf.urls.include | django.urls.include | 路径变更
django.conf.urls.url | django.urls.re_path | 异名同功能，url不会立即废弃


* re_path中可以使用正则表达式，可以理解为是原来url()的另外一个名字，功能是一样的
* urls.py 路由表中设置 re_path，如果要使用Python正则中的组，基本形式是(?P<name>),
  同一个表达式中如果要引用前面命名所获取的匹配的信息，可以直接使用(?P=name)
例如:
```
reNamedGroupTestStr = u'标签：<a href="/tag/情侣电话粥/">情侣电话粥</a>';
 
# 1. (?P=name)
# 此处就是通过 (?P=name)的方式，来引用，正则表达式中，前面已经命名tagName的group的
foundTagA = re.search(u'.+?<a href="/tag/(?P<tagName>.+?)/">(?P=tagName)</a>', reNamedGroupTestStr);
print "foundTagA=",foundTagA; #foundTagA= <_sre.SRE_Match object at 0x00876D60>
 
if(foundTagA):
    # 2. mateched.group(name)
    # 可以通过之前给group命的名，来获得匹配到的值
    namedGroupStr = foundTagA.group("tagName");
    print("namedGroupStr=",namedGroupStr)
    #namedGroupStr= 情侣电话粥
 
```
在urls.py 文件中
例如:
```
urlpatterns = [
    re_path(r'^search-form/(?P<TEST>page[0-9]{4})/(?P=TEST)', search_view.search_form),
]

```
对应的在views.py中的视图函数中，需要定义传入参数TEST，来接收组名为TEST匹配后传来的值
```
def search_form(request,TEST):
	print(TEST)
	return render_to_response('search_form.html')
```
