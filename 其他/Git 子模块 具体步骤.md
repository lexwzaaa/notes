## Git 子模块 具体步骤

### 步骤 1: 创建子项目仓库

如果还没有子项目仓库，首先需要在 GitHub 上创建一个新的仓库：

**1**.	登录到 GitHub。

**2**.	点击右上角的 ”+” 按钮，选择 “New repository”。

**3**.	填写仓库名称和其他信息，然后点击 “Create repository”。

### 步骤 2: 在主项目中添加子模块

在你已有的主项目仓库中执行以下步骤：

**1**. 导航到主项目的本地目录：

```sh
cd /path/to/your/main-project
```

**2**. 添加子模块：

使用以下命令将子项目仓库添加为子模块。将 <子项目仓库的URL> 替换为你刚刚创建的子项目仓库的 URL（可以在 GitHub 仓库页面找到）：

```sh
git submodule add <子项目仓库的URL> <子项目文件夹>
```
例如：

```sh
git submodule add https://github.com/username/subproject-repo.git subproject
```

**3**.	初始化子模块（如果是第一次使用）：

```sh
git submodule init
```

**4**.	更新子模块（获取最新的子项目内容）：

```sh
git submodule update
```

### 步骤 3: 提交更改

**1**.	提交对子模块的更改：

添加子模块后，主项目中会生成一个 .gitmodules 文件和指向子项目的引用。你需要将这些更改提交到主项目的仓库：

```sh
git add .gitmodules subproject
git commit -m "Add subproject as a submodule"
```

**2**.	推送到远程仓库：

将更改推送到主项目的远程仓库：

```sh
git push origin main
```

### 步骤 4: 使用和管理子模块

**1**. 更新子模块：要更新子模块到最新版本，可以进入子模块目录并拉取更改：

```sh
cd subproject
git pull origin main
```

**2**.	回到主项目：

```sh
cd ..
```

**3**.	提交子模块更新：
当子模块内容更新时，主项目的引用也会发生变化，记得在主项目中提交这些变化：

```sh
git add subproject
git commit -m "Update subproject"
git push origin main
```

### 总结

#### 通过以上步骤，你可以将一个已经存在的仓库关联到另一个仓库作为子项目，并且保持两个项目的独立性和管理的灵活性。