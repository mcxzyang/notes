### GIT 常用操作

> **场景一.**搬代码ing，突然想git pull一下服务器上的代码。可是本地的改动不想add+commit然后pull，怎么办呢？

- git stash先暂存自己改动的code
- git pull更新服务器上的code
- git stash pop 取出暂存的code



>**场景二**.搬代码ing,突然接到一个线上bug需要修复，怎么办合适呢？

- git config --global --list 先查看git配置信息
- 第三项的值如果不是current,执行命令git config --global push.default current（ 推送当前分支到远程服务器端名字相同的分支）
- git branch repair remotes/origin/master  基于远程主分支新建一个修复bug的本地工作分支
- git checkout repair切换到本地修复bug的分支
- 修复bug完成
- add+commit+pull+push,这样push时git会自动帮你创建一个远程分支和本地repair同名
- 切换到主分支（git checkout master），执行命令git merge repair 合并修复bug的分支（repair）到主分支（master)
- 删除本次修改bug创建的多余分支git branch -d repair(删除本地分支)，git push origin -d repair(删除远程分支)