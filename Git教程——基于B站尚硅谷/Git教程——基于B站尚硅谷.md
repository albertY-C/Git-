# Git教程——基于[B站尚硅谷](https://www.bilibili.com/video/BV1pW411A7a5/?p=7)

## 1. Git命令行操作

### 1.1 本地库操作

* **本地库初始化**

  > * 命令：`git init`
  >
  > * 效果：
  >
  >   ![image-20200614092946460](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200614092946460.png)
  >
  > * 注意事项：.git目录中存放的是本地库相关的子目录和配置文件；

* **设置签名**

  > * **形式**：
  >
  >   * 用户名：tom
  >
  >   * E-mail地址：goodMorning@163.com
  >
  > * **作用**：*区分不同开发人员；*
  >
  > * **辨析**：这里设置的签名和远程库(代码托管中心)的账号、密码没有任何关系；
  >
  > * **命令**：
  >
  >   * 项目级别/仓库级别：仅在当前版本本地库生效
  >
  >     项目级别命令：
  >
  >     `git config user.name tom` (设置名字)
  >
  >     `git config user.email goodMorning@163.com`(设置E-mail地址)
  >
  >     ![image-20200614094151895](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200614094151895.png)
  >
  >   * 系统用户级别：登陆当前系统的用户
  >
  >     系统级别命令：
  >
  >     `git config --global user.name tom` (设置名字)
  >
  >     `git config --global user.email goodMorning@163.com`(设置E-mail地址)
  >
  >     ![image-20200614094223333](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200614094223333.png)
  >
  >     * 级别优先级
  >
  >       就近原则：项目级别优先于系统用户级别，二者都有时则采用项目级别的签名；
  >
  >       唯一原则：如果只有系统用户级别的签名，就以系统级别用户级别的签名为准；
  >
  >       必需原则：二者级别至少有一个要存在，否则操作时Git会报错；
  >
  >     * 信息保存的位置：
  >
  >       ` cat .git/config`
  >
  >       ![image-20200614095958144](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200614095958144.png)
  >
  >     

* **版本管理**

  利用HEAD指针还原历史版本，一个历史版本的生成分为以下几步：

  工作区	——>	暂存区	——>	本地库

  工作区：即为Git管理下所编辑的文档、代码等用户直接操作的文件；

  暂存区：即为`git add . `命令后，文件所发生的改变；

  本地库：即为`git commit -m "MESSAGE"`命令后，文件所提交到的地方；

  > 命令：
  >
  > * 文件添加操作
  >
  >   * `git status`
  >
  >     查看工作区、暂存区[^1]的状态；
  >
  >   * `git add .`
  >
  >     将工作区的新建/修改添加到暂存区，进入待提交状态，此时的文件显示绿色；
  >
  >   * `git commit -m 'message'`
  >
  >     提交当前缓存的文件；
  >
  > * 文件删除
  >
  >   * git status
  >
  > * 版本控制操作
  >
  >   每一次提交都会有个版本，并且附带提交的信息；
  >
  >   ![image-20200615103649261](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200615103649261.png)
  >
  >   * 版本显示
  >
  >     `git log`/`git log --online`/`git reflog`(多屏显示：`b`向上翻页、`space`向下翻页、`q`退出)
  >
  >     查看提交的信息，包括：版本号(哈希算法)、作者、提交的时间、附加的信息；
  >
  >     ![image-20200615103916878](D:\Software\MarkDown\workspace\Git使用方法\attachment\pic\image-20200615103916878.png)
  >
  >   * 基于索引值操作[推荐]
  >
  >     利用版本号恢复相对应的版本内容，类似于指针索引；
  >
  >     > `git reset --hard [版本号]`(版本号可以使用头部标识的版本)
  >     >
  >     > 在本地库移动HEAD指针,重置暂存区,重置工作区;
  >     >
  >     > SPECIFICATION: *Resets the index(暂存区) and working tree(工作区). Any changes to tracked files in the working tree since `<commit>` are discarded.*
  >     >
  >     > 例：`git reset --hard 1957e04`
  >     >
  >     > ---
  >     >
  >     > `git reset --soft[版本号]`
  >     >
  >     > 仅在本地库移动HEAD指针，通俗的理解即为将文件操作恢复到`add`之前;
  >     >
  >     > SPECIFICATION: *Does not touch the index file or the working tree at all (but resets the head to `<commit>`, just like all modes do). This leaves all your changed files "Changes to be* committed", as `git status` would put it.
  >     >
  >     > ---
  >     >
  >     > `git reset --mixed[版本号]`
  >     >
  >     > 在本地库移动HEAD指针,重置暂存区，通俗的理解即为将文件内容恢复到`commit`之前;
  >     >
  >     > SPECIFICATION: *Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.*
  >     
  >   * 文件差异比较
  >
  >     > `git diff [FileName]`
  >     >
  >     > 将工作区的文件个暂存区进行比较；
  >     >
  >     > ---
  >     >
  >     > `git diff [本地库中历史版本] [FileName]`
  >     >
  >     > 将工作区中的文件和本地库历史记录比较

* **分支管理**

  在版本控制过程中，使用多条线同时推进多个任务；

  同时并行推进多个功能开发，提高开发效率；

  各个分支之间相互独立，如果一个分支开发失败不会影响到其他分支开发进度；

  >* 创建分支
  >
  >  `git branch [分支名]`
  >
  >* 查看分支
  >
  >  `git branch -v`
  >
  >* 切换分支
  >
  >  `git checkout [分支名]`
  >
  >* 合并分支
  >
  >  第一步：切换到接受修改的分支(被合并)上；
  >
  >  `git checkout [被合并的分支名]`
  >
  >  第二步：执行merge命令；
  >
  >  `git merge [有新内容的分支名]`
  >
  >* 解决冲突

































































[^1]:暂存区的作用在于可以撤销修改过的文件，`git add`命令操作的文件会存放到暂存区，`git commit`命令操作的文件会直接存放到工作区；

