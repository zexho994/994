# 关于 git 对象

git 的文件存储在/.git/object 里面找到.

整个文件系统可以分为3个部分,

- commit 对象: 每一次commit后都会生成一个commit对象
- tree 对象:就像Linux文件系统里面的文件夹
- Blob 对象: 快照,保存文件的数据

commit 对象和 tree对象是**一一对应**的,一个 Tree 关联着多个blog

![](http://mednoter.com/media/files/2014/jul/29-git.png)

###Commit 对象

commit对象保存着与它一一对应的tree的编号. 

parent 保存着上一次commit对象的编号,author和committer就是git config里面我们配置的个人信息.

然后最下面保存的就是 git commit -m 'xxx' 里的说明内容了

![](http://mednoter.com/media/files/2014/jul/29-object-commit.png)

### Tree对象

一个tree可以保存多个blob的编号和子tree的编号.

![](http://mednoter.com/media/files/2014/jul/29-object-tree.png)

###Blob对象

快照当然保存的就是该文件里面的内容了

![](http://mednoter.com/media/files/2014/jul/29-object-blob.png)



## 步骤分析

1. 首次提交,提交了一个简单的文件 a.txt `git commit -m 'Add a.txt'`

   这时候git就创建了一个commit对象(编号为e9178,对应的tree为782c5,说明内容也在里面); tree里面保存了 快照的地址

![](https://l.ruby-china.org/photo/2014/9c44291362d64765803afba65fa2a0a4.png)

2. 我们修改a.txt里面的内容,然后再次提交.新生成的commit对象编号aef54,parent指向了上次提交的commit对象

![](https://l.ruby-china.org/photo/2014/ba84d2ce8ba5066444a3e382ed644206.png)

![](https://l.ruby-china.org/photo/2014/1ab7f0d2ab24734f0af6fc2d8e7c7a7d.png)

![](https://l.ruby-china.org/photo/2014/8378188d524614d5b12bc27c42404a24.png)

![](https://l.ruby-china.org/photo/2014/8e555b42a9775d725bd95ee7f369af7c.png)

