[TOC]

# Git 安装配置

安装Git，默认安装流程/Git 各平台安装包下载地址为：http://git-scm.com/downloads

Git 提供了一个叫做 git config 的命令，用来配置或读取相应的工作环境变量。

这些变量可以存放在以下三个不同的地方：

-   `/etc/gitconfig` 文件：系统中对所有用户都普遍适用的配置。若使用 `git config` 时用 `--system` 选项，读写的就是这个文件。
-   `~/.gitconfig` 文件：用户目录下的配置文件只适用于该用户。若使用 `git config` 时用 `--global` 选项，读写的就是这个文件。
-   当前项目的 Git 目录中的配置文件（也就是工作目录中的 `.git/config` 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 `.git/config` 里的配置会覆盖 `/etc/gitconfig` 中的同名变量。

在 Windows 系统上，Git 会找寻用户主目录下的 .gitconfig 文件。主目录即 $HOME 变量指定的目录，一般都是 C:\Documents and Settings\$USER。

此外，Git 还会尝试找寻 /etc/gitconfig 文件，只不过看当初 Git 装在什么目录，就以此作为根目录来定位。

## 用户信息

配置个人的用户名称和电子邮件地址，这是为了在每次提交代码时记录提交者的信息：

```
git config --global user.name "chennuofeng"
git config --global user.email 1771015028@qq.com
```

如果用了 **--global** 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

## 文本编辑器

设置 Git 默认使用的文本编辑器,一般可能会是 Vi 或者 Vim，如果你有其他偏好，比如  VS Code 的话，可以重新设置：

```
git config --global core.editor "code --wait"
```

## 差异分析工具

还有一个比较常用的是，在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话：

```
git config --global merge.tool vimdiff
```

Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。

当然，你也可以指定使用自己开发的工具，具体怎么做可以参阅第七章。

## 查看配置信息

要检查已有的配置信息，可以使用 git config --list 命令：

```
$ git config --list
http.postbuffer=2M
user.name=runoob
user.email=test@runoob.com
```

有时候会看到重复的变量名，那就说明它们来自不同的配置文件（比如 /etc/gitconfig 和 ~/.gitconfig），不过最终 Git 实际采用的是最后一个。

这些配置我们也可以在 **~/.gitconfig** 或 **/etc/gitconfig** 看到，如下所示：

```
vim ~/.gitconfig 
```

显示内容如下所示：

```
[http]
    postBuffer = 2M
[user]
    name = runoob
    email = test@runoob.com
```

也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可，像这样：

```
$ git config user.name
runoob
```

## 生成 SSH 密钥（可选）

如果你需要通过 SSH 进行 Git 操作，可以生成 SSH 密钥并添加到你的 Git 托管服务（如 GitHub、GitLab 等）上。

```
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```

按提示完成生成过程，然后将生成的公钥添加到相应的平台。

## 验证安装

在终端或命令行中运行以下命令，确保 Git 已正确安装并配置：

```
git --version
git config --list
```

# Git 创建仓库

本章节我们将为大家介绍如何创建一个 Git 仓库。

你可以使用一个已经存在的目录作为 Git 仓库。

------

## git init

Git 使用 **git init** 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 **git init** 是使用 Git 的第一个命令。

在执行完成 **git init** 命令后，Git 仓库会生成一个 .git 目录，该目录包含了资源的所有元数据，其他的项目目录保持不变。

### 使用方法

进入你想要创建仓库的目录，或者先创建一个新的目录：

```
mkdir my-project
cd my-project
```

使用当前目录作为 Git 仓库，我们只需使它初始化。

```
git init
```

该命令执行完后会在当前目录生成一个 .git 目录。

使用我们指定目录作为Git仓库。

```
git init newrepo
```

初始化后，会在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：

```
$ git add *.c
$ git add README
$ git commit -m  "<日志内容 提交说明>"
```

以上命令将目录下以 .c 结尾及 README 文件提交到仓库中。

> 临时提交到本地git

git log 查看提交日志 

![image-20241009144923616](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241009144923616.png)

## git回退

git reset --hard <commit ID> 上图中有显示 （清空）

​				--soft

​				--mixed 两种模式

commit提交后增加分支，可进行分支合并等

## 分支branch （切换分支）

#创建分支

git branch 0.2

#查看分支

git branch -a 

#切换

git checkout 0.2

git checkout master

#合并

git merge 0.2 

# 修改remote

方式1、直接修改：

git remote set-url origin xxxxx.git

方式2、先删后加 ：

git remote rm origin
git remote add origin xxxxx.git

# git创建github创建初始化

git init 

​                   #如果有大于100M的文件，要先执行lfs 在下面

git add .

#先当前项目提交，并备注  当前分支内容变更后就要commit

