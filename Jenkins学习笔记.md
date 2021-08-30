<center>JENKINS-STUDY<center>
​																																										by Koji

[toc]

#### 一、`jenkins`概念

##### 1、概念

​		Jenkins是一个开源的、可扩展的持续集成、交付、部署（软件/代码的编译、打包、部署）的基于web界面的平台。允许持续集成和持续交付项目，无论用的是什么平台，可以处理任何类型的构建或持续集成。

##### 2、`jenkins`的特性

（1）开源的`java`语言开发持续集成工具，支持CI，CD；

（2）易于安装部署配置：可通过yum安装,或下载war包以及通过docker容器等快速实现安装部署，可方便web界面配置管理；

（3）消息通知及测试报告：集成`RSS/E-mail`通过`RSS`发布构建结果或当构建完成时通过e-mail通知，生成`JUnit/TestNG`测试报告；

（4）分布式构建：支持`jenkins`能够让多台计算机一起构建/测试；

（5）文件识别:Jenkins能够跟踪哪次构建生成哪些jar，哪次构建使用哪个版本的jar等； 

（6）丰富的插件支持:支持扩展插件，你可以开发适合自己团队使用的工具，如`git`，`svn`，`maven`，`docker`等。



#### 二、Linux系统中安装`jenkins`

##### 1、安装条件

​		安装最低配置：不少于`256M`内存，不低于`1G`磁盘，`JDK`版本>=8（`openjdk`也可以）。

##### 2、安装Java环境，安装`jdk`

​		Java Development Kit（`JDK`）是太阳微系统针对Java开发人员发布的免费软件开发工具包。

（1）使用命令安装`java`

```shell
sudo yum -y install java
```

（2）查看`jdk`版本,`java`的版本要在8以上`jdk`为1.8时，Java的版本是8

```shell
java -version
```

##### 3、安装`wget`

```shell
sudo yum -y install wget
```

##### 4、下载并安装`jenkins`

（1）使用`wget`下载`jenkins`安装包，yum的`repo`中默认没有`jenkins`，需要先将`jenkins`存储库添加到yum `repos`

```shell
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
```

（2）导入key，此步不执行，无法进行下一步安装`jenkins`

```shell
 sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

（3）安装`jenkins`，默认安装最新的

```shell
sudo yum -y install jenkins
```



#### 三、启动`jenkins`

1、`VM`命令启动`jenkins`

```shell
service Jenkins start
```

2、设置虚拟机端口转发规则

​		将子系统端口设置为8080，主机端口设置为8000（可自定义），主机`IP` 为127.0.0.1

3、打开浏览器，访问`ip:8080`进行安装，`ip`为服务器`ip`

​		在浏览器上访问`127.0.0.1:8000`

4、安装默认插件后创建第一个`Admin`用户

​		用户名：`Matisyahu`

​		密码：`zhimi1995@@@`

4、实例配置

`jenkins` URL: http://127.0.0.1:8000/



#### 四、创建任务

##### 1、创建任务时的配置项

（1）General-基本配置

​		项目名字,描述,参数,禁用项目,并发构建,限制构建默认node等 。

（2）Source code management -源码管理

​		 代码库信息,支持Git,Subversion等 。

（3） Build Triggers -构建触发器

​		 周期性构建,`poll scm`,远程脚本触发构建,其他项目构建结束后触发等 。

（4） Build Environment -构建环境

​		 构建前删除workspace,向Console输出添加时间戳,设置构建名称,插入环境变量等 。

（5） Build -构建

​		 添加1个或者多个构建步骤 。

（6） Post-build Actions -构建后操作

​		 Artifact归档,邮件通知,发布单元测试报告,触发下游项目等 。



#### 五、创建job例子

##### 1、执行python脚本

（1）安装python脚本所需的插件

* 回到Jenkins初始界面，在左侧菜单栏找到 **Manage Jenkins**
* 进入系统管理界面后，点击 **`Manage Plugins`**
* 点击**可选插件**选项，在右上角搜索框搜索**`python plugin`**，点击安装即可
* 也可以下载安装包，在**高级**选项下根据提示安装

（2）创建一个python的job并配置

* 回到Jenkins初始界面，在左侧菜单栏找到**新建Item**
* 输入任务名称，构建一个**Freestyle Project**（自由风格的项目）

* 填写项目描述，在**构建**菜单下点击**Execute Python script**（安装`python plugin`后会有）

* 输入python脚本，点击**保存**

（3）构建job

* 回到主页，在主面板上找到新创建的项目，点击**立即构建**

（4）查看结果

* 构建完成后，进入项目，查看**控制台输出**

