* 1、我们运行django程序的时候，一般都是直接使用python manage.py runserver，其实这里面有些默认设置需要我们注意的。看官方的文档：这里，摘录下面几句。
```python
Note that the default IP address, 127.0.0.1, 
is not accessible from other machines on your network. 
To make your development server viewable to other machines on the network, 
use its own IP address (e.g. 192.168.2.1) or 0.0.0.0 or :: (with IPv6 enabled).
```

* 2、意思很明确，如果想让其他机器访问的话，发布的时候IP地址就不能用127.0.0.1了，要么用0.0.0.0要么用局域网的IP地址（比如windows上可以用ipconfig查看）。当然，0.0.0.0可以省略成0，所以最简单的可以写成：
```python
python manage.py runserver 0:8000
```

* 3、这样运行之后，就可以使用这台开发电脑的局域网IP地址（比如是192.168.1.1）去访问了，比如192.168.1.1:8000/posts之类的。
