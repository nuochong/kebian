# 可变分区式存储管理程序演示截图

> 推荐使用火狐、谷歌、safri、opera 等浏览器查看，IE9 以下没有效果，完整版请使用 IE9+浏览器打开。

1. 申请一个大小为 20 的空间
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/11.png)

2. 继续申请三个大小都为 20 的空间，然后申请两个为 10 的空间，提示剩余空间不能分配。
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/22.png)
3. 释放编号为 2 的空间
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/33.png)
4. 继续释放编号为 2 的空闲空间，因为本来就是空闲空间，所以不能释放，将提示此编号名无效！
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/44.png)
5. 释放编号为 0 的作业后继续释放编号为 1 的作业，可以看到空间合并。
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/55.png)
   ![An image](https://raw.githubusercontent.com/nuochong/kebian/master/img/66.png)

释放可以使用鼠标点击左边红色占用块自动添加编号。
