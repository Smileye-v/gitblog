# [python爬虫读取ins照片问题总结](https://github.com/Smileye-v/gitblog/issues/15)

在运行[python爬虫项目](https://github.com/Smileye-v/python-crawling-instagram)时
![image](https://user-images.githubusercontent.com/68359161/226536075-b04662ba-d748-4156-81fd-60da84e435d0.png)
出现该报错时添加cookies
![image](https://user-images.githubusercontent.com/68359161/226536099-c01b4de8-c2c3-45e3-b241-60b2b87bf88c.png)
这是库ulllib3版本的错误。使用pip install urllib3==1.25.8，降低urllib3的版本 但安装时出现报错

```
ERROR: Could not find a version that satisfies the requirement urllib3
ERROR: No matching distribution found for urllib3
```

**解决方法**: 因为python国内网站网络不稳定的问题，于是使用镜像

`pip install 包的名字 -i http://pypi.doubanio.com/simple/ --trusted-host pypi.doubanio.com`
