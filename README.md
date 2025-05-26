# 1. 打开 GitHub Token 页面：

👉 https://github.com/settings/tokens

#### 2. 点击 **“Generate new token (classic)”**

#### 3. 设置权限（Scopes）时，请确保勾选以下内容：

- ✅ `repo`（如果你发布的是私有仓库）
- ✅ `write:packages`（发布 npm 包）
- ✅ `read:packages`（安装 npm 包）

记得一定要创建的是          Tokens (classic)  不然会发包不成功

然后创建 **Select scopes**  全部 打勾。

打勾完会生成一个 token

```
ghp_Lg9wpgAaKtcRRx880elDqaI0zxxxxxxxx
```

# 安装 gh_2.73.0_windows_amd64

登录github

```
gh auth login
```

1. 按提示打开浏览器，访问：
   👉 https://github.com/login/device
2. 粘贴刚才的代码，点击“Continue”
3. 登录你的 GitHub 账户并授权 GitHub CLI

要查看你是否已经通过 GitHub CLI 登录了 GitHub，可以在命令行中运行以下命令：

```
gh auth status
```

### 如果你已经登录，会看到类似这样的输出：

```
✓ Logged in to github.com as ygs-code (GitHub username)
✓ Git operations for github.com configured to use https protocol.
✓ Token: *******************
```

### 如果你没有登录，会看到：

```
You are not logged into any GitHub hosts. To log in, run: gh auth login
```

也可以用刚才的token登录。登录完成之后

# 3.新建一个npm 包项目

目录一定要有两个文件

package.json

```
{
  "name": "@ygs-code/test",    #包名称和注册名要对应上
  "version": "1.0.1",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  # 这里必须添加这段
  "publishConfig": {
    "registry": "https://npm.pkg.github.com/"
  },
  
  "author": "",
  "license": "ISC",
  "description": ""
}

```

### 项目根目录中添加 .npmrc 文件

@ygs-code/test        @ygs-code 只是私有报名注册一个命名而已

```
@ygs-code:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=ghp_Lg9wpgAaKtcRRx880elDqaI0zxxxxxxxx
 
```

@ygs-code 是用户名

_authToken= 是刚才创建的token  ghp_Lg9wpgAaKtcRRx880elDqaI0zxxxxxxxx

### 然后运行   npm publish    即可发包

```
 npm publish  
```

### 常见的 NPM 钩子函数（生命周期脚本）

以下是一些常用的 NPM 生命周期钩子：

| 钩子名称           | 触发时机说明                                         |
| ------------------ | ---------------------------------------------------- |
| `preinstall`     | 在依赖安装之前执行                                   |
| `install`        | 安装依赖时执行                                       |
| `postinstall`    | 安装依赖之后执行                                     |
| `preuninstall`   | 卸载包之前执行                                       |
| `uninstall`      | 卸载包时执行                                         |
| `postuninstall`  | 卸载包之后执行                                       |
| `prepublishOnly` | 仅在 `npm publish` 之前执行                        |
| `prepare`        | 在 `install` 和 `publish` 之前都执行，常用于构建 |
| `pretest`        | 在运行 `npm test` 之前执行                         |
| `test`           | 运行测试命令                                         |
| `posttest`       | 测试完成后执行                                       |

### 示例：在 `package.json` 中使用钩子

```
{
  "scripts": {
    "preinstall": "echo '准备安装依赖...'",
    "install": "echo '正在安装依赖...'",
    "postinstall": "echo '依赖安装完成！'",
    "pretest": "echo '准备开始测试...'",
    "test": "node test.js",
    "posttest": "echo '测试完成。'"
  }
}

```

# 4.查看已发的包

https://github.com/users/ygs-code/packages/npm/package/github-pk

[查看包 - GitHub 文档](https://docs.github.com/zh/packages/learn-github-packages/viewing-packages)

[关于 GitHub Packages 的权限 - GitHub 文档](https://docs.github.com/zh/packages/learn-github-packages/about-permissions-for-github-packages#permissions-for-repository-scoped-packages)

# 5.使用包

使用包必须项目中有.npmrc 文件并且 有token

```

@ygs-code:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=ghp_Lg9wpgAaKtcRRx880elDqaI0zxxxxxxxx
 
```

### 安装包

npm i  包名

```
npm i @ygs-code/test
```
