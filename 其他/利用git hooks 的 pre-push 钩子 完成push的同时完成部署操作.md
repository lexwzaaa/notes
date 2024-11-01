# 利用git hooks 的 pre-push 钩子 完成push的同时完成部署操作

* 编辑 pre-push 钩子：在 .git/hooks 目录下创建或编辑 pre-push 文件，将构建和推送的逻辑写入。

``` sh	
#!/bin/bash
echo "执行 pre-push 钩子..."

# 步骤1: 构建项目
echo "构建项目..."
npm run build

# 检查构建是否成功
if [ $? -ne 0 ]; then
  echo "构建失败，终止 push 操作。"
  exit 1
fi

# 步骤2: 将 dist 部署到另一个仓库
echo "将 dist 部署到目标仓库..."

TARGET_REPO="git@github.com:your-username/your-deploy-repo.git"
TARGET_BRANCH="main"
TEMP_DIR=$(mktemp -d)
cp -r dist/* "$TEMP_DIR"

cd "$TEMP_DIR"
git init
git remote add origin "$TARGET_REPO"
git checkout -b "$TARGET_BRANCH"
git add .
git commit -m "Deploy new build"
git push -f origin "$TARGET_BRANCH"

# 清理临时目录
rm -rf "$TEMP_DIR"

echo "dist 已成功部署到目标仓库。继续执行 push 操作..."

# 返回主仓库目录
cd - > /dev/null

# pre-push 钩子成功完成
exit 0
```

	
* 赋予执行权限：

``` sh
chmod +x .git/hooks/pre-push
```


每次执行 git push 时，该钩子会首先构建项目，若构建成功，则将 dist 文件夹内容部署到目标仓库，接着继续执行主仓库的推送操作。