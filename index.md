我的学习笔记

一 Git 相关

1.常用git config命令

    Config file location
        --global              use global config file
        --system              use system config file
        --local               use repository config file
        --worktree            use per-worktree config file
        -f, --file <file>     use given config file
        --blob <blob-id>      read config from given blob object
    
    Action
        --get                 get value: name [value-pattern]
        --get-all             get all values: key [value-pattern]
        --get-regexp          get values for regexp: name-regex [value-pattern]
        --get-urlmatch        get value specific for the URL: section[.var] URL
        --replace-all         replace all matching variables: name value [value-pattern]
        --add                 add a new variable: name value
        --unset               remove a variable: name [value-pattern]
        --unset-all           remove all matches: name [value-pattern]
        --rename-section      rename section: old-name new-name
        --remove-section      remove a section: name
        -l, --list            list all
        --fixed-value         use string equality when comparing values to 'value-pattern'
        -e, --edit            open an editor
        --get-color           find the color configured: slot [default]
        --get-colorbool       find the color setting: slot [stdout-is-tty]
    
    Type
        -t, --type <>         value is given this type
        --bool                value is "true" or "false"
        --int                 value is decimal number
        --bool-or-int         value is --bool or --int
        --bool-or-str         value is --bool or string
        --path                value is a path (file or directory name)
        --expiry-date         value is an expiry date
    
    Other
        -z, --null            terminate values with NUL byte
        --name-only           show variable names only
        --includes            respect include directives on lookup
        --show-origin         show origin of config (file, standard input, blob, command line)
        --show-scope          show scope of config (worktree, 



2.Github国内加速克隆及下载

cnpmjs.org

https://github.com.cnpmjs.org/

克隆加速

    git clone https://github.com/kubernetes/kubernetes.git
    
    #改为
    git clone https://github.com.cnpmjs.org/kubernetes/kubernetes.git
    
    #或者
    git clone https://hub.fastgit.org/kubernetes/kubernetes.git
    
    #或者
    git clone https://gitclone.com/github.com/kubernetes/kubernetes.git



3.Git 仓库基础操作

3.1仓库基本管理

初始化一个Git仓库(以/home/gitee/test文件夹为例)

    $ cd /home/gitee/test    #进入git文件夹
    $ git init               #初始化一个Git仓库

将文件添加到Git的暂存区

    $ git add "readme.txt" 

注：使用git add -A或git add . 可以提交当前仓库的所有改动。

查看仓库当前文件提交状态（A：提交成功；AM：文件在添加到缓存之后又有改动）

    $ git status -s

从Git的暂存区提交版本到仓库，参数-m后为当次提交的备注信息

    $ git commit -m "1.0.0"

将本地的Git仓库信息推送上传到服务器

    $ git push https://gitee.com/***/test.git

查看git提交的日志

    $ git log

3.2远程仓库管理

修改仓库名

一般来讲，默认情况下，在执行clone或者其他操作时，仓库名都是 origin 如果说我们想给他改改名字，比如我不喜欢origin这个名字，想改为 oschina 那么就要在仓库目录下执行命令:

    git remote rename origin oschina

这样 你的远程仓库名字就改成了oschina，同样，以后推送时执行的命令就不再是git push origin master 而是 git push oschina master 拉取也是一样的

添加一个仓库

在不执行克隆操作时，如果想将一个远程仓库添加到本地的仓库中，可以执行

    git remote add origin  仓库地址

注意: 1.origin是你的仓库的别名 可以随便改，但请务必不要与已有的仓库别名冲突 2. 仓库地址一般来讲支持 http/https/ssh/git协议，其他协议地址请勿添加

查看当前仓库对应的远程仓库地址

    git remote -v

这条命令能显示你当前仓库中已经添加了的仓库名和对应的仓库地址，通常来讲，会有两条一模一样的记录，分别是fetch和push，其中fetch是用来从远程同步 push是用来推送到远程

修改仓库对应的远程仓库地址

    git remote set-url origin 仓库地址

3.3自我总结

用户信息配置

    $ git config --global user.name "Tobin Gao"		#配置用户名称
    $ git config --global user.email 1046978455@qq.com		#配置电子邮件地址
    $ git config --global core.editor emacs		#配置用户名称文本编辑器为emacs
    $ git config --list		#检查已有的配置信息

创建SSH Key

SSH公钥可以让你在你的电脑和 Gitee 通讯的时候使用安全连接（Git的Remote要使用SSH地址）

    $ ssh-keygen -t rsa -C "1046978455@qq.com"

上传步骤

    $ git add .    #添加文件
    $ git commit -m "提示消息"    #提交
    $ git push origin master    #推送远程
    $ git remote add origin git@gitee.com:caifugao110/obarabackups.git
    #第一次提交设置添加远程库
    $ git push -u origin master
    #第一次把本地库的所有内容推送到远程库上,由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样.



git clone 指定分支

    git clone -b 分支名仓库地址
    #示例克隆远程仓库的main分支
    $ git clone -b main https://gitee.com/caifugao110/mygitdemo.git

切换本地分支

    #本地默认的main分支切回master分支
    Administrator@PC-GAOJIAN MINGW64 /e/git/obarabackups (main)
    $ git checkout -b master
    Switched to a new branch 'master'

3.4常见错误分析

fatal: not a git repository (or any of the parent directories): .git

这是由于本地版本管理仓库被删除了，需要重新初始化仓库：git init

    $ git init
    Initialized empty Git repository in E:/git/obarabackups/.git/
    #初始化仓库成功

fatal: The current branch master has no upstream branch.To push the current branch and set the remote as upstream,use......

初始push未添加远程,使用以下命令添加

    $ git remote add origin git@gitee.com:caifugao110/obarabackups.git
    #添加远程

! [rejected]        master -> master (fetch first)error: failed to push some refs to '......'

出现这个问题是因为github中的README.md文件不在本地代码目录中，可以通过如下命令进行代码合并

    $ git pull --rebase origin master
    From gitee.com:caifugao110/obarabackups
     * branch            master     -> FETCH_HEAD
     * [new branch]      master     -> origin/master
    Successfully rebased and updated refs/heads/master.
    #成功保存



4.我的测试仓库地址

码云:

https://gitee.com/caifugao110/mygitdemo.git

github:

https://github.com/caifugao110/obara_choosegun.git



---

---

二 JUC并发编程相关