git commit -m "内容备注"  

git branch -M main 主分支

#等于创建一个网盘，知道上传到哪里

git remote add origin <http 自己的仓库>      

git push -u origin <main分支名> 上传必须要commit一下

#拉取分支

git pull -u origin <分支>  再从新建分支，保证当前是最新的

## #参与别人的开源项目

github中拉取仓库，添加分支

git clone  <http>   .    #克隆仓库代码

git remote -v  查看仓库连接

git remote add upstream <htpp>别人的代码库

git checkout -b <分支名> 切换分支



```
git add .

gti commint -m "<>"

git push -u origin <分支>
```

# Git报错fatal: unable to access ’--‘ Recv failure Connection was res

个人比较推荐方法二。https://blog.csdn.net/2301_81265915/article/details/144092365

##### 方法一：取消代理设置

这是最常见的解决方法之一，通过在终端执行以下命令，可以取消 Git 的代理设置：

git config --global --unset http.proxy 
git config --global --unset https.proxy


注意：

输入的不仅仅是 git config --global --unset http.proxy 还有后面的http://127.0.0.1:7890。

##### 方法二：设置系统代理（推荐）

有时候取消代理设置仍然会出现报错，这时可以通过设置系统代理来解决。具体步骤如下：

1）打开系统设置，搜索代理设置，并点击编辑按钮。

2）在代理服务器中，将代理IP地址设置为127.0.0.1。端口设置为7890（这个端口不会影响正常上网，可以放心设置），然后点击保存。

关于下面的locall......无需在意。

3） 在终端输入以下命令，设置 Git 使用本地代理：

git config --global http.proxy http://127.0.0.1:7890
设置完成后，可以通过以下命令检验是否设置成功：

git config --global -l

##### 方法三：不挂梯子时

如果你把梯子关闭了，在拉取代码时报错：

 Failed to connect to 127.0.0.1 port 7890 after 2034 ms: Couldn't connect to server
主因是未连接到服务端，我们可以通过cmd查看是否使用代理：

git config --global http.proxy
如果存在代理，清除即可

git config --global --unset http.proxy

# Github上传大于50M的模型文件

二、自己的实际操作流程

下面是我的一个详细的步骤：

2.1 准备工作
在电脑中自选目录新建一个文件夹（例：F:\git文件夹\pretrained_ckpt）；
在GitHub上新建一个仓库（Repositories），GitHub有官方教程；
打开Git Bash，进入刚刚新建的文件夹：
cd /f/git文件夹

2.2 初始化仓库
git init

git init 是一个 Git 命令，用于在当前目录中初始化一个新的 Git 仓库。通过运行该命令，Git 会在当前目录下创建一个隐藏的 .git 文件夹，用于存储仓库的相关信息和版本控制的历史记录。

如果命令执行成功，你将看到一个类似于以下内容的输出：

Initialized empty Git repository in /path/to/your/repository/.git/


2.3 安装git lfs（一个仓库里面执行一次就好了）
git lfs install

git ls install 是 Git LFS（Large File Storage）的命令之一，用于在本地系统中安装 Git LFS 扩展。

下面是使用 git lfs install 安装 Git LFS 的步骤：

确保你已经在本地系统中安装了 Git。你可以在命令行终端中运行以下命令来验证是否安装了 Git：
git --version
如果已安装 Git，将显示 Git 的版本信息。如果未安装 Git，请按照适用于你操作系统的说明进行安装。

打开命令行终端，并进入要使用 Git LFS 的目录。

运行以下命令：

git lfs install

这将下载和安装 Git LFS 扩展，并将其配置为与 Git 一起使用。

如果安装成功，你将看到类似以下输出：
Updated git hooks.
Git LFS initialized.
这表示 Git LFS 已成功安装和初始化。

现在，你的系统已安装 Git LFS，并可以在 Git 仓库中使用 Git LFS 来管理大文件。你可以使用其他 Git LFS 命令来跟踪大文件、添加文件到 Git LFS 管理、推送和拉取文件等操作。请确保你的 Git 服务器和其他协作者也已正确配置和支持 Git LFS，以便顺利地使用 Git LFS 功能。

2.4 跟踪一下你要上传（push）的文件或指定文件类型
git lfs track "*.pth"

这将告诉 Git LFS 跟踪所有扩展名为 .pth 的文件，并使用 Git LFS 进行管理。

完成上述步骤后，Git LFS 将会跟踪并管理所有匹配 .pth 扩展名的文件。在提交、推送和拉取时，Git LFS 会相应地处理这些大文件，确保它们被正确地上传和下载。

2.5 添加.gitattributes
.gitattributes 是 Git 的一个配置文件，用于指定特定文件或文件类型的属性和处理方式。它可以用于定义 Git 在处理文件时的行为，例如在版本控制、合并和检出文件时的属性设置。

