## merge
1. fast-forward
快进合并不可能出现冲突（将自己的分支合并到master时，master分支没有被更改过）
2. 非fast-forward
将自己的分支合并到master时，master分支在自己分支叉出去之后又有了新的更新，这时就需要把master分支和自己分支修改的内容汇合起来生成一个新的提交，同时HEAD会移动到该提交上。
3. 设置 non fast-forward
设置方法：添加 -no-ff
在设定了non fast-forward选项的情况下，即时在能够fast-forward的情况下也会产生新的提交并合并
## rebase
rebase会在原有提交的基础上将差异内容添加到master分支的后面，历史记录成一条直线。
rebase分为两步
1. git rebase master
rebase的时候出现冲突，解决冲突时的提交不是使用commit命令，而是执行 git rebase --continue
若要取消，则执行 git rebase --abort
2. rebase后，master的HEAD位置不变（不会自动前移），因此要执行
git checkout master
git merge bugfix //此时为快进合并，不会有冲突

#### rebase规则：不要对在自己的仓库外有副本的分支执行变基

## 区别
1. 对历史记录的事情不同
merge：记录的是仓库的历史实际发生过的事情（记录的是第一版原有状态）
rebase：对仓库中发生过的事情进行反复修订后的整洁的版本（记录整理后的状态，而非第一版草稿）

2. 撤销提交不同
撤销merge操作：直接使用revert命令进行撤销
撤销rebase操作：使用rebase -i对提交进行重新编辑，（不能使用revert是因为rebase已经没有merge commit了）
