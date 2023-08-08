# Win10快捷操作手册

## 1 Git配置

### 1.1 安装Git

windows下的配置更方便，直接到官网一键安装即可。
`git bash` 的安装（[可参考](https://www.cnblogs.com/xueweisuoyong/p/11914045.html)）：

官网：[Git (git-scm.com)](https://git-scm.com/)

下载最新版windows的安装程序，一路按Next即可。

### 1.2 Git配置

参考：[Windows 10 环境下安装配置Git并连接到GitHub](https://www.dusaiphoto.com/article/13/)

首先要配置的名字和Email地址，以后每次进行git操作时才能有据可查。打开Git Bash，输入：

```
git config --global user.name 'your_name'
git config --global user.email 'your_email'
```

接下来我们需要创建版本库（Repository），也就是代码的仓库。这个仓库中的文件Git会进行跟踪，以便日后的数据备份和还原。

随便找一个位置，创建一个文件夹git_repo作为版本库目录：

```
mkdir git_repo
```

输入cd git_repo进入刚创建文件夹的路径：

```
cd git_repo
```

再输入指令git init初始化Git，告诉Git这里是一个版本库了：

```
git init
Initialized empty Git repository in E:/django_project/git_repo/.git/
```

这样就建好了一个空的仓库了。

### 1.3 添加文件到Git库
在git_repo目录中创建一个test.txt，内容随意。

在bash中输入命令git add "file_name"告诉Git需要追踪的文件：

```
git add test.txt
```

再用命令git commit进行提交：

```
git commit -m "test git"
```

如果bash打印出下面的文本：

```
[master 5e04f34] test git
1 file changed, 1 insertion(+)
create mode 100644 test.txt
```

说明版本库已经顺利运行起来了。

### 1.4 Git库连接GitHub
创建SSH Key
首先还是打开Git Bash，创建SSH Key，用于Git和GitHub之间的SSH加密传输：

```
$ ssh-keygen -t rsa -C 'your_email'
```

回车后提示输入passphrase，类似于密码，每次于GitHub通信时都会要求输入。

passphrase也可以不用设置，一路回车就好。

```
$ ssh-keygen -t rsa -C 'yourname@email.com'
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/yourname/.ssh/id_rsa):
Created directory '/c/Users/yourname/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/yourname/.ssh/id_rsa
Your public key has been saved in /c/Users/yourname/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:ajd2oFsg7+hJEqiv0EDHDslRSvkozbgJj36Z9l/uUEM yourname@email.com
The key's randomart image is:
+---[RSA 3072]----+
| oo.             |
|o.=              |
| Xoo     E       |
|=o*.    .        |
|==... . So       |
|=o.. o +...      |
|+ o + =.=..      |
|.o B = =+o       |
|..+.=.+..o       |
+----[SHA256]-----+

```

完成后会在用户目录里生成.ssh目录，比如说我的在C:\Users\yourname\.ssh，里面包含id_rsa和id_rsa.pub两个文件。

接下来登录GitHub账号，在account/settings中找到SSH and GPG keys，点击NEW SSH key；其中的Title文本框请随便填，Key文本框填入id_rsa.pub中的内容。点击Add SSH key，就完成了SSH key 的添加。



### 1.5 连接GitHub（远程仓库和本地仓库的关联）

**首先创建版本库。**点击GitHub导航栏里的`New repository`：

在`Repository name`中输入库名称。这里因为是我的[Django搭建博客教程](http://www.dusaiphoto.com/article/article-detail/2/)的库，因此输入`django_blog_tutorial`。

写完后点击`Create repository`，远程版本库就生成了。

进入库的主页，点击SSH，后面的就是远程库的地址：

根据页面的提示，进入本地刚才创建的库目录`git_repo`，将本地的Git库和远程仓库关联起来：

```
git remote add origin git@github.com:stacklens/django_blog_tutorial.git
git push -u origin master
```

bash中打印出如下字符：

```
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 281 bytes | 140.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:stacklens/django_blog_tutorial.git
   848cc16..5e04f34  master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

则表示本地Git已经顺利连接上了GitHub远程仓库。

以后每次需要提交代码到GitHub时，**进入到git仓库文件夹，**执行下面的代码：

```
# 提交当前目录下所以文件
$ git add .

# 提交记录说明 
$ git commit -m "xxx"

# 提交到github
$ git push origin master
```

请尽情享用吧~

参考：[Git的使用--如何将本地项目上传到Github（三种简单、方便的方法）（二）（详解）-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1504684)

### 1.6 从远程库上进行克隆

在远程仓库新建项目，使用`git clone`命令克隆到本地进行开发。这时候本地就会出现一个和项目名称相同的文件夹，在文件夹下同样`.git`文件夹来记录版本信息，这时候`git`已经在本地帮我们建立好了一个仓库。因为我们是直接在`git`上克隆下来的，所有已经和远程的仓库建立了关联，我们可以直接进行代码的推送（这里就不用再像之前那样把本地仓和远程仓进行关联）。

```

$ git add *


$ git commit -m "88"
[main 7c70d75] 88
 1 file changed, 1 insertion(+)


$ git push origin
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 369 bytes | 369.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/yourname/hik_ros.git
   42d9361..7c70d75  main -> main
```





### 1.7 BUG



```
fatal: not a git repository (or any of the parent directories): .git
```

原因：没有git init

```
fatal: unable to access 'https://github.com/yourname/hik_ros.git/': Recv failure: C
onnection was reset
```

因为代理问题，多push几次就能成功






## 2 在blog文件夹下打开cmd

~~在win10下，直接在该文件夹下的地址栏输入`cmd`即可打开该路径的终端窗口~~

以上可用，但是`git bash`直接还原`linux`操作，更方便

## 3 更新博客

`hexo g`

## 4 本地预览

`hexo s`

## 5 在线更新

**.sh文件**，是shell script格式的，在Linux系统下是可以直接运行的，但是，由于C:\Windows\System32这里是没有bash.exe文件的，在Windows环境下，需要借助第三方软件。

在终端里面，【ctrl】+【insert】相当于复制，【shift】+【insert】相当于粘贴，在其他操作系统的终端一样试用，例如linux

快捷路径：`/c/Users/yourname/OneDrive/Git/yourname/blog`

在`git bash`终端下像`linux`那样正常操作出现如下错误

fatal: unable to access 'https://github.com/yourname/yourname.github.io.git/': OpenSSL SSL_read: Connection was reset, errno 10054

这是服务器的SSL证书没有经过第三方机构的签署，所以报错。
错误原因可能是网络不稳定，连接超时造成的，如果你试了多次还是报这个错误，建议你执行下面的命令

`git config --global http.sslVerify "false"`

然后继续正常操作即可

`bash deploy.sh`

或者 `bash push.sh`
