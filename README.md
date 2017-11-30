# git-diff-patch
git diff 生成patch, git apply patch 打补丁方法说明，以及分支管理的简单操作

先git log 查看commit ID, 记录你想要打的补丁的ID
比如说：
```
git log
commit 4ff35d800fa62123a28b7bda2a04e749addf1918
Author: chenfulin5 <chenfulin5@gmail.com>
Date:   Tue Dec 20 17:37:09 2016 +0800

    [I2C EEPROM]

commit acb8cd154cecf20894ae25fc3787d6b6ba9b32ea
Author: chenfulin5 <chenfulin5@gmail.com>
Date:   Mon Dec 19 18:45:03 2016 +0800

    [I2C0 AT24] add at24 eeprom
```
那么你就可以运行如下命令进行生成patch
git diff acb8cd15   4ff35d80  > patch
现在已经生成了一个patch, 那么可以使用 git apply 进行打补丁。

#### git branch

不过我们现在可以建一个分支进行试验。
```
git branch new_branch
git branch  
```
可以看到多了一个分支。
切换分支使用如下命令：
```
git checkout new_branch
```
也有快捷命令直接创建分支并切换：
```
git checkout -b test_branch
```
git branch 可以看到你已经切换到了test_branch 分支上面。

删除分支：
```
git branch -D test_branch
git branch 
```
可以看到已经将 test_branch分支删除掉。


重命名分支：
```
git branch -m new_branch chen_new_branch
git branch 
```
可以看到new_branch 已经改名为chen_new_branch分支

分支合并：
现在我假定你还有两个分支:    
一个master主分支以及一个chen_new_branch分支。
```
git checkout chen_new_branch 
```
确定你现在在这个分支上面
提交一个改动：
```
echo "test" >> test
git add .
git commit -m "This is test"

git diff chen_new_branch master 
```
就可以看到不同   

也可以
```
git log master
git log chen_new_branch
```
查看他们两个分支的commit 有什么不同。

然后跳到master分支：
```
git checkout master
git branch 
```
确认你已经在master 分支上面。
```
git merge chen_new_branch 
```
合并。

#### git apply

回到我们刚才利用git diff HARD HARD > patch 生成的补丁文件。
将这个补丁文件拷贝过来
```
git checkout -b  patch_test
git apply patch
git status 
```
看到状态后你知道你要做相关的动作了吗？
OK你做吧
最后:
```
git commit -m "test"
```

你是不是想这不是试验，那么
```
git checkout master
git merge patch_test 合并分支。OK
```
2017.11.30
