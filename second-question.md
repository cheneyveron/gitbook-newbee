前面讲了如何使用Git进行版本控制。一旦你掌握了Git的使用方法，拿到SVN你就会发现：这不是一样的吗？

如果是一个人开发，那第一节的内容大概就能满足你了。如果是多人一起开发，那就会出来第一个有点棘手的问题：冲突\(Conflict\)处理。

# 1. 解决冲突

第一节中的项目还在吧？

## 1.1 模拟第二个开发者

1. 打开Gitlab，进入Sample项目的Detail页面，找到它的SSH地址，形如：`git@gitlab.com:cheneyveron/sample.git`。
2. 在命令行下，创建一个新目录并进入，如`D:\conf`，把远端仓库克隆到新目录中：`git clone git@gitlab.com:cheneyveron/sample.git`。这条命令会创建一个仓库同名文件夹\(sample\)，初始化sample文件夹为Git仓库，将远程仓库master分支的Commits拉到这个文件夹中，并且将这个远端仓库添加为本地仓库的origin远端。你也可以手动创建新文件夹，用git init初始化，然后`git remote add origin git@gitlab.com:cheneyveron/sample.git`，最后`git pull`。
3. 进入sample目录，创建一个`a.txt`，内容为`hahaha`，添加这个文件`git add a.txt`，创建一个Commit`git commit -m "add a.txt"`，push到远端`git push -u origin master`。

使用`git log`或者在gitlab网站上都可以查看当前分支的Commit历史。此时的历史形如`... -> 8dbf45`

## 1.2 开发者1也开始开发了

1. 进入原来的项目，如`D:\phvis\car`
2. 拉取远端`git pull`
3. 将a.txt中的`hahaha`删掉，改成`phviscar`，然后添加此文件，创建Commit后push到远端.

此时Commit历史变成了`... -> 8dbf45 -> e23743`

## 1.3 开发者2继续开发

1. 进入`D:\conf\sample`，将`a.txt`中的`hahaha`删掉，改成`confsample`，然后添加此文件，创建Commit。

此时开发者2手中的Commit历史变成了`... -> 8dbf45 -> 88aec5`

此时如果推送到服务器上，会发现被Reject了，因为开发者2手中的Commit历史与网站上的Commit历史有**冲突\(Conflict\)**。

## 1.4 文明的解决方法

既然不让push到远端，我们就在本地解决冲突吧！下面是开发者2的身份：

1. 进入`D:\conf\sample`
2. 拉取远端仓库`git pull`
3. 可以看到git自动将冲突部分进行了合并。打开a.txt，会发现git动了我们的代码，如下：![](/assets/WX20171118-114754@2x.png)
4. 从`<<<<<<< HEAD`到`=======`是本地Commit`88aec5`的内容，而从`=======`到 `>>>>>>> e23743`则是远端Commit中的内容。
5. 所以我们选择性的保留某一部分，或者都保留，然后把Git添加的那些文本删掉，然后添加a.txt、Commit、push到远端即可。

## 1.5 暴力的解决方法

如果你不想要他的改动，想直接用本地的仓库覆盖远程仓库的话，那就强行推送吧：

`git push -u origin master -f`

不过，这样估计开发者1要哭了:\(

