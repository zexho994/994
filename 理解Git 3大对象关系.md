在刚开始学习git的时候，我很疑惑git可以同时管理这么多分支，而且切换分支都是瞬间完成。尽管Git官方推荐我们多使用分支去开发，但是天真的我很担心分支太多，导致文件数量会剧增，所以一直不敢使用太多分支。

直到有一天想要去揭开心中的疑惑，git是怎么样管理这些不同分支的，最后发现和git里面的3个对象有关，搞懂3个对象的关系，相信在以后使用git命令的时候，头脑里会自然而然的浮现这些对象的关系网图。

- ==Commit对象==

 	 在命令行中，可以使用 git cat-file -p  <object id> 去查看每个对象里面的内容。
	
	由3部分组成，parent存储父commit对象的ID，每一个commit对象都一个ID，使用`git log`可以查看。Tree部分存储一个Tree对象的ID，下面部分存储的就是`git commit -m "xxx"`里面的注释内容了。

###### <img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gau1bdlvotj30cs09at8v.jpg" alt="image-20200112200749581" style="zoom:50%;" />

- ==Tree 对象==

	可以把Tree对象理解为一个文件夹，每一个commit对象对应一个Tree，可以把这个Tree当作根目录。这个Tree里面存储了根目录下的子Tree的ID，以及BlobId。

- ==Blob 对象==

	一个Tree对应一个文件夹，Blob对应的是文件，Blog里面存储的也真的是文件的内容。

#### 举个🌰

###### <img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gau1ob6y9nj30jk0d4jro.jpg" alt="image-20200112202046245" style="zoom:50%;" />

git的根目录是Java，Java文件夹里有一个test.class文件和一个JDK文件夹，JDK文件夹下面还有一个java8.class文件，那么我们第一次`git commit`后的关系图就是这样

###### <img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gau1uvyaxnj316c0dwq46.jpg" alt="image-20200112202700139" style="zoom: 25%;" />



此时我们修改了test.class文件的内容后，重新`git add test.class`再`git commit -m'update'`，这时候就会产生一个新的commit对象，结构就像这样:

###### <img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gau2693hdaj31g60qwq6s.jpg" alt="image-20200112203735217" style="zoom:25%;" />

发现只是保存了一个新的test.class的快照，java8.class没有发生改变，就没有生成生成新的快照。这样看来，真的是很节省磁盘了。

git还有许许多多的使用场景，如果你能理解以上的关系，那么其他的情况下，都是一样的，不妨自己去命令行 `git cat-file -p <object id>` 验证验证吧～



### <img src="https://s2.ax1x.com/2020/01/11/l5minI.png" alt="目录" style="zoom:65%;" />推荐阅读

[理解git对象](https://ruby-china.org/topics/20723)
