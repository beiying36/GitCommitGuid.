# Git Commit message 编写指南

## 规范的 Commit message 格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。需要编写多行提交 message 时使用` git commit ` 代替 ` git commit -m "message" `。可以为 git 设置 commit 模板，时刻提醒自己.

每次一个小的改动就是一个 commit ,不要一大堆改动一个 commit ,不然 review 的时候痛苦到死.
这样 review 起来方便 log 写起也简单.

### 设置 git commit 模板方法

1.新建 .gitmessage.txt 文件，编写模板

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

2.设置模板 命令如下:

```
git config commit.template .gitmessage.txt // 当前项目
<!-- git config --global commit.template .gitmessage.txt // 全局设置 -->
```

## Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

type: 用于说明 commit 的类别，只允许使用下面7个标识。如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。

```
feat 新功能（feature）
fix 修补bug

docs 文档（documentation）
style 格式（不影响代码运行的变动）例如改变缩进，增删分号
refactor 重构（即不是新增功能，也不是修改bug的代码变动）
test 添加测试或者修改现有测试
chore 构建过程、辅助工具的变动

perf 提高性能
```

scope: 用于说明 commit 影响的范围，如数据层(model)，视图层(view)，控制层（controller）等。

subject: 是 commit 目的的简短描述，以动词开头,不超过50个字符。使用第一人称现在时，比如 change，而不是 changed 或 changes ,第一个字母大写,结尾不加句号

## Body

Body 部分是对本次 commit 的详细描述，可以分成多行。

## Footer

Footer 部分只用于不兼容变动和关闭 Issue。


## Example

```
feat(search): 增加用户搜索功能

用户反馈，不能搜索用户。增加搜索功能，可以让用户快速定位某一个用户进行关注或其他后续操作

resolves #55
```

## 利用工具规范，检查提交格式

安装 husky 和 commitlint 依赖

```
npm install husky --save-dev
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```

新建并配置 commitlint.config.js 文件

```
module.exports = {
    extends: ['@commitlint/config-conventional']
};
```

配置 package.json 文件, 添加 husky 字段

```
"husky": {
    "hooks": {
      "commit-msg": "commitlint -e $HUSKY_GIT_PARAMS"
    }
  },
```

## 配置 git commit 的提升工具

安装 commitizen 和 cz-conventional-changelog

```
npm install --save-dev commitizen
npm install --save-dev cz-conventional-changelog
```

配置 package.json 文件, 添加如下配置

```
"config": {
    "commitizen": {
        "path": "cz-conventional-changelog"
    }
}
# 在 script 中添加，使用`npm run commit`命令代替`git commit` 可以提示作用
"scripts": {
    "commit": "git-cz"
},
```

提示的详细说明

```
```

## 根据commit消息生成changelog

conventional-changelog 安装

```
npm install -save-dev conventional-changelog-cli
```

配置 package.json 文件, 添加如下配置, `npm run changelog` 生成 CHANGELOG.md

```
"scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
},
```

```
# 不会覆盖以前的 Change log，只会在 CHANGELOG.md 的头部加上自从上次发布以来的变动
$ conventional-changelog -p angular -i CHANGELOG.md -s 

# 生成所有发布的 Change log
$ conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```
