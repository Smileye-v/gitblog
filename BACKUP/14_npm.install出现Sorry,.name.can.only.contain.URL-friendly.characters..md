# [npm install出现Sorry, name can only contain URL-friendly characters.](https://github.com/Smileye-v/gitblog/issues/14)

在前端项目里安装安装 gulp的时候，出现了如下“Sorry, name can only contain URL-friendly characters.“
![image](https://user-images.githubusercontent.com/68359161/226535684-2af57f96-5e8e-46ad-a7ec-00735613d7ca.png)
这是因为在npm初始化的时候，会向我们询问项目名，如果我们不命名回车跳过的话，它会指定你的文件件的名称当做项目名。但是我的项目名称是不规范的有了两个-，所以需要重新npm install gulp –save-dev一下，在询问项目名的时候定义一下，比如说police。然后其他的信息可以先不填后期填。
![image](https://user-images.githubusercontent.com/68359161/226535710-18fd1ed3-0020-42ef-9b0e-61575371afb2.png)
![image](https://user-images.githubusercontent.com/68359161/226535720-db7f1e66-6875-43ac-b421-8147dc18a323.png)
最后确认