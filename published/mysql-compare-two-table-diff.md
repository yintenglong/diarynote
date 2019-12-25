sqlyog 同步两个数据库之间的数据同步

compare two database data

因为工作上遇到 同一个项目被部署到不同服务器上，原项目(后统称"源")在运行中，后部署的项目(后统称"目标")也在运行中。需要源的mysql数据同步到目标的mysql上。

我的情况是数据库的表结构是一样的，是数据需要同步。

在 sqlyog 也可以通过ssh通道来连接mysql(和navicat for mysql用法一样).

-------

下面是我在网上找的sqlyog软件并使用的，如果你懒得去再找，可以尝试下面的分享连接来下载使用

链接: [https://pan.baidu.com/s/1nZh1-EFqnZSMYL_k1v3Twg](https://pan.baidu.com/s/1nZh1-EFqnZSMYL_k1v3Twg) 提取码: jcbu 



------

前提: 两个有相同表结构的数据库的备份sql都导入到本地的mysql中

目标: 同步并生成对应的sql脚本，可以将这些sql脚本在 目标服务器的mysql中执行对比之后的sql脚本，达到同步数据的效果



我的操作步骤是: sqlyog的菜单栏 `高级工具` -> `数据库S 同步向导`

1. 弹出 向导的窗口，默认是`开始新工作`,点击`下一步`按钮
2. 选择源和目标的数据库，点击`下一步`按钮
3. 进入`数据同步高级选项`,我选的是`单向同步`并勾选`不要在目标删除额外的行`,点击`下一步`按钮
4. 进入`选择想要同步的表`,我选的是`在数据库中同步所有表`,点击`下一步`按钮
5. 进入`你要如何执行同步?`页，因为我是在本地导入了2个数据库，需要将同步的sql导入到远程上，所以选择的是`同步和生成脚本`,然后在给`文件名` 选择存放sql的路径,点击`下一步`按钮
6. 进入`错误处理`页，我是全不勾选,点击`下一步`按钮
7. 进入`在定期间隔发送查询结果`，我选择的是`立即运行`,点击`下一步`按钮
8. 进入到进行处理 同步操作了，等待执行完成，执行完成之后，`下一步`按钮是启用的了，点击`下一步`按钮之后，会进入`向导成功完成`页，点击`完成`按钮或者当前窗口的关闭按钮就会关闭窗口了。

然后打开第5步保存的sql文件，看里面是否是有 `INSERT`或者`UPDATE` 语句，如果有，将所有语句复制到远程的 phpmyadmin中的目标数据库中，执行对应的sql语句，就完成了数据同步操作了。



## References

1. [Compare two MySQL databases [closed]](https://stackoverflow.com/a/5516218)