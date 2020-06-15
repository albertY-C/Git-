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

* **分支管理**

