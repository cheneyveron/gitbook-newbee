# 1. 域名的诞生

假如在阿里云买了个服务器，互联网这么大，如何寻找到这台服务器呢？聪明的先人发明了一套tcp/ip协议用于确定某台主机的**地址**，叫做**IP地址**。最开始的时候要访问网站、聊天室等，都是直接用IP地址。

但是ip地址不好记啊，于是就衍生出了**域名**。简单来说，域名可以代替ip，来“指向”服务器的地址。

## 1.1 什么是域名呢？

先从`网址(URL)`说起，比如`https://cheneyveron.gitbooks.io/newbee/`：

- `https://`叫做`协议(Protocal)`
- `cheneyveron.gitbooks.io`叫做`域名(Domain)`
- `/newbee/`叫做`路径(Path)`

例如，`baidu.com`、`image.baidu.com`、`a.image.baidu.com`都叫做域名。

另，域名不区分大小写。

# 2. 域名的分类

## 2.1 顶级域名、二级域名、子域名

简单来说，各级域名之间用`.`分隔，顶级域名就是倒数第一的那个，以此类推。

例如，`image.baidu.com`中 ，`.com`是顶级域，`baidu`是二级域，`image`是三级域。

`baidu.com`是`.com`的子域名。`image.baidu.com`和`map.baidu.com`都是`baidu.com`的子域名。

## 2.2 通用顶级域名

常见的通用顶级域名有：

- `.com`：商业
- `.net`：网络
- `.org`：组织
- `.info`：信息
- 新通用顶级域名，如`.biz`、`.site`、`.win`等。

通用顶级域名的**域名管理机构**往往是国际中立的组织或者商业公司。

## 2.3 国别顶级域名

- `.cn`：中国国家域名
- `.us`：美国
- `.uk`：英国
- `.it`：意大利
- ...

这些域名的**域名管理机构**往往是某个国家的信息部门。所以可能会有一些奇葩的规定，比如：

- 所有`.cn`的域名都需要提交一份“实名认证信息”。
- 只有`.co.uk`、`.me.uk`、`.org.uk`的所有者才能注册新的`.uk`域名。

# 3. 域名的注册

注册域名之前，需要先找一个**域名注册商**。

**顶级域名注册商**会向**域名管理机构**申请某域名的注册权限。还有一些“二道贩子”实际上是**顶级域名注册商**的代理，一般不要去小网站上注册域名，一旦跑路了要拿回域名就会很麻烦。

因为我国的政策原因，这里把国内和国外域名注册商分开讲。

## 3.1 国外域名注册商

每个域名在注册时候都要登记一些信息，这个信息被称作**Whois信息**。一般有注册人、邮箱、电话、地址。

这个信息不需要核对真伪，全网可查，并且注册商可以选择把它隐藏起来。官方查询地址就是[who.is](https://who.is)。万网也提供了一个[接口](https://whois.aliyun.com)。

常见的（我用过的）域名注册机构有：[Godaddy](https://www.godaddy.com)、[Name.com](https://name.com)、[NameCheap](https://www.namecheap.com)(荐)、[NameSilo](https://www.namesilo.com)(荐)、[register.io](https://register.io)等。

在它们上面注册大多数域名，只需要填写whois信息即可。注册完成就能使用。如果域名管理机构有额外要求的，则还需要多填写一些信息。比如`.cn`在哪里注册都是需要**实名认证**的。

## 3.1 国内域名注册商

如：[万网](http://wanwang.aliyun.com)、[西部数码](https://www.west.cn)、[新网](http://www.xinnet.com)等。

根据政策，**所有**国内注册商中注册的域名，除了要填写Whois信息之外，还要在注册完成后进行**实名认证**。

# 4. 域名的备案

简而言之，不管在哪注册的域名，只要域名指向的服务器在**中国大陆**，就必须备案才能通过域名访问服务器。

所以，下列情况下都是**不需要**备案的：

- 服务器不在中国大陆。比如在香港、台湾、日本、美国、新加坡、韩国。
- 直接用IP访问服务器，不使用域名。


当然了，备案的前提是你得有个注册好的域名。

# 5. 总结

所以，下面总结一下不同情况下注册一个域名需要填写的信息：

- Whois信息：所有域名。
- 实名认证信息：使用国内注册商。或者所有注册商注册`.cn`域名。
- 备案信息：域名注册完毕后，需要指向国内服务器。