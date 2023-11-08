# Git 学习

### 一、常用命令

#### 1.设置用户签名

```
git config --global user.name <用户名>           
git config --global user.email <邮箱>     

#首次安装后设置即可，用于区分不同操作者身份
```



#### 2.初始化本地库

```
git init

#希望将某个文件夹设为git仓库时，先在该文件夹右键bash，然后初始化
```



#### 3.查看本地库状态

```
git status
```



#### 4.将工作区的文件添加到暂存区

```
git add <文件名>
```



#### 5.将暂存区的文件提交到本地库

```
git commit -m <"日志信息"> <文件名>
```

<img src="C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231012134606101.png" alt="image-20231012134606101" style="zoom: 67%;" />

#### 6.查看历史版本

```
git reflog            #查看版本信息
git log               #查看版本详细信息
```



#### 7.版本穿梭

```
git reset --hard <版本号>

#每次提交代码都会产生历史版本，通过本指令可以在不同版本中切换
#底层原理：Git 切换版本，其实是移动 HEAD 指针
```



### 二、分支操作

- 同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支
- 创建分支可以从开发主线上分离出来，开发自己分支的时候不会影响主线分支的进行
- 各个分支在开发过程中，某一个分支开发失败，不会对其他分支有影响

<img src="C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231012143252111.png" alt="image-20231012143252111" style="zoom:67%;" />

#### 1.查看分支

```
git branch -v
```



#### 2.创建分支

```
git branch <分支名>
```



#### 3.切换分支

```
git checkout <分支名>
```



<img src="C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231012160339086.png" alt="image-20231012160339086" style="zoom:67%;" />

- 每个分支名其实都是指向具体版本记录的指针，所以创建分支的本质就是多创建一个指针

- 当前所在的分支，其实是由 HEAD 指针决定的， HEAD 指向哪一个分支，目前就在那一个分支上。

- 如图中，目前就是在 master 分支的 v2 版本上，切换分支和切换版本的本质都是改变指针

  

#### 4.合并分支

```
git merge <分支名>

#此处是将所选的分支合并到当前分支上来
```



#### 5.合并冲突

- 冲突产生的表现：后面状态为 MERGING

![image-20231012151831758](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231012151831758.png)

- 冲突产生的原因：合并时两个分支在同一文件的同一位置有两套不同的修改，必须认为决定新代码内容

- 查看状态

  ```
  git status
  ```



#### 6.解决冲突

```
#冲突时代码显示如下

<<<<<<< HEAD  
XXX          #当前分支的代码  
XXX
======
XXX          #要合并的代码
XXX
>>>>>>> hot-fix

```

- 编辑有冲突的文件，删除特殊符号，决定要使用的内容
- 删掉 “<<<<<<< HEAD” 、 “======” 、 “>>>>>>> hot-fix”
- 在两个部分中，自行选出需要保留的内容，然后保存即可，保存时的代码即是最后提交的代码



解决完冲突的代码添加到暂存区

```
git add <文件名>
```

执行提交（此时git commit 命令时**不能带文件名**）

``` 
git commit -m <"日志信息">

#因为两个分支都修改了同一个文件名的文件，git commit带文件名时，git不知道你要提交的是哪一个
```



### 三、GitHub操作

#### 1.创建远程仓库

![image-20231016132520779](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016132520779.png)

#### 2.远程库链接

<img src="C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016133434803.png" alt="image-20231016133434803" style="zoom:67%;" />

<img src="C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016133451650.png" alt="image-20231016133451650" style="zoom:67%;" />



#### 3.创建别名

链接不方便输入和记忆，给链接起一个别名，方便操作

```
git remote -v						    #查看当前所有远程地址别名
git remote add <别名> <远程地址>          #创建远程地址别名
```

例如

```
git remote add demo https://github.com/YC-CS/demo.git		#例子
```



#### 4.推送本地分支到远程仓库

```
git push <别名> <分支>
```



#### 5.将远程库对于分支最新内容拉取出与当前本地分支直接合并

```
git pull <远程库地址别名> <远程分支名>
```



#### 6.将远程仓库的内容克隆到本地

```
git clone <远程地址>
```

clone 会做如下操作：

1、拉取代码

2、初始化本地仓库

3、创建别名



#### 7.团队内协作

邀请团队内成员的操作如下

![image-20231016162252561](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016162252561.png)

邀请的账户可以修改内容，并直接将修改后的内容传入远程仓库



#### 8.跨团队协作

- 将远程仓库的地址复制发给邀请跨团队协作的人
- 对于跨团队的修改者，点击fork将项目叉到本地仓库

![image-20231016162515788](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016162515788.png)



- 此时修改文件并提交，创建一个Pull请求

![image-20231016163221052](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016163221052.png)

- 拥有者收到Pull请求，审核，审核通过后，才会修改仓库的代码

![image-20231016163334722](C:\Users\YC105\AppData\Roaming\Typora\typora-user-images\image-20231016163334722.png)

