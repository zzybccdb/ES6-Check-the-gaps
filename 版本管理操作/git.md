# git 相关内容学习

使用 githug 进行 git 指令操作, 本次指令说明以在 githug 中出现为主

> git clone https://github.com/Gazler/githug.git

## 1. git 指令说明

- git mv <oldfile> <newfile>
移动或为文件重命名, 已经存在的文件会自动 commit
```bash 
# 实际运行的是这三条指令
$ mv test.txt mydir/
$ git rm test.txt
$ git add mydir
```

- git commit --amend 将当前暂存区（stage/index）内的信息, 补全到之前 commit 的版本库中

- git reset [--soft | --mixed | --hard] [HEAD] [文件名]
    - hard: 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交
    - soft: 用于回退到某个版本
    - mixed(默认): 可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

- git remote :
    - \-v 查看当前远程地址
    - add 添加远程地址
    - remove 删除远程地址

- git blame 查看代码是谁写的

- git checkout 
    - \-b 切换 branch
    - tags/<tag_name>

- git stash 建立一个临时暂存区
    - save <注释内容>
    - pop 将暂存区移回
    - branch 在 stash 的基础上, 建立新分支

- git push <远端仓库地址名> <本地分支名> <远端分支名> 

- git fetch: 远端获取分支, 但是不合并到当前分支. git pull = git fetch + git merge

- git bisect: bisect 二分法, 通过二分法定位是哪一个版本提交引入了错误
    - git bisect start <起始版本号> <结束版本号>
    - 当前版本正确 git bisect good
    - 当前版本错误 git bisect bad

- git reflog 查询所有提交记录, git log 只会输出当前线的提交记录

- git submodule add : 自模块载入
    - git clone https://github.com/username/project-main.git --recurse-submodules 递归克隆自模块到本地
    - 另外一种可行的方式是，在当前主项目中执行：
    ```bash
        git submodule init
        git submodule update
        则会根据主项目的配置信息，拉取更新子模块中的代码。
    ```

- git tag 标签
    > 为当前 commit 版本添加标签, 为当前快照打上一个标注, 便于后期回调, 查找.
    - 创建标签 
        - git tag 标签号
        - git tag -a 标签号
            - -a 创建一个带注释的标签
        - git tag 标签号 指定快照版本

    - 查看已有标签 
        - git tag

    - 删除标签
        - git tag -d 标签号

    - 查看此版本所修改的内容
        - git show 标签号


- git rebase 测试练习
    1. 新建 rebase_test 分支
    2. 新建 rebase 测试文件
    3. 合并分支线，将多条分支线，重整为 1 条
    场景描述: 新需求需要处理, 新建分支, 产生新的 commit. 主线上也进行了更新, 产生了新的 commit. 
    利用 rebase 直接将两条分支合并为一条管理线, 与 merge 不同. 当前情况下 rebase 后只留下一条版本线.

        - 新建分支 rebase_merge_branch, 并且为分支新增加 commit
        - 新建 master commit    
        - 切换至 rebase_merge_branch => 执行 git rebase master
        - 切换回 master, 执行 git merge rebase_merge_branch
        - 支线与主线冲突
            - 解决冲突内容
            - git add 冲突文件
            - git rebase --continue
        - 如有需要可以删除 rebase 后的多余分支 git branch -d 分支名

    4. commit 重命名 git rebase -i commit_id reword
    5. commit 合并 git rebase -i commit_id squash
    6. 可以通过修改 rebase 文档内容, 例如调整结构顺序, 修改 commit 顺序


## 2. git 实际问题解决

- 加入缓存区的问题, 想要在通过 gitignore 忽视它的话, 就需要清空缓存区
```bash
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```

- git 安装完成后修改 eol
```bash 
git config --global core.autocrlf [true | input | false]
```


