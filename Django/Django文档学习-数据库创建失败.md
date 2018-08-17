在修改了models.py后，有些用户会喜欢用python manage.py makemigrations生成对应的py代码。

但有时执行python manage.py makemigrations命令，会提示"No changes detected." 可能有用的解决方式如下：



1. 直接使用python manage.py migrate.

可能会先生成对应数据库的py代码，再自动执行这段代码，创建数据库表格 （我没有仔细去读文档 不清楚这条命令的逻辑）



2. 来自：https://docs.djangoproject.com/en/1.8/topics/migrations/

先 python manage.py makemigrations --empty yourappname 生成一个空的initial.py

再 python manage.py makemigrations 生成原先的model对应的migration file
