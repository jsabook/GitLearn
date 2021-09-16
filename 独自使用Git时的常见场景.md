# 删除不需要的分支

删除

```
git branch -d branch_name
```

强制删除，没有merge也可以直接删除

```
git branch -D branch_name
```



# commit 操作

## 修改最新commit的message

```
git commit --amend
```

在这个`vi`界面进行操作；

![image-20210917000658715](img/image-20210917000658715.png)

修订完毕之后，查看这一次提交

![image-20210917000750319](C:\Users\Administrator\Desktop\GitLearn\img\image-20210917000750319.png)

可以发现已经发生了修改

TODO

## 修改老版本的**commit**的**message**

```
git rebase -i commit_id_parent_id
```

我们需要选择父亲节点。例如，这里修改`d2d2c1c95019ee6b`

![image-20210917003157105](img/image-20210917003157105.png)

查看，可以得到

![image-20210917003401861](img/image-20210917003401861.png)

进行修改

![image-20210917003720190](img/image-20210917003720190.png)

退出后进行修改

![image-20210917004227145](img/image-20210917004227145.png)

做完操作后，可以发发现产生了新的commit

```
[detached HEAD 56e755a] MOVE README =>Successfully rebased and updated
```

可以发现已经发生了变化

![image-20210917005301803](C:\Users\Administrator\Desktop\GitLearn\img\image-20210917005301803.png)



## 整合多个commit

> 因为我们需要在rebase界面修改，因此需要选择父亲的父亲节点。

```
git rebase -i commit_id_parent_parent_id
```

这里的commit也需要选择其commit_parent的父亲节点的id。下面的样例中，把`MOVE README`和`change readme`进行合并。则需要选择`add readme`的ID号（因为这个id号是change readme的父亲commit id）。

![image-20210917005917618](C:\Users\Administrator\Desktop\GitLearn\img\image-20210917005917618.png)

选择后，查看

![image-20210917010443921](img\image-20210917010443921.png)
进行修改

![image-20210917010523207](img/image-20210917010523207.png)

修改完毕，则发现已经合并到一起了

![image-20210917010711018](img/image-20210917010711018.png)

c32c8c4

## 整合非连续的commit

![image-20210917012322750](img/image-20210917012322750.png)

显示结果

![image-20210917012516540](img/image-20210917012516540.png)

会出现多个独立的commit

TODO

# 比较暂存区与HEAD文件的差异

**HEAD**表示的是目前最新一次的**commit**

```
git  diff --cache
```

# 比较工作区和暂存区之间的区别

```
git diff
```

# 让暂存区恢复成和HEAD一样

不保留缓存区的所有文件内容

```
git reset HEAD
```

这一条命令也就是清除缓存区（因此reset也有清除的含义）

![image-20210915060318365](img/image-20210915060318365.png)

清除部分文件

```
git reset HEAD -- <file>
```

# 工作区恢复为和暂存区一样

部分文件

```
git checkout -- <file>
```

# 取消最近几次的提交

——将commit从git仓库中消失

```
git reset --hard  old_commit_id
```

将暂存区与工作区都指向`old_commit_id`这个commit。同时`HEAD`也指向`old_commit_id`对应位置。

# 查看不同提交的指定文件的差异

```
git diff dev master -- <file>
```

# 文件/文件夹不纳入管理

创建一个`.gitignore`文件，在文件中放入的文件就不会被管理，支持通配符。

```
doc/
doc
*.doc
doc/*.txt
```

# git 的备份



| 协议名称 | 语法格式                               | 说明             |
| -------- | -------------------------------------- | ---------------- |
| 本地协议 | /path/to/repo.git                      | 哑协议           |
| 本地协议 | file:///path/to/repo.git               | smb协议/智能协议 |
| http协议 | http://git-server.com/path/to/repo.git |                  |
| ssh协议  | user@git-server.com/path/to/repo.git   |                  |

## 哑协议

**下载**

```
git clone --bare file:///path/to/repo.git
```

**上传**

```
git remote add zhineng file:///path/to/repo.git
git push  --set-upstream zhineng branch_name
```

