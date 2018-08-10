```python
ret=UserInfo.objects.all()
```
all返回的是QuerySet对象，程序并没有真的在数据库中执行SQL语句查询数据，但支持迭代，使用for循环可以获取数据。

注意返回值:**[<Publisher: Apress>, <Publisher: O'Reilly>]**
```python
Publisher.objects.all()
[<Publisher: Apress>, <Publisher: O'Reilly>] #返回的是类似列表的一个数据
```
---
```python
ret=UserInfo.objects.get(id='1')
```
get返回的是Model对象，类型为列表，说明使用get方法会直接执行sql语句获取数据

注意返回值:**<Publisher: Apress>**
```python
Publisher.objects.get(id=50)
<Publisher: Apress> #返回的是类似列表的一个数据
```
---
```python
ret=UserInfo.objects.filter()
```
filter和get类似，但支持更强大的查询功能 

补充： 
示例:
```python
Publisher.objects.filter(name__contains="press")
```

条件选取querySet的时候，filter表示=，exclude表示!=。 

querySet.distinct() 去重复

__exact 精确等于 like ‘aaa’ 

__iexact 精确等于 忽略大小写 ilike ‘aaa’ 

__contains 包含 like ‘%aaa%’ 

__icontains 包含 忽略大小写 ilike ‘%aaa%’，但是对于sqlite来说，contains的作用效果等同于icontains。 

__gt 大于 

__gte 大于等于 

__lt 小于 

__lte 小于等于 

__in 存在于一个list范围内 

__startswith 以…开头 

__istartswith 以…开头 忽略大小写 

__endswith 以…结尾 

__iendswith 以…结尾，忽略大小写 

__range 在…范围内 

__year 日期字段的年份 

__month 日期字段的月份 

__day 日期字段的日 

__isnull=True/False 
