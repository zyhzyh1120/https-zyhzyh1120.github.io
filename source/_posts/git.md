---
title: Git
date: 2022-11-21 19:01:27
tags: Git
categories: Git
excerpt: git 随笔
---

## Git 常用命令速查

### 常用命令

```bash
git branch -r  // 查看远程所有分支

git revert [commit_id]   // 撤销某次操作，此次操作之前和之后的 commit 和 history 都会保留
git revert HEAD          //撤销倒数第一次提交
git revert HEAD^         //撤销倒数第二次提交
git revert HEAD~2        //撤销倒数第三次提交

// 创建本地分支并关联
git checkout -b 本地分支 origin/远程分支
git branch --set-upstream-to origin/远程分支名 本地分支名      //已有本地分支创建关联
git pull // 拉取


// 验证github秘钥
ssh -T git@github.com
```

### 版本回退

```bash
git revert ：撤销某次操作
git reset <hash>：是撤销某次提交，但是此次之后的修改都会被退回到暂存区。除了默认的 mixed 模式，还有 soft 和 hard 模式。
git reset --soft ：回退到某个版本，只回退了 commit 的信息，不会恢复到 index file 一级。如果还要提交，直接 commit 即可；
git reset --hard ： 彻底回退到某个版本，本地的源码也会变为上一个版本的内容，撤销的 commit 中所包含的更改被冲掉；

1. 当代码已经 commit 但没有 push 时，可使用如下命令操作：
   git revert HEAD //撤销倒数第一次提交
   git revert HEAD^ //撤销倒数第二次提交
   git revert HEAD~2 //撤销倒数第三次提交

   git revert [commit_id] // 比如：fa042ce57ebbe5bb9c8db709f719cec2c58ee7ff）撤销指定的版本，撤销也会作为一次提交进

2. 当代码已经 commit 并 push 时，可使用如下命令：
   git revert HEAD~1 //代码回退到前一个版本

# 注意: 当回退有冲突时，需手动合并冲突并进行修改，再 commit 和 push。
# 这相当于增加了一次新的提交并且版本库中有记录。
  git reset --soft 和 git reset --hard
  git reset –-soft
```

- 回退到某个版本，只回退了 commit 的信息，不会恢复到 index file 一级；如果还要提交，直接 commit 即可；
  - 如果是为了版本回退，本地低于线上版本则需要加 --force
  - git push origin 分支 --force // ok，大功告成

## 补充

```bash
git reset -–hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容，撤销的 commit 中所包含的更改被冲掉，接着推送就可以了；
// 参数 --soft 指的是：保留当前工作区，以便重新 commit。
// 参数 --hard 指的是：不保留工作区，丢弃代码
// 然后 git reset HEAD 就回退成功了

// 如果是为了版本回退，本地低于线上版本则需要加 --force
git push origin 分支 --force // ok，大功告成

// 删除指定的 commits，需要执行变基操作，在多人协作的项目中，不推荐对已推送到远程仓库的内容进行变基操作
交互式的变基简介
在 rebase 命令中加入 -i 或 --interactive 参数，在交互模式下完成
交互模式会将指定的 commit 后的所有提交列出，行格式：(action) (partial-sha) (short commit message)
你可以上下移动这些行从而对提交进行重排序。当你退出编辑器时，git 会按照你指定的顺序去应用提交，并且做出相应的操作（action）。
操作(action)说明
edit：使用 commit，但是暂停以便进行修正
squash：使用 commit，但是把它与前一次 commit 合并
pick：使用 commit
drop：移除 commit
git rebase -i origin/master 会将最后一次从 origin 仓库拉取或者向 origin 推送之后的所有提交列出。

1. 首先使用 git log 命令找到需要删除的 commit 版本的前一次 commit 的 commit_id
2. 进入交互模式，进入后不会列出当前版本
3. git rebase -i [commit_id]
4. 进入编辑模式，将第一行（即你需要删除的 commit）前的操作符修改为 drop
5. 修改完成后，退出编辑模式然后保存 :wq

## git 提交日志规范
- feat：新功能（feature）
- fix：修补 bug
- docs：文档（documentation）
- style： 不影响代码运行的变动（css，空格，格式，缺少分号等）
- refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动，对构建过程或辅助工具和库（如文档生成）的更改
- build： 源码构建配置文件的变动
- test： 添加缺失或更正现有测试 ，单元（集成）测试的源码提交
- revert: 代码还原的变动
- ci: 持续集成工具的变动
- perf: 代码更改可提高性能，软件性能分析工具的变动
- [^可单个或多个标识组合使用：]: 例：fix+style(_): 修改了去除定位偏移的 bug+背景样式修改
scope
用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同，逗号分隔。
说明哪个模块受到影响，子模块斜杠分割，多个模块逗号分隔。
例：feat(品牌大全/列表页，新机大全/详情页，某个模块名)：添加 xxx
例：feat(.eslintrc.js,某个单文件文件名)：更新 xx 配置
当更改影响多个范围时，您可以使用_。
例：feat(\*): 更新远端 dev 仓库代码
subject
是 commit 目的的简短描述，不超过 50 个字符。
开头请使用： 添加 xxx 移出(清空)xxx 升级(更新)xxx 覆盖 xxx 改变 xxx 切换 xxx 为 xxx 修复 xxx
以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
第一个字母小写
结尾不加句号（.）
```

#### 分支说明：

```
dev：开发分支，为未通过测试最新代码源
pre: 预发布环境, 为部署生产最后调整
master：生产环境，为部署线上正式环境代码源
合并代码过程中，有冲突需先解决冲突部分代码。
合并代码完成，检查两个文件与分支说明是否对应：
```

#### 本地运行

1.安装 node.js
2.npm install
3.npm run serve
手动构建(打包)流程
开发环境 npm run dev 测试环境 npm run test 开发环境 npm run prod 以上所有构建流程之前先配置好(.gitlab-ci.yml)打包环境
