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

  执行此命令后有可能会让输入用户名、密码（第一次要加-u，之后就不用了）

```javascript
git push -u origin master
```

复制

由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需 **`git push origin master`**

  执行完之后如果无错误就上传成功了，需要提示的是这里的 master 是 gitee默认的分支。

1. 如果你本地的当前分支不是 master，就用git checkout master命令切换到master分支。
2. 如果你想用本地当前分支上传代码，则把第6步的命令里的 master 切换成你的当前分支名即可。

**失败原因：** 由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过**`git pull --rebase origin master`**命令先将内容合并,此时再push就能成功了。







### 远程仓库设置

由于本地Git仓库和Github仓库之间的传输是通过SSH加密的，所以连接时需要设置一下：

- 5.1、创建SSH KEY。先看一下你C盘用户目录下有没有.ssh目录，有的话看下里面有没有id_rsa和id_rsa.pub这两个文件，有就跳到下一步，没有就通过下面命令创建
   **`$ ssh-keygen -t rsa -C "youremail@example.com"`**
   然后一路回车。这时你就会在用户下的.ssh目录里找到id_rsa和id_rsa.pub这两个文件.
- 5.2、登录Github   --->点击右上角的图标     --->选择Settings     --->点击左边的SSH and GPG KEYS    --->点击右上角的New SSH key    --->Title随便填     --->把刚才id_rsa.pub里面的内容复制到Title下面的Key内容框里面    --->最后点击Add SSH key    --->完成SSH Key的加密。具体步骤如下：

![img](https:////upload-images.jianshu.io/upload_images/13098542-1bd5d81617e91e3e.png?imageMogr2/auto-orient/strip|imageView2/2/w/694/format/webp)

- 5.3、在Github上创建一个Git仓库。

![img](https:////upload-images.jianshu.io/upload_images/13098542-cc9081220c33a824.png?imageMogr2/auto-orient/strip|imageView2/2/w/652/format/webp)

在Github上创建好Git仓库后通过命令**`git remote add origin git@github.com:linsili/test.git`**和本地仓库进行关联

![img](https:////upload-images.jianshu.io/upload_images/13098542-1a0dcf2ee4e03a37.png?imageMogr2/auto-orient/strip|imageView2/2/w/395/format/webp)

注意 origin 后面加的是你Github上创建好的仓库的地址。

![img](https:////upload-images.jianshu.io/upload_images/13098542-db664836f0524179.png?imageMogr2/auto-orient/strip|imageView2/2/w/991/format/webp)

------

7. 关联好之后通过命令**`git push -u origin master`**将本地库的所有内容推送到远程仓（Github）

![img](https:////upload-images.jianshu.io/upload_images/13098542-c4f5586f356eaaab.png?imageMogr2/auto-orient/strip|imageView2/2/w/549/format/webp)

由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需 **`git push origin master`**

刷新Github页面进入刚才新建的仓库里面就会发现项目已经上传成功

![img](https:////upload-images.jianshu.io/upload_images/13098542-147f5fe4c3c7c14d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1002/format/webp)

至此完成将本地项目上传到Github的整个过程。

------

**注意有坑：** 在上面第5步新建远程仓库的时候如果你勾选了Initialize this repository with a README（就是创建仓库的时候自动给你创建一个README文件），那么到了第7步你将本地仓库内容推送到远程仓库的时候就会报一个failed to push some refs to  https://github.com/guyibang/TEST2.git的错。



**原因：** 由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过**`git pull --rebase origin master`**命令先将内容合并,此时再push就能成功了。

------

## **总结：本地项目通过git上传到github**

- 1)、在本地创建一个版本库（即文件夹），通过`git init`把它变成Git仓库；
- 2)、把项目复制到这个文件夹里面，再通过`git add .`把项目添加到仓库；
- 3)、再通过`git commit -m "注释内容"`把项目提交到仓库；
- 4)、在Github上设置好SSH密钥后，新建一个远程仓库，通过`git remote add origin 远程仓库地址`将本地仓库和远程仓库进行关联；
- 5)、最后通过`git push -u origin master`把本地仓库的项目推送到远程仓库（也就是Github）上。



