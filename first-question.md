在开发软件之前我们要做什么呢？答案是建立一个版本控制系统。这东西不是凭空冒出来的，而是无数项目惨痛教训的结晶。

# 一、没有版本控制之前

设想这么一个场景，A、B和C共同开发一个项目。

第一天，A创建了a.py，并写了一些东西。

第二天，B创建了b.py，并改了一些a.py中的东西。A也改了一些a.py中的东西。这天结束了以后，B和A就凑到一起商量着合并彼此的代码，商量了好几个小时才合并完。

第三天，C改了b.py、a.py，B也改了b.py，A也改了b.py。他们仨商量了更久。

...

一星期后，b.py出了点问题，谁也不知道第几天、谁写的代码有问题了。

版本控制系统就是为了防止这种情况出现而生的。它的唯一作用就是记录的代码变更历史。然后在需要的时候我们查看过去某个时刻的代码和代码说明，并进行回滚/合并等操作。

# 二、使用图形界面的Github客户端

Github做了一个图形界面的客户端，能形象的展示版本记录的过程，但是它有一些bug，所以你借助它理解了版本记录这个东西以后，最好还是用命令行进行各种操作。

注1：这个客户端是Github专用的，所以不能用于`Gitlab`或者`码云`。`SourceTree`是一个通用的Git客户端，但是它操作起来比较复杂，而且Windows客户端性能存在严重问题。

注2：我更推荐使用命令行使用git。对于一些稍微复杂一些的操作图形界面就无能为力了，比如

1. 重置Commit内容
2. 或者删掉历史Commit
3. 从所有Commit中删除某个文件

## 1. 安装

