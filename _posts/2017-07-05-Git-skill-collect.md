---
layout: post
title: "Git 本地配置多账户"
date: 2017-07-05 23:25:06 +0800
description: 今天在工作中遇到了自己的账户和公司账户两个在我电脑上同时维护的问题，记录下来，以备使用！
tags: 
 - Git

---
问题描述：
>我自己在Github上有一个[账号](https://github.com/flypig-xian)，里面维护了一些资料和工具，这次入职链家，团队给了一个新的账号和[平台](http://git.lianjia.com)。如果不配置SSH Key到服务器上，每次都要输入密码很麻烦！

感谢同事的指点，虽然不是理想的解决方法，但是也是解决方法的一部分！最后经过精确检索，将正确的解决方法记录在这里！

总的来说，解决方法也很简单，就是对应两个账号，生成两套Key(保存文件名要不一样)，然后添加Key，最后在~/.ssh下配置config文件就可以了！

- 假设已经配置过一个Git账号了，我们先用`ssh-keygen`命令生成一组新的`id_rsa_new`和`id_rsa_new_pub`
>ssh-keygen -t rsa -C "your new email"
这里需要注意，给保存秘钥的文件起一个不一样的名字，不要一路回车下去，否则会覆盖原有的秘钥文件。

- 使用`ssh-agent`命令让ssh识别不同的秘钥
>ssh-add ~/.ssh/id_rsa_new

    如果出现`Could not open a connection to your authentication agent`的错误提示，可以尝试按下述方式解决：
    >ssh-agent bash
    ssh-add ~/.ssh/id_rsa_work

- 在`~/.ssh`下添加config配置文件并加上相应的配置
   >touch config        # 如果不存在，则创建config文件

    文件内容按照示例设置：
    >\# 本文件用于配置私钥对应的服务器
        \# Default user
        Host github.com.cn
        HostName github.com.cn
        User git
        IdentityFile ~/.ssh/id_rsa
        \# Second user
        \# 建一个github别名，新建的帐号使用这个别名做克隆和更新
        Host git@code.xxxxxxx.com
        HostName https://code.xxxxxxx.com    #公司的gitlab
        User git
        IdentityFile ~/.ssh/id_rsa_new

    Host会替换HostName中的内容，所以如果系统有默认的话，可以直接用Host,或者两者内容改成一致。
    最后不要忘记把Key添加到服务器中。
