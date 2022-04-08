# 将本地代码仓库关联到 github 上

![image-20220408195008316](C:\Users\think\AppData\Roaming\Typora\typora-user-images\image-20220408195008316.png)



 仓库地址就是复制这里的地址。作用是将本地的仓库关联到远程仓库。   在这一步时如果出现错误：`fatal:remote origin already exists`，解决方法如下：

1. 先输入

```javascript
git remote rm origin
```

其实所谓的：neiwang、waiwang、origin，都只不过是`.git/refs/remotes/`下的一个文件夹名称而已，这是git的工作原理决定的，`.git/refs/remotes/`下的文件夹，是跟远程仓库数据关联的，你可以认为它们是远程仓库在你本地的缓存

rm是remove 去除

1. 再输入

```javascript
git remote add origin 仓库地址
```



# 将代码由本地仓库上传到 gitee远程仓库

## 6.1、获取远程库与本地同步合并

  如果远程库不为空必须做这一步，否则后面的提交会失败。

```javascript
# 不加这句可能报错，原因是 gitee 中的 README.md 文件不在本地仓库中。
# 可以通过该命令进行代码合并
git pull --rebase origin master  
```

复制

## 6.2、 把当前分支 master 推送到远程

  执行此命令后有可能会让输入用户名、密码

```javascript
git push -u origin master
```

复制

  执行完之后如果无错误就上传成功了，需要提示的是这里的 master 是 gitee默认的分支。

1. 如果你本地的当前分支不是 master，就用git checkout master命令切换到master分支。
2. 如果你想用本地当前分支上传代码，则把第6步的命令里的 master 切换成你的当前分支名即可。