到[这里](https://central.github.com/deployments/desktop/desktop/latest/win32)去下载。

最好用爱国工具，不然网速可能会很慢。安装后登录你的Github账号。

## 2. 创建一个新仓库\(Create a new Repository\)

输入仓库名，描述，选择仓库位置，点击创建即可。Git中的仓库\(Repository\)可以理解成项目。一旦创建了Git仓库，Git就会在后台默默的监控这个文件夹中的文件变更。

创建完以后就是下面的界面了，不要恐慌，现在可以最小化这个窗口了：![](/assets/WX20171108-195716@2x.png)

## 3. 写代码

注意，Git不是用来写代码的。所以你选择一个自己喜爱的编程工具写代码即可，如Notepad++、Visual Studio Code、Sublime text。

## 4. 提交代码

写了一个小版本，或者完成了一个组件以后，记得记录下现阶段的工作，相当于给代码拍个快照，然后加一个说明。

回到Github客户端，可以看到已经检测到了文件变更，选中需要git来追踪的文件，下面输入变更说明，然后点Commit to master即可：![](/assets/WX20171108-200541@2x.png)在这里，Github客户端帮我们做了两件事：1. 添加了需要监控的文件， 2. 创建了一个版本\(Commit\)。

随着我们不断的写代码提交，可以在History中看到我们的项目的一点点的进展。点击每个版本\(Commit\)可以看到提交的详情，右击某个Commit选择回滚\(Revert\)就可以撤销这个Commit所做的更改。

## 5. 发布到Github

即使不上传到Github，本地使用Git也能很好的帮助我们进行版本控制。

不过，一旦发布到github上面以后别人也可以看到这个项目了。发布很简单，点击Publish Repository即可。发布后，打开github.com并登陆就可以看到自己的新项目。

注意，Github网站只是浏览版本和代码用的，写代码的工作还在本地，并且需要咱们手动Publish到github上以后才能出现改动。

# 二、命令行下使用版本控制

别担心，命令行下也很简单。只要熟悉了Git的工作流程,你就会发现图形界面完全是可有可无的东西。

## 1. 安装git

Windows用户：到[这里](https://git-scm.com/download/win)去下载并安装。

Linux/macOS用户：都用Linux/Mac了，不用我教了吧？

## 2. 初始化新仓库\(Repository\)

安装好以后，我们新建一个文件夹，假如是在`D:\phvis\car`。然后运行`命令提示符CMD`或者`Power Shell`，使用下面的命令进入这个文件夹：

`D:`

`cd D:\phvis\car`

初始化一个新仓库：

`git init`

这样子就是在告诉git，现在开始监控`D:\phvis\car`这个文件夹吧。

## 3. 写代码

这一步就和git无关了，用你喜欢的工具，如Notepad++、Visual Studio Code、Sublime text在D:\phvis\car中写代码吧。

## 4. 记录变更

写好初始版本，或者某个小模块以后，打开命令行，进入这个仓库，然后使用下面的命令查看当前的仓库状态：

`git status`

会看到有许多红色的文件，状态是untracked，也就是git未追踪这些文件。

现在我们告诉git将哪些文件添加到这个版本中进行追踪：

`git add .`

如果你不想记录所有的文件，可以将`.`替换成`文件的路径`，也可以使用通配符，如`src/*.py`

现在再用`git status`查看一下仓库状态，就会看到那些文件变成了绿色的，等待`提交\(commit\)`的状态。

我都告诉git添加哪些文件了，为什么还要我再提交一下呢？设想一下如果不加一些说明的话，一星期以后谁知道这个版本都干了啥呢？所以还需要一个简单的版本说明：

`git commit -m "完成了初稿，功能1、2、3"`

这样子git就会记住当下的文件状态了，保存成一个commit。

## 5. 同步远端仓库

这个仓库不一定在Github/Gitlab上面，只要运行着Git服务端即可。这里用Gitlab为例。

### 5.1 创建远程仓库

直接用Github账号即可登录Gitlab，然后点击右上角的`加号` -&gt;`New Project`：

![](/assets/WX20171117-171649@2x.png)

输入项目名称和描述，点击创建即可。

注意：一些网站\(比如Github\)可能会问你是否要替你创建README和LICENSE文件，请勿选择。因为它实际上是拷贝了两个文件，然后给你自动创建了第一个Commit。这样子就会和你自己本地项目的第一个Commit发生冲突\(Conflict\)。冲突不难解决，不过最好避免一开始就遇到这种麻烦事儿。

### 5.2 本地仓库关联远程仓库

创建完成远程仓库后，进入Detail页面，可以看到仓库的地址，形如：`https://gitlab.com/cheneyveron/sample.git`，或者`git@gitlab.com:cheneyveron/sample.git`。

仔细看上面的地址，就会发现一个是HTTPS链接，一个是SSH链接，这两种方式都可以访问这个仓库。

* 使用HTTPS链接访问，需要gitlab.com的登录用户名和密码来认证。
* 使用SSH链接，则可以使用RSA-256公私钥密钥认证。推荐使用SSH链接，安全性高，并且后续提交push拉取pull不需要再输入密码。

公私钥认证简介：公钥加密后的内容只有对应私钥能解开，私钥加密后的内容只有对应公钥能解开。私钥在我们自己手里，公钥在服务器上，两者互相配对。配对后续所有加密内容均由公私钥加密后再发送，因此可保证安全。

1. 生成SSH密钥。下载PuTTY（[32位](https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.70-installer.msi)）（[64位](https://the.earth.li/~sgtatham/putty/latest/w64/putty-64bit-0.70-installer.msi)）这个小软件，安装
2. 开始-&gt;PuTTY-&gt;PuTTYgen，下面的`Parameters`中，Type选择`RSA`，Number of bits填写`2048`，点击中间的Generate，如下图：![](/assets/Jietu20171117-212108.jpg)
3. 然后鼠标在上方空白区域胡乱移动造一些随机数， 直到生成完毕。
4. 保存OpenSSH格式的私钥：点`Conversions`-&gt;`Export OpenSSH Key`，务必保存为`C:\用户\[用户名]\.ssh\id_rsa`文件，如果不存在`C:\用户\[用户名]\.ssh`文件夹就手动创建。在Linux/Mac下，这个目录是`~\.ssh`，所有的SSH会话都默认用这个文件来认证。
5. 保存公钥：不要点击`Save public key`，直接全选，复制上面的框中的密钥，用纯文本编辑器（比如记事本、Notepad++）保存为文本文件，建议文件名`id_rsa.pub`。
6. 打开Gitlab，点击右上角的头像-&gt;`Settings`-&gt;`SSH Keys`，将刚才复制的密钥整个的粘贴到Key部分，然后点`Add key`。

至此，就完成了密钥的添加。

1. 进入本地仓库中：`cd D:\phvis\car`
2. 关联远端仓库，命名为origin：`git remote add origin git@gitlab.com:cheneyveron/sample.git`
3. 写代码 -&gt; add 写好的文件 -&gt; commit 这些文件
4. 有了一些commit以后，推送到远程仓库origin中的master分支：`git push -u origin master`
5. 到网页上刷新，见证奇迹：）



