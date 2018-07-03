* /   网站根路径 

* ./  当前路径

* ../ 上一级路径

* ../../ 上两级路径，如果没有2级，就是根目录

* windows中用\，Unix/Linux用/


例如以上 本地静态网站 index页面地址  
```html
127.0.0.1/bootstrap_test/index.html
```


需要引入 css 文件夹的 bootstrap.css文件 

1、
```html
<link href="css/bootstrap.min.css" rel="stylesheet"> 
```
实际请求地址为：127.0.0.1/bootstrap_test/css/bootstrap.min.css 

2、
```html
<link href="./css/bootstrap.min.css" rel="stylesheet">  
```
实际请求地址为：127.0.0.1/bootstrap_test/css/bootstrap.min.css 

3、
```html
<link href="/css/bootstrap.min.css" rel="stylesheet">  
```
实际请求地址为：127.0.0.1/css/bootstrap.min.css 

4、
```html
<link href="../bootstrap_test/css/bootstrap.min.css" rel="stylesheet">  
```
实际请求地址为：127.0.0.1/bootstrap_test/css/bootstrap.min.css
