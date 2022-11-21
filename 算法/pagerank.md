## pagerank简介
PageRank算法的基本想法是在有向图上定义一个随机游走模型，即一阶马尔可夫链，描述随机游走者沿着有向图随机访问各个结点的行为。在一定条件下，极限情况访问每个结点的概率收敛到平稳分布，这时各个结点的平稳概率值就是其PageRank值，表示结点的重要度。PageRank 是递归定义的，PageRank 的计算可以通过迭代算法进行。


入链数：指向该节点的链接数
出链数：由该节点指出的链接数
以上图为例：A的入链数为1，出链数为3，所以将由A指向其他节点的边权重设置为1/3，表示A访问B、C、D节点的概率均为1/3

两个重要假设
数量假设:在Web图模型中，如果一个页面节点接收到的其他网页指向的入链数量越多，那么这个页面越重要。
质量假设:指向页面A的入链质量不同，质量高的页面会通过链接向其他页面传递更多的权重。所以越是质量高的页面指向页面A，则页面A越重要。


![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/6387e09ea1f3cca3c452442a413c41f9.png)

三个页面A、B、C

  

为了便于计算，我们假设每个页面的PR初始值为1，d为0.5。

  

-   页面A的PR值计算如下：
    

![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/7841aa10c2753cfa4c91ad92cb2d7cc7.png)

-   页面B的PR值计算如下：
    

![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/15e7cc211db866fe646df04c1ede000d.png)

-   页面C的PR值计算如下：
    

![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/d445a630ed43a6bb342f1f93550c4d20.png)

  

下面是迭代计算12轮之后，各个页面的PR值：

  

  

![640?wx_fmt=png](https://img-blog.csdnimg.cn/img_convert/500afb6b8d5e4880a6006161a5035d1b.png)

  

那么什么时候，迭代结束哪？一般要设置收敛条件：比如上次迭代结果与本次迭代结果小于某个误差，我们结束程序运行；比如还可以设置最大循环次数。




## 参考链接
https://blog.csdn.net/leadai/article/details/81230557?spm=1001.2101.3001.6650.7&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-81230557-blog-124208393.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-7-81230557-blog-124208393.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=8