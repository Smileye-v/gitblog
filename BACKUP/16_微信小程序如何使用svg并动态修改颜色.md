# [微信小程序如何使用svg并动态修改颜色](https://github.com/Smileye-v/gitblog/issues/16)

微信小程序并不支持直接使用svg标签，但是其image标签src支持base64
因此我们可以将svg转化为image支持的base64格式代码，每次需要动态修改时都需要将修改后的svg转为base64格式代码再重新赋值，从而实现动态样式转化
示例：
https://juejin.cn/post/7115607195082358821