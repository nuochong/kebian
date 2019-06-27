# 可变分区式存储管理

## [Variable-partitioned-storage-management]

> 推荐使用火狐、谷歌、safri、opera 等浏览器查看，IE9 以下没有效果，完整版请使用 IE9+浏览器打开。

可变分区 存储管理 不是预先把内存中的用户区域划分成若干固定分区，而是在作业要求装入内存时，根据用户作业的大小和当时内存空间使用情况决定是否为该作业分配一个分区。因此分区大小不是预先固定的，而是按作业需求量来划分的；分区的个数和位置也不是预先确定的。它有效地克服了固定分区方式中，由于分区内部剩余内存空置造成浪费的问题。

## 存储管理

**基本思想**  
在作业要求装入内存时，若当时内存中有足够的存储空间满足该作业的需求，那就划分出一个与作业相对地址空间同样大小的分区分配给它使用。

**内、外部碎片**

| 内部碎片                                                   | 外部碎片                                                             |
| :--------------------------------------------------------- | :------------------------------------------------------------------- |
| 存储管理中，把分配给了用户而用户未用的存储区称为“内部碎片” | 存储管理中，把那些无法分配出去满足作业存储请求的空闲区称为“外部碎片” |

## 空闲区的合并

**前后相邻接分区的四种关系**

-   释放分区的前、后邻接分区都是已分配区，没有合并的问题存在。
-   释放分区的前邻接分区是空闲区，后邻接分区是已分配区。释放区应该和前邻接的空闲区合并成一个新的空闲区。
-   释放区的前邻接分区是已分配区，后邻接分区是空闲区。因此，释放分区应该和后邻接的空闲区合并成一个新的空闲区。
-   释放区的前、后邻接分区都是空闲区。因此，释放区应该和前、后两个邻接的空闲区合并成一个新的空闲区。

**空闲分区合并的时机**

-   一是调度到某作业时，若系统的每个空闲区尺寸都小于它的需要，但空闲区总存储量大于它的存储请求，于是进行空闲区合并，得到一个大的空闲区，满足该作业的需要。
-   一是只要有作业运行完归还所占用的存储区，系统就进行空闲区的合并。

## 程序模拟操作步骤

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
