# movieComentsSentimentAnalysis
电影评论情感分析
先记录一下，后续再传代码

之前做过酒店评论情感分析，那个数据集比较小，并且用的是sklearn和keras。
最近刚学完了tensorflow，想着重新找一个大一点的数据集来练练手~~~

首先：
拿到的数据是excel，是各个用户对不同电影做的评价和打分。做数据摘取，构建样本。


先用rnn试一试，用rnn最后输出的hstate，接一个softmax，learning_rate从0.0001 batch_size从64开始，根本不收敛，各种波动
看着每一个batch算出来的loss和accuracy一点规律都没有，我的内心是崩溃的。。。。
然后谷歌了下，为什么loss不降，有人说是初始化的问题，有人说是模型的问题。。。。

我只能凭着感觉，首先把learning_rate调大一点，然后batch_size也调大一点。。。
并且换成textCNN，终于慢慢开始收敛了。。。

然后再试着打印出进度。。。看起来也人模狗样的的。。。

但是，后来，从epoch0过度到epoch1的时候，都说我的数据没有对整齐。。。又一次崩溃ing。。。
把我破碎的玻璃心捡起来缝一缝，继续找bug。。。
发现是get_batch函数里面出的问题。这时候也遇到了几个问题。。。
1. numpy.int32 不能用于list的index
2. 每次get_batches的时候才把x数据补齐，但是经过一轮epoch之后，x_train数据已经被改变过了？
   根本原因是Python中对list的引用，修改引用，原数据也会被修改
   


先写到这里。。。要继续复习，为了明天的面试~~~~~
