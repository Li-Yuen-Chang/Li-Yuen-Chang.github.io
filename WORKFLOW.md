# 博客更新工作流程

## 关于部署和版本控制的说明

在使用 Hexo 博客系统时，我们实际上在处理两个不同的内容：

1. 源文件
   - 包含你的 Markdown 文章、配置文件、主题等
   - 这些文件通常保存在 main/master 分支
   - 使用 `git push` 来管理这些源文件

2. 生成的静态网站文件
   - 通过 `hexo generate` 生成的静态 HTML 文件
   - 这些文件通过 `hexo deploy` 部署到 gh-pages 分支
   - 用于实际展示的网站内容

因此，`hexo deploy` 和 `git push` 实际上是操作不同的分支，不会产生冲突：
- `hexo deploy` 只更新 gh-pages 分支（或者你配置的部署分支）
- `git push` 更新 main/master 分支（源文件）

## 本地更新博客内容

1. 在本地编写新的博客文章
   ```bash
   # 进入博客目录
   cd blog
   
   # 创建新的文章
   hexo new post "文章标题"
   ```

2. 编辑文章内容
   - 文章位于 `source/_posts` 目录下
   - 使用 Markdown 格式编写内容
   - 可以在文章头部设置标签、分类等信息

3. 本地预览
   ```bash
   # 启动本地服务器
   hexo server
   ```
   访问 `http://localhost:4000` 预览效果

## 同步到 GitHub

1. 生成静态文件
   ```bash
   # 清理之前的构建文件
   hexo clean
   
   # 生成新的静态文件
   hexo generate
   ```

2. 部署到 GitHub Pages
   ```bash
   # 部署到 GitHub
   hexo deploy
   ```

3. 保存源文件更改
   ```bash
   # 添加更改的文件
   git add .
   
   # 提交更改
   git commit -m "更新: 添加新文章"
   
   # 推送到 GitHub
   git push origin main
   ```

## 推荐的更新流程

为了确保源文件和部署的网站都正确更新，建议按以下顺序操作：

1. 更新博客内容
   ```bash
   # 编写新文章或修改内容
   hexo new post "新文章"
   
   # 本地预览
   hexo server
   ```

2. 部署网站
   ```bash
   # 生成并部署静态文件到 gh-pages 分支
   hexo clean
   hexo generate
   hexo deploy
   ```

3. 保存源文件
   ```bash
   # 将源文件的更改推送到 main 分支
   git add .
   git commit -m "更新: 添加新文章"
   git push origin main
   ```

这样的顺序可以确保：
- 网站内容正确更新
- 源文件得到备份
- 避免任何分支间的冲突

## 注意事项

1. 确保 `_config.yml` 中的部署配置正确：
   ```yaml
   deploy:
     type: git
     repo: [你的 GitHub 仓库地址]
     branch: gh-pages
   ```

2. 首次部署前确保已安装部署插件：
   ```bash
   npm install hexo-deployer-git --save
   ```

3. 确保本地 git 配置正确且已登录 GitHub

## 常见问题解决

1. 如果部署失败，检查：
   - GitHub 仓库权限设置
   - 本地 SSH key 配置
   - 网络连接状态

2. 如果预览显示异常，可以尝试：
   ```bash
   hexo clean
   hexo generate
   hexo server
   ```

3. 保持主题更新：
   ```bash
   git submodule update --remote
   ``` 