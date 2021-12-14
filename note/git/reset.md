# Git reset

## 撤回 commit

当commit之后还没有push

```bash
git reset --mixed <commit_id>
```

* `--soft`  保留源码,只回退到commit信息到某个版本.不涉及index的回退,如果还需要提交,直接commit即可.
* `--mixed` 会保留源码,只是将git commit和index 信息回退到了某个版本.
* `--hard` 源码也会回退到某个版本,commit和index 都会回退到某个版本.(注意,这种方式是改变本地代码仓库源码)