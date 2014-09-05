# 第一次gradle成功构建以及编译android stdio 项目

## 前言
一直对构建工具嗤之以鼻，或许因为之前收到好兄弟影响的缘故。把github上的Project的src跟res，jar包，以及配置文件等一个个复制过来导入ADT即可，但是即使这样也多次碰壁，因为有部分依赖找起来实在蛋疼，于是先前花了两天时间经过一番折腾，终于成功用gradle构建了一个AndroidStdio项目，在这里做个记录。

## 路径配置
### gradle路径配置
-  gradle路径的配置非常简单，下载gradle版本还是挺蛋疼的（墙的缘故）gradle版本传送门：[gradle官网][1]

-  路径：基本就是解压下来的目录，然后在环境变量里面新建一个gradle_home即可。我的gradle路径是：
    
    <img src="gradle_dir.jpg" alt="gradle路径图片" width="240">



### androidstdio路径配置


  [1]: http://www.gradle.org