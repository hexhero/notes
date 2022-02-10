# Git reset

## 撤回 commit

当commit之后还没有push

```bash
git reset --mixed <commit_id>
```

* `--soft`  保留源码,只回退到commit信息到某个版本.不涉及index的回退,如果还需要提交,直接commit即可.
* `--mixed` 会保留源码,只是将git commit和index 信息回退到了某个版本.
* `--hard` 源码也会回退到某个版本,commit和index 都会回退到某个版本.(注意,这种方式是改变本地代码仓库源码)

## 撤回 reset

当需要撤回reset的时候,reflog 就是用来解决这个问题的.

```sh
$ git reflog
5e972cff (HEAD -> hotfix) HEAD@{0}: reset: moving to 5e972cff
041c2e33 (origin/INT) HEAD@{1}: reset: moving to 041c2e330a0c9cf563330261b769871baf87abb3
041c2e33 (origin/INT) HEAD@{2}: reset: moving to 041c2e330a0c9cf563330261b769871baf87abb3
5e972cff (HEAD -> hotfix) HEAD@{3}: commit: 1.53/hotfix 4/MB-14629
756bdf90 (origin/hotfix) HEAD@{4}: commit: 1.53/hotfix 4/MB-14629
```

回到最后一次提交的位置
```sh
git reset 5e972cff
```