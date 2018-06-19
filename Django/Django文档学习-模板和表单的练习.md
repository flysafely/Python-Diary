## 关于模板在表单中的运用练习
* http://djangobook.py3k.cn/2.0/chapter07/ 第7章节中一个作业题：
简单的view函数来显示 request.META 的所有数据，这样你就知道里面有什么了。 这个view函数可能是这样的：
```
def display_meta(request):
    values = request.META.items()
    values.sort()
    html = []
    for k, v in values:
        html.append('<tr><td>%s</td><td>%s</td></tr>' % (k, v))
    return HttpResponse('<table>%s</table>' % '\n'.join(html))
```
在views.py中的函数模板写法:
```
def display_meta(request):
    values = request.META.items()
    #html = []
    #for k, v in values:
    #    html.append('<tr><td>%s</td><td>%s</td></tr>' % (k, v))
    return HttpResponse(ShowMetaByTemplateHtml(values))
    #return HttpResponse('<table>%s</table>' % '\n'.join(html))

def ShowMetaByTemplateHtml(metalist):
    raw_template = """
    <html>
    <body>
    <p>request meta info ...........</p>
    <table>
    {% for meta in meta_list %}

        <tr>
            <td><b>{{meta.0}}:</b></td>
            <td>{{meta.1}}</td>
        </tr>

    {% endfor %}
    </table>
    </body>
    </html>
    """
    temp = Template(raw_template)
    con = Context({'meta_list':metalist})
    temp_con = temp.render(con)
    print(temp_con)
    return temp_con


```
