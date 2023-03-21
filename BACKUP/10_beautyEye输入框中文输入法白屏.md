# [beautyEye输入框中文输入法白屏](https://github.com/Smileye-v/gitblog/issues/10)

在使用Java Swing编写程序时引用beautyEye以修改样式，但在使用输入框时，输入中文窗口就出现白屏。
![image](https://user-images.githubusercontent.com/68359161/226533454-3ccf4247-1a5e-4fec-b108-f1731def2b0f.png)
![image](https://user-images.githubusercontent.com/68359161/226533485-7bdbffbe-fb7e-410b-a1aa-a779d360eb10.png)

### 解决方法
在初始化前加入System.setProperty(“sun.java2d.noddraw”, “true”);
```
public static void main(String[] args) {
		
		try {
			System.setProperty("sun.java2d.noddraw", "true");
			org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper.launchBeautyEyeLNF();
			
		} catch (Exception e) {
			// TODO exception
		}
		
	}
```
