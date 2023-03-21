# [Java mousedragged事件时控件闪烁](https://github.com/Smileye-v/gitblog/issues/9)

在使用Java Swing做程序时，使用MouseMotionListener的mousedragged鼠标事件，但拖动时，元素位置闪烁变化。
![image](https://user-images.githubusercontent.com/68359161/226532997-45f88329-74f7-4ac4-a409-8576b51abbf1.png)
输出了位置数值查看发现位置会往左上角“瞬移”。
```
import java.awt.event.MouseMotionListener;
public void mouseDragged(MouseEvent e) {
//鼠标拖动
    // TODO Auto-generated method stub
    panel_lable.setLocation(e.getX(),e.getY());//面板位置随鼠标拖动变化
    System.out.println(e.getX()+","+e.getY());
}
```
### 解决方法
因为我用的是awt的组件,需要使用双缓冲来避免画面的抖动。修改后的代码如下：
```
public void mouseDragged(MouseEvent e) {
//鼠标拖动
    // TODO Auto-generated method stub
    panel_lable.setLocation(e.getX()+(int)panel_lable.getLocation().getX(),e.getY()+(int)panel_lable.getLocation().getY());//面板位置随鼠标拖动变化
    System.out.println(e.getX()+","+e.getY());
}
```
修改后抖动的问题就没有了。