.gitattributes 文件的作用包括：

文件属性设置：你可以使用 .gitattributes 文件指定特定文件或文件类型的属性。例如，你可以定义某个文件应被视为二进制文件，或者使用 Git LFS 进行管理。
文本处理：.gitattributes 文件可以用于指定文本文件的行尾格式（如 CRLF 或 LF），这对于跨平台协作很有用。你可以设置文件的 text 或 binary 属性，控制 Git 是否将其视为文本文件。
合并策略：通过 .gitattributes 文件，你可以为不同类型的文件指定合并策略，以决定在合并分支时如何处理这些文件的冲突。
过滤和清理：.gitattributes 文件允许你配置 Git 过滤器，以在提交或检出文件时执行自定义的过滤和清理操作。这对于对文件进行自动处理、格式转换或敏感信息过滤很有用。
.gitattributes 文件的语法是基于模式匹配的，你可以使用通配符、正则表达式和文件路径模式来匹配文件，并为其指定相应的属性和操作。

请注意，.gitattributes 文件需要添加到 Git 仓库，并确保其他协作者在克隆或拉取仓库时能够正确应用这些属性规则。

在命令行终端中，使用 Git 命令将 .gitattributes 文件添加到仓库并提交：

git add .gitattributes


2.6 添加要上传（push）的文件并提交（commit）
git add .


git commit -m "RegionCLIP_pretrained_ckpt"


2.7 将本地与新建仓库进行配对
git remote add origin git@github.com:biluko/RegionCLIP_petrained_ckpt.git

2.8 让上传看起来更连续，而不是多出很多无用的merge commit
git pull --rebase origin master

git pull --rebase origin master 是一个 Git 命令，用于从远程仓库（通常是命名为 origin）拉取最新的提交，并通过变基（rebase）方式将本地的提交应用到更新后的远程分支上。

该命令的作用如下：

从远程仓库（origin）拉取最新的提交：git pull 首先会执行 git fetch，将远程仓库的最新提交下载到本地的远程跟踪分支（例如 origin/master）。
变基（rebase）本地提交：–rebase 参数告诉 Git 在将本地的提交应用到更新后的远程分支之前，先执行变基操作。变基会将当前分支的提交“重新播放”在远程分支的最新提交之上。
应用本地提交：在变基操作完成后，Git 会将本地的提交逐个应用到更新后的远程分支上。
使用 git pull --rebase origin master 命令的优势在于能够在提交历史中保持一条干净的线性历史。相比使用普通的 git pull 命令（默认使用合并方式），使用变基可以避免创建额外的合并提交，使得提交历史更加整洁。

然而，需要注意的是，当多个人同时在同一分支上工作时，使用变基操作可能会导致冲突。在进行变基操作前，请确保你的本地分支没有与远程分支冲突的提交，或者在变基后解决任何可能的冲突。

综上所述，git pull --rebase origin master 的作用是拉取远程分支的最新提交，并使用变基方式将本地提交应用到更新后的远程分支上。这有助于保持提交历史的整洁性。

2.9 正式上传
git push -u origin master


git push origin master


原文链接：https://blog.csdn.net/wzk4869/article/details/131661472

# 顶级细节教程

[git、github 保姆级教程入门，工作和协作必备技术，github提交pr - pull request_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1s3411g7PS/?spm_id_from=333.337.search-card.all.click)

## VScode 使用

修改环境变量    

![img](https://i-blog.csdnimg.cn/blog_migrate/296f7cebb61873ea675940c19c86ae96.png#pic_center)

![image-20241009150453011](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241009150453011.png)

修改vscode的路径配置

vscode终端内容修改，否则终端找不到git

![image-20241009150555415](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20241009150555415.png)







## git clone

我们使用 **git clone** 从现有 Git 仓库中拷贝项目（类似 **svn checkout**）。

克隆仓库的命令格式为：

```
git clone <repo>
```

如果我们需要克隆到指定的目录，可以使用以下命令格式：

```
git clone <repo> <directory>
```

**参数说明：**

- **repo:**Git 仓库。
- **directory:**本地目录。

比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：

```
$ git clone git://github.com/schacon/grit.git
```

执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。

如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：



```
$ git clone git://github.com/schacon/grit.git mygrit
```

## 配置

git 的设置使用 git config 命令。

显示当前的 git 配置信息：

```
$ git config --list
credential.helper=osxkeychain
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
```

编辑 git 配置文件:

```
$ git config -e    # 针对当前仓库 
```

或者：

```
$ git config -e --global   # 针对系统上所有仓库
```

设置提交代码时的用户信息：

```
$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com
```

如果去掉 **--global** 参数只对当前仓库有效。

