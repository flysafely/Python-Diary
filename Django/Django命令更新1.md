### 一、 数据库的配置：

        1、首先你要保证在终端上安装了数据库（MySQL）。接下来在在里面创建你自己的数据库，比如create database djangodb.

        2、cd到你创建工程的目录，我的是username/djcode/mysite,然后cd 到mysite里，然后vim settings.py,对这个文件中的DATABASES项进行设置，完成后大概是这样的

         DATABASES = {
       ‘default‘: {
        ‘ENGINE‘: ‘django.db.backends.mysql‘,
        ‘NAME‘: ‘django‘,#你使用的数据库名字
        ‘USER‘: ‘root‘,
        ‘PASSWORD‘:‘‘,  #这里填写你的数据库密码
        ‘HOST‘: ‘localhost‘,
        ‘PORT‘:‘3306‘,
         }
      }

       当你运行python manage.py shell时可能会遇到错误，比如提示你没有mysqldb，那你应该按照Python -easy -install

### 二、创建模型

       还要把你的模型放在settings.py中INSTALLED_APPS。你的模型就是你在工程目录下执行python manage.py startapp books时创建的，名字不一定要叫books。创建完对其进行定义。然后你要激活模型，将 books app添加到配置文件的已安装应用列表中即可完成此步骤。设置完貌似是这样的：

       INSTALLED_APPS = [
    ‘django.contrib.admin‘,
    ‘django.contrib.auth‘,
    ‘django.contrib.contenttypes‘,
    ‘django.contrib.sessions‘,
    ‘django.contrib.messages‘,
    ‘django.contrib.staticfiles‘,
    ‘books‘,  #不要忘记后面的逗号
]

      定义并激活了模型，你可能会验证模型是否有效，如果我没说错，你可能会执行python manage.py validate ，然后你会特别伤心的看到人家提示Unknown command: ‘validate‘Type ‘manage.py help‘ for usage.，对吧？所以你要用如下这个命令：python manage.py check来验证。

      然后你还想生成sql语句，你就运行了python manage.py sqlall books,错误提示是Unknown command: ‘sqlall‘Type ‘manage.py help‘ for usage.同样如果你想提交sql语句到数据库而运行syncdb，错误提示是Unknown command: ‘syncdb‘
Type ‘manage.py help‘ for usage. 为什么没有这些命令，因为它们被淘汰了。所以你只需运行如下的命令：

      python manage.py makemigrations books    #用来检测数据库变更和生成数据库迁移文件

      python manage.py migrate     #用来迁移数据库

      python manage.py sqlmigrate books 0001 # 用来把数据库迁移文件转换成数据库语言

        在命令行依次执行完这三个命令你就可以进行数据访问了。

        因为我曾经被这些问题困扰 ，所以真心希望对看的这篇博客的人有所帮助。
