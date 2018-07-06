* 在模板文件html文件中如果有中文字符，默认的setting.py文件中的设置在渲染的时候会报错UnicodeDecodeError
* 在setting.py文件中设置两个默认参数：
```python
FILE_CHARSET = 'gb18030'
DEFAULT_CHARSET = 'utf-8'
```
