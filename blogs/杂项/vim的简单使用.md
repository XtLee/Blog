# vim的简单使用

> Vim是从 vi 发展出来的一个文本编辑器。代码补全、编译及错误跳转等方便编程的功能特别丰富，在程序员中被广泛使用，和Emacs并列成为类Unix系统用户最喜欢的文本编辑器。


### 我们今天就来说说如何快速上手，简单快捷的使用vim。
 

#### 在git bash中输入vim，进入vim编辑器。
![vim编辑器初始状态](http://upload-images.jianshu.io/upload_images/6885620-e0e11a255b45b2e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 输入“i”进入编辑模式
![编辑模式](http://upload-images.jianshu.io/upload_images/6885620-ac5f80dbbb6fa2d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### “esc”返回到命令模式
![命令模式](http://upload-images.jianshu.io/upload_images/6885620-c53d27e75ed868a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### “:wq”保存退出（“:q!”不保存强制退出）
![退出](http://upload-images.jianshu.io/upload_images/6885620-ebc8df90f13dc247.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 在vim中常用到的命令


1. 快速定位到当前段落的开头**“（”**或者**“{”**
2. 快速定位到当前段落的结尾**“）”**或者**“}”**
3. 复制 **“y”** ， 粘贴 **“p”**
4.  **“dd”** 删除当前行，并把删除的行放入剪切板
5. **HJKL** 或者 **↑↓←→** 上下左右移动光标  （**HJKL** 对应左 下 上 右 四个方向）
6. 光标移动到文档开头 **gg**，光标移动到最后一行开头 **shift+g**
7.  **“：help”** 显示相关命令帮助 （退出帮助 **“：q”** ）
8. 在命令模式中使用 **ctrl+b** 上翻页， **ctrl+f** 下翻页， **ctrl+u** 上翻半页， **ctrl+d** 下翻半页。
9. **“/ +需要查找的字符”** 显示文本中出现的第一个字符； **“ ？+需要查找的字符”** 显示文本中出现的最后一个字符。