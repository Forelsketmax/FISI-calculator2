# 🚀 GitHub 部署快速指南

## 📦 当前文件夹结构

```
FII筛/
├── index.html          # 主页面 ✓
├── data/
│   └── foods.json      # 食物数据 ✓
├── README.md           # 项目说明 ✓
├── DEPLOYMENT.md       # 详细部署指南 ✓
├── .gitignore         # Git配置 ✓
└── vercel.json        # Vercel配置 ✓
```

## ✅ 准备就绪

所有必要文件已准备完毕，可以直接上传到GitHub！

## 🎯 部署步骤

### 方法1：使用GitHub网页上传（最简单）

1. **创建GitHub仓库**
   - 访问 https://github.com/new
   - Repository name: `fisi-calculator`
   - 选择 Public
   - 点击 "Create repository"

2. **上传文件**
   - 在仓库页面点击 "uploading an existing file"
   - 将 `FII筛` 文件夹中的所有文件拖拽到页面
   - 确保包含 `data` 文件夹及其中的 `foods.json`
   - 点击 "Commit changes"

3. **启用GitHub Pages**
   - 进入仓库的 Settings
   - 左侧菜单找到 Pages
   - Source 选择 "Deploy from a branch"
   - Branch 选择 "main" 和 "/ (root)"
   - 点击 Save
   - 等待几分钟

4. **访问网站**
   ```
   https://your-username.github.io/fisi-calculator/
   ```

### 方法2：使用Git命令行

```bash
# 1. 进入FII筛文件夹
cd FII筛

# 2. 初始化Git仓库
git init

# 3. 添加所有文件
git add .

# 4. 提交
git commit -m "Initial commit: FISI Calculator"

# 5. 添加远程仓库（替换your-username）
git remote add origin https://github.com/your-username/fisi-calculator.git

# 6. 推送到GitHub
git branch -M main
git push -u origin main
```

然后按照方法1的步骤3启用GitHub Pages。

## 🔍 验证清单

上传前确认：
- [ ] `index.html` 文件存在
- [ ] `data/foods.json` 文件存在（约1.2MB）
- [ ] `README.md` 文件存在
- [ ] `.gitignore` 文件存在

上传后确认：
- [ ] 所有文件都已上传
- [ ] `data` 文件夹结构正确
- [ ] GitHub Pages已启用
- [ ] 网站可以正常访问

## ⚠️ 常见问题

### Q: 上传后显示404
A: 等待3-5分钟让GitHub Pages部署完成

### Q: 显示"data/foods.json not found"
A: 确认：
1. `data` 文件夹已上传
2. `foods.json` 在 `data` 文件夹中
3. 文件名大小写正确

### Q: 文件太大无法上传
A: GitHub单个文件限制100MB，`foods.json`约1.2MB，完全没问题

## 🎉 部署成功后

访问你的网站：
```
https://your-username.github.io/fisi-calculator/
```

功能测试：
1. 搜索食物（如：milk）
2. 添加食物并输入摄入量
3. 查看FISI计算结果
4. 测试移动端显示

## 📱 分享你的网站

部署成功后，你可以：
- 分享链接给朋友
- 在社交媒体上发布
- 添加到你的简历或作品集

## 🆘 需要帮助？

- 查看 [DEPLOYMENT.md](DEPLOYMENT.md) 获取详细说明
- 查看 [README.md](README.md) 了解项目功能
- 在GitHub仓库提交Issue

---

**祝你部署顺利！** 🚀
