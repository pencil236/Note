# 基本介绍

git是一个分布式版本控制系统。

- 为什么要用git？

  这其实是两个问题

  - 为什么要用版本控制系统？

  - 版本控制系统为什么要用git？

    Git跟踪并管理的是修改，而非文件

    远程仓库。

    Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成

  



# 跟着操作过程中的随手记

- pwd 显示当前目录路径

- mkdir directory1   //创建一个名为directory1 的目录

- cd directory1   //到directory1这个目录去

- git init  把当前文件夹初始化成一个git仓库   //initation 初始化 除了这个命令，其他命令必须在git仓库目录执行

- git add <file> 把文件添加到要暂存区，可以添加多个文件  //暂存区相当于*添加清单*(我自己的形容)，如果文件名带空格，就用双引号引起来

- git commit -m <message>    把暂存区的文件提交到git的本地仓库  //commit 在git中被成为快照 相当于游戏存档

- git status 查询工作区的状态 

- git diff 查看修改的内容  //diff 是 difference的缩写

- git log 查看commit(提交)的历史记录

- git log --pretty=oneline 只显示了更改的信息，以及一大串黄色数字，commit id (版本号)

- HEAD是一个指针指向表示当前的版本  HEAD^是上一个版本 HEAD^^是上上个版本    往上100个版本就写成HEAD～100

- git reset 回退版本或者把暂存区的修改回退到工作区

- git reset --hard HEAD^           //--hard参数指回退到上一个版本的已提交状态 *--soft回退到上一个版本未提交的状态 --mixed回退上一个版本未添加状态*  **这两个参数没用过 存疑,,,后两个参数的使用可能会导致head指向多个版本号的情况。具体代表什么，为什么会这样，以后研究**

- git reflog  查看命令历史,是reference log的缩写。指针的记录，也就是修改的记录




- 概念辨析：工作区 版本库 暂存区 分支 狭义修改 添加 提交 

  答：

  ​	举个例子，我创建了一个名为learngit的目录，这个目录就是**工作区(Working Directory)**,
  
  ​	当我用git init将这个目录初始化为一个git仓库后，这个目录中会有一个名为.git的目录，.git就是**版本库(Repository)**。
  
  ​	在版本库中有分支和暂存区(stage)，刚刚创建的版本库会自动创建第一个分支master，以及指向master的第一个指针HEAD。
  
  ​	我在learngit上创建一个名为readme.txt的文本文件(默认在master分支)，当我编辑文本的时候，我就是在**对工作区进行修改操作**。(狭义)
  
  ​	当我使用git add命令时就是把文件**添加到暂存区**。
  
  ​	当我用 git commit命令时就是把暂存区的所有文件一并**提交的到当前分支中**
  
  ​	广义的修改包括狭义修改 添加 提交三种操作(这是我自己分的)
  
  ​	git只有在每次commit的时候才会生成新的版本号
  
- git checkout -- <file>    用来撤销对工作区的修改。如果是修改后没有add(**修改没add**)，就会撤销到跟版本库一模一样的状态，如果是add后才对工作区进行了修改(**即add又修改**)，就会撤销到add后的状态。总而言之就是回到最近一次add或者commit的状态。--<file>必须要写，不然就是切换到另一个分支的命令

- git reset HEAD <file> 用来把暂存区的修改撤销掉，重新放回工作区.(用来应对**修改又add**的情况)   这个操作过后就是修改没add的状态了

- 如果是修改后又add还commit了，那就在推送到远程库之前回退版本库就好。用命令git reset --hard commit_id     这时候git reflog在远程库就看不到修改前的那个版本了（具体为什么还是有点含糊）

- 本地git仓库和GitHub仓库之间通过SSH加密   在用户的主目录.ssh目录有id_rsa 和 id_rsa.pub 两个文件。这两个就是SSH Key的密钥对，前者是私钥，后者是私钥

