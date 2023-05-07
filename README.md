# Git

### 一、基本配置

1、设置用户信息

```
git config --global user.name"liqinglin"
```

```
git config --global user.email"1740242084@qq.com"
```

2、查看配置信息

```
git config --global user.name
```

```
git config --global user.email
```

3、为常用指令配置别名

+ 打开用户目录，创建 .bashrc 文件

```
touch ~/.bashrc
```

+ 在 .bashrc 文件中输入以下内容

```
#用于输出git提交日志

alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'

#用于输出当前目录所有文件及基本信息

alias ll='ls -al'
```

4、打开 GitBash，执行

```
source ~/.bashrc
```

5、解决 GitBash 乱码问题

+ 打开 GitBash 执行下面命令

```
git config --global core.quotepath false
```

+ 在 ${git_home}/etc/bash.bashrc 文件最后加入下面两行

```
export LANG="zh_CN.UTF-8"

export LC_ALL="zh_CN.UTF-8"
```

### 二、获取本地仓库

1、任意创建一个空目录（比如test）作为本地Git仓库

2、进入这个目录，打开 GitBash 执行下面命令

```
git init
```

3、如果创建成功后可在文件夹下看到隐藏的.git目录

### 三、Git常用指令

仓库(repository) <- git commit -- 暂存区(index) <- git add -- 工作区(workspace) <- 修改已有文件/新创建一个文件 --

1、创建文件

```
touch xxx.xxx
```

2、查看修改的状态(status)

```
git status
```

3、添加工作区到暂存区(add)

```
git add .
```

4、添加暂存区到本地仓库(commit)

```
git commit -m '注释'
```

5、查看提交日志(log)

```
git log
```

```
git-log // 推荐
```

6、修改文件

```
vi xxx.xxx
```

7、版本回退/版本切换

```
git reset --hard <commitID>
```

8、查看已删除的记录

```
git reflog
```

9、添加文件至忽略列表

在工作目录中创建名为 .gitignore 文件，列出要忽略的文件模式

```
touch .gitignore
```

```
vi .gitignore
```

### 四、分支

1、查看本地分支

```
git branch
```

2、创建本地分支

```
git branch <分支名>
```

3、切换分支(checkout)

```
git chechout <分支名>
```

还可以切换到一个不存在的分支（创建并切换） // 推荐

```
git checkout -b <分支名>
```

4、合并分支(merge)

合并分支时，一般将其他分支合并到 master 分支上，即在  master 分支上进行合并分支

```
git merge <分支名称>
```

注意，如果 Git 版本过低，会进入类似于 vi 的编译器，退出指令为：Esc + : + wq 

5、删除分支

不能删除当前分支，只能删除其他分支

```
git branch -d <分支名称> // 删除分支时，需要做各种检查
```

```
git branch -D <分支名称> // 不做任何检查，强制删除
```

6、解决冲突

当两个分支上对文件的修改可能会存在冲突，例如同时修改了同一个文件的同一行，这时就需要手动解决冲突

解决步骤：处理文件冲突的地方 -> 将解决完冲突的文件加入暂存区(add) -> 提交到仓库(commit)

7、开发中分支使用原则与流程

+ master(生产)分支 -- 线上分支，主分支，中小规模项目作为线上运行的应用对应的分支；

+ develop (开发)分支 -- 从 master 创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要是合并到 master 分支，准备上线；

+ feature/xxx 分支 -- 从 develop 创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到 develop 分支；

+ hotfix/xxx 分支 -- 从 master 派生的分支，一般作为线上 bug 修复使用，修复完成后需要合并到 master, teat, develop 分支；

+ 其他分支，如 test 分支（用于代码测试）、pre 分支（预上线分支）等等。

### 五、Git远程仓库

1、配置 SSH 公钥

+ 生成 SSH 公钥

```
ssh-keygen -t rsa
```

不断回车 -> 如果公钥已经存在，则自动覆盖

+ 获取公钥

```
cat ~/.ssh/id_rsa.pub
```

+ 验证是否配置成功

```
ssh -T git@github.com
```

2、操作远程仓库

+ 添加远程仓库

```
git remote add origin <仓库路径>
```

+ 查看远程仓库

```
git remote
```

+ 推送到远程仓库

```
git push origin master // 远程分支名和本地分支名相同，则可以只写本地分支
```

```
git push --set-upstream origin master // --set-upstream 推送到远端的同时并且建立起和远端分支的关联关系
```

```
git push // 将 master 分支推送到已关联的远端分支，如果当前分支已经和远端分支关联，则可以省略分支名和远端名
```

3、从远程仓库克隆

```
git clone <仓库路径> <本地目录>
```

4、从远程仓库中拉取和抓取

+ 抓取：抓取指令就是将仓库里的更新都抓取到本地，不会进行合并

```
git fetch <remote name> <branch name>
```

如果不指定远端名称和分支名，则抓取所有分支

+ 拉取：拉取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于 fetch + merge

```
git pull <remote name> <branch name>
```

如果不指定远端名称和分支名，则抓取所有并更新当前分支

5、解决合并冲突

在一段时间内，A、B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突

解决步骤：远程分支也是分支，所以合并时冲突的解决方式也和解决本地分支冲突相同

处理文件冲突的地方 -> 将解决完冲突的文件加入暂存区(add) -> 提交到仓库(commit)
