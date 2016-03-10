## Commit message 格式

每次提交，Commit message 都包括三个部分：`Header`,`Body` 和 `Footer`
```
<type>(<scope>): <subject>// 空一行<body>// 空一行<footer>
```
其中，Header 是必需的，Body 和 Footer 可以省略

### 1  Header
#### 1.1 type
`type` 用于说明 commit 的类别，只允许使用下面7个标识。

- `feat`：新功能（feature）
- `fix`：修补bug
- `refactor`：重构完善（即不是新增功能，也不是修改bug的代码变动）
- `docs`：文档（documentation）
- `style`： 格式（不影响代码运行的变动）
- `test`：增加测试
- `chore`：构建过程或辅助工具的变动




如果`type`为`feat`和`fix`，则该 commit 将出现在 Change log 之中。所以应该保证应用这两个type的提交信息是具有代表性的。

**注：一般情况下，我们都是针对某个功能的完善或者修复一些小BUG，所以常用的 type 还是 `refactor`，切勿在 change log 中出现两个相同的提交内容**

如：新的网站中需要加入登陆的功能，那么应该由我们的前端完成登陆页面后做一个 `feat` 提交，后续的完善和修复bug都是属于 `refactor`了。


#### 1.2 scope

`scope` 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### 1.3 subject

`subject` 是 commit 目的的简短描述，不超过50个字符。

- 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
- 第一个字母小写
- 结尾不加句号（.）

### Example:

```
git commit -m "feat(view): 增加登陆功能"
```


## Commitizen

[`Commitizen`](https://github.com/commitizen/cz-cli) 是一个撰写合格 Commit message 的工具。

安装命令如下:

```
$ npm install -g commitizen
```

然后，在项目目录里，运行下面的命令，使其支持 Angular 的 Commit message 格式。

```
$ commitizen init cz-conventional-changelog --save --save-exact
```
以后，凡是用到 `git commit` 命令，一律改为使用 `git cz`。这时，就会出现选项，用来生成符合格式的 Commit message。


## 生成 Change log

如果你的所有 Commit 都符合 Angular 格式，那么发布新版本时， Change log 就可以用脚本自动生成。

生成的文档包括以下三个部分。

- New features
- Bug fixes
- Breaking changes

每个部分都会罗列相关的 commit ，并且有指向这些 commit 的链接。当然，生成的文档允许手动修改，所以发布前，你还可以添加其他内容。

[`conventional-changelog`](https://github.com/stevemao/conventional-changelog-cli) 就是生成 Change log 的工具，运行下面的命令即可。

```
$ npm install -g conventional-changelog-cli
$ cd my-project
$ conventional-changelog -p angular -i CHANGELOG.md -s
```

上面命令不会覆盖以前的 Change log，只会在`CHANGELOG.md`的头部加上自从上次发布以来的变动。

如果你想生成所有发布的 Change log，要改为运行下面的命令。

```
$ conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

为了方便使用，可以将其写入`package.json` 的 `scripts` 字段。

```
{
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r"
  }
}
```
以后，直接运行下面的命令即可。

```
$ npm run changelog
```