- 我们把id_rsa.pub的内容给到GitHub，GitHub就能确认是我自己推送的内容。我可以添加多台电脑的key到GitHub这样就可以在每台电脑上往GitHub推送了

- 当我们在GitHub上创建一个远程库的时候，可以从这个仓库克隆出新的仓库到本地，也可以把一个我们自己的本地仓库与这个远程库关联，然后，再把本地仓库的内容推送到GitHub仓库

- 在本地的learngit仓库下中运行 git remote add origin git@github.com : pencil236/learngit.git命令，就可以把本地的learngit仓库和远程仓库关联起来。其中 origin是远程仓库名可以自定义 pencil236是我的GitHub账户名 git@github.com中的git是GitHub预定义的SSH用户名，@后面的是GitHub服务器的域名      这里的learngit应该以远程仓库的名字为准           //remote就是远程的意思          关联的抽象命令是git remote add origin git@server-name:path/repo-name.git

- 上面那一段的命令，当你在github创建一个新的空的仓库的时候，github会给你提示，直接复制粘贴过去就好了

- 现在提倡把master分支改成main分支

- 如果远程仓库地址有误，可以使用 `git remote set-url origin <正确的地址>` 命令来修改。git@github.com : pencil236/learngit.git就是一个地址。

- git push origin master 就是把本地master分支的最新修改推送到GitHub

- 在第一次推送的时候，使用了命令git push -u origin master 这个-u参数不仅推送了本地分支master，还把本地master分支和远程的master分支关联起来。下次就可以简化命令了

- 注意 ：用公共网络的时候会限制不让推送，比如校园网。。。。记得换成手机热点

- git remote -v 这个命令用来查看远程库的信息

- git remote rm <name>  用来解除本地和远程的绑定关系，而不是物理上删除。要物理删除就登录到GitHub网站上去删除 这里name指库名，比如origin

- git clone git@github.com:pencil236/learngit.git  用来将远程库克隆到本地，具体在本地你输入这条命令时所在的文件夹

- HEAD指向当前分支，当前分支指向当前的commit。初始化时默认有一个分支master

- git branch dev 创建dev分支

- git checkout dev 切换到分支dev

- git checkout -b dev 创建并切换到分支dev

- git branch 会列出所有的分支 当前分支前面会标一个*号

- git merge <branch name>合并指定分支到当前分支 eg 我们当前在master分支 当我们使用命令 git merge dev 就会让master指向dev指向的commit，也就将dev分支上的内容合并到master分支了。这种合并是快进模式，不是每种情况都能成功

- git branch -d dev  删除dev分支

- 创建一个分支来工作，完成后再合并到主分支master，这样更安全

- 最新版git提供了新的命令来切换分支 如下

  git switch -c dev 创建并切换到devfenzhi

  git switch master 切换到已有的master分支

- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

  解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

  用git log --graph命令可以看到分支合并图。

- 对于GitHub上别人的仓库，想克隆到本地，得先在网站上别人的项目主页，点Fork，把这个项目克隆到自己的账号上，再用命令 git clone git@github.com:pencil236/<仓库名.git> 克隆到本地。如果从别人的仓库克隆，会没有推送修改的权限。

- 下次从分支管理策略开始看(含)









# 杂记

- **MINGW64**，指的是**Minimalist GNU for Windows 64-bit** 是windows用来模拟类unix环境的环境因为git一开始只能在类unix环境中运行。在git bash中MINGW 64～表示当前所在的工作目录路径

- 23623@pencil    //23623是当前的用户名 pencil是我的主机名 你会发现<用户名>@<主机名> 是很常见的搭配

  ![image-20250708061720579](C:\Users\23623\AppData\Roaming\Typora\typora-user-images\image-20250708061720579.png)
  
- 在windows自带的命令行中，依然可以使用git，但是习惯上还是用git bash因为git bash

  使用的还是Linux的命令，同时有颜色的区分，更好用点。git bash 打开后默认在他所在的目录里面

- git默认是不区分大小写的，但是可以自己设置









# 总结

