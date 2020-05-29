# commit-message
写出好的commit message
引用自 https://ruby-china.org/topics/15737
# 基本要求
- 第一行应该少于 50 个字。 随后是一个空行 第一行题目也可以写成：Fix issue #8976
- 喜欢用 vim 的哥们把下面这行代码加入 .vimrc 文件中，来检查拼写和自动折行
> autocmd Filetype gitcommit setlocal spell textwidth=72
- 永远不在 git commit 上增加 -m <msg> 或 --message=<msg> 参数，而单独写提交信息
> 一个不好的例子 git commit -m "Fix login bug"
>> 一个推荐的 commit message 应该是这样： Redirect user to the requested page after login https://trello.com/path/to/relevant/card Users were being redirected to the home page after login, which is less
useful than redirecting to the page they had originally requested before
being redirected to the login form.
Store requested path in a session variable
Redirect to the stored location after successfully logging in the user
> 注释最好包含一个连接指向你们项目的 issue/story/card。一个完整的连接比一个 issue numbers 更好
> 提交信息中包含一个简短的故事，能让别人更容易理解你的项目
# 注释要回答如下信息
### 为什么这次修改是必要的？
### 如何解决的问题？
### 这些变化可能影响哪些地方？
# 小提示
- 使用 fix, add, change 而不是 fixed, added, changed
- 永远别忘了第 2 行是空行
- 用 Line break 来分割提交信息，让它在某些软件里面更容易读
- 请将每次提交限定于完成一次逻辑功能。并且可能的话，适当地分解为多次小更新，以便每次小型提交都更易于理解
# 例子
```
Fix bug where user can't signup.

[Bug #2873942]

Users were unable to register if they hadn't visited the plans
and pricing page because we expected that tracking
information to exist for the logs we create after a user
signs up.  I fixed this by adding a check to the logger
to ensure that if that information was not available
we weren't trying to write it.
```
```
Redirect user to the requested page after login

https://trello.com/path/to/relevant/card

Users were being redirected to the home page after login, which is less
useful than redirecting to the page they had originally requested before
being redirected to the login form.

* Store requested path in a session variable
* Redirect to the stored location after successfully logging in the user
```
# 依赖 Github Issue 的 Commit message 格式
这种工作方式期望团队使用 Github 的 Project 和 Issue 来管理开发任务。这时 Commit message 的 Header 部分应该包含 Issue Number。
```
[#123] Diverting power from warp drive to torpedoes
[Closes #123] Torpedoes now sufficiently powered
[Closes #123][#124][#125] Torpedoes now sufficiently powered
```
# Message Template
```
[<optional state> #issueid] (50 chars or less) summary of changes

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, preceded by a
single space, with blank lines in between, but conventions vary here
```
# Angular 规范的 Commit message 格式
每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。
```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
其中，Header 是必需的，Body 和 Footer 可以省略。
#### Header
Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）
type 用于说明 commit 的类别，只允许使用下面 7 个标识
- feat 新功能（feature）
- fix 修补 bug
- docs 文档（documentation）
- style 格式（不影响代码运行的变动）
- refactor 重构（即不是新增功能，也不是修改 bug 的代码变动）
- test 增加测试
- chore 构建过程、辅助工具的变动
- perf 提高性能
如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中
scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同
subject 是 commit 目的的简短描述，不超过 50 个字符
- 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
- 第一个字母大写
- 结尾不加句号
### Body
Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例
```
More detailed explanatory text, if necessary.  Wrap it to
about 72 characters or so.

Further paragraphs come after blank lines.

-Bullet points are okay, too
-Use a hanging indent  
```
应该说明代码变动的动机，以及与以前行为的对比，参考前文提到的 注释要回答如下信息
### Footer
Footer 部分只用于不兼容变动和关闭 Issue
```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```
```
Closes #123, #245, #992
```
