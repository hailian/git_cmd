## git 指令汇总

### 0 忽略HTTPS的CA认证

```shell
git config --global http.sslVerify false
```



### 1 常用指令

#### 1.1创建仓库

```shell
# 在当前目录下创建git环境
git init .
```

#### 1.2添加文件

```shell
# 把当前所有文件添加到缓存区
git add .
```

#### 1.3提交文件

```shell
# 把缓存区文件提交
git commit -m "first commit"
```

##### 1查看提交状态

```shell
# 查看提交状态与记录
git log
```

##### 2 修改提交message

```shell
# 修改最后一次提交的 message（只能修改最后一次的提交）
git commit --amend 
```



#### 1.4 查看状态

```shell
git status
```

##### 1 未add到缓存区

```shell
# 添加到缓存区
git add .
# 更改回退
git restore <filename>
```

##### 2 在缓存区未提交

```shell
# 提交
git commit -m "log message"
# 更改回退
git restore --staged <filename>
# 回退后依旧在工程区，再去掉更改
git restore <filename>
```

#### 1.5 对比文件

##### 1 对比当前文件与缓冲区所有文件

```shell
# 对比当前文件与缓冲区所有文件
git diff
```

##### 2 对比当前文件与缓冲区某一文件

```shell
git diff <filename>
```

##### 3 对比两次提交的文件

```shell
git diff <commit> <commit>
# <commit>为commit的16进制标识码
```

##### 4 对比两题提交的某一文件

```shell
git diff <commit> <commit> -- <filename>
```

#### 1.6 删除文件

```shell
 git rm --cached "文件路径"，不删除物理文件，仅将该文件从缓存中删除；
```

```shell
git rm --f "文件路径"，不仅将该文件从缓存中删除，还会将物理文件删除（不会回收到垃圾桶）
```

----------

### 2 版本管理

#### 2.1 版本切换

```shell
# 版本间的切换
git checkout <commit>
```

#### 2.2 同一版本，log合并

```shell
# 版本合并
git rebase -i HEAD~[number_of_commits]

#选择pick操作		git会应用这个补丁，以同样的提交信息（commit message）保存提交
#选择reword操作		git会应用这个补丁，但需要重新编辑提交信息
#选择edit操作		git会应用这个补丁，但会因为amending而终止
#选择squash操作		git会应用这个补丁，但会与之前的提交合并
#选择fixup操作		git会应用这个补丁，但会丢掉提交日志
#选择exec操作		git会在shell中运行这个命令
```

#### 2.3 撤销某次commit

```
# 撤销commit
git reset --soft HEAD^

# HEAD^的意思是上一个版本，也可以写成HEAD~1
# 如果你进行了2次commit，想都撤回，可以使用HEAD~2
```

--------

### 3 分支管理

#### 3.1 查看分支

```shell
# 查看本地
git branch 
```

```shell
# 查看本地和远程
git branch -a
```

#### 3.2 删除分支

```shell
# 删除本地分支
git branch -d [branchname]
```

```shell
# 删除远程分支
git push origin --delete [branchname]
```

#### 3.3 创建分支

```shell
git branch [branchName]
```

#### 3.4 指定版本创建分支

```shell
git checkout -b [branchName] <commit>
# 默认在当前版本下创建分支
```

#### 3.5 上传分支

```shell
git push origin [branchName]
```

#### 3.6 合并分支

```shell
git merge [branchName]
```

```shell
//忽略合并
git merge --abord
```

#### 3.7 获取分支

```shell
git fetch origin [branchName]
```

### 4 https换成ssh

#### 4.0 生成ssh.public

```shell
//查看备份key，没有则忽略
cd ~/.ssh
//执行,生成key
ssh-keygen
//拷贝public的key到ssh配置
```

#### 4.1 移除origin

```shell
git remote rm origin
```

#### 4.2 增加origin

同样对于ssh换成https也是一样

```shell
//git remote add origin git@192.168.12.192:debenv/git_cmd.git
git remote add origin [url]
```



### 5 tag版本管理

#### 5.1新建tag

```shell
git tag <tag name>
```

#### 5.2给指定的某个commit号加tag

```shell
//给指定的某个commit号加tag
git tag -a <tagName> <commit> -m <log str>
```

#### 5.3删除某个tag

本地删除

```
git tag -d <tagName>
```

远程删除

```shell
git push origin :refs/tags/<tagName>
```

#### 5.4将tag同步到远程服务器

```shell
git push origin <tagName>
```
#### 5.5 同步子模块

```shell
git submodule update --init
```

