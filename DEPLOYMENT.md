# FISI 计算器 - 部署指南

本文档详细说明如何将FISI计算器部署到各种平台。

## 📋 部署前准备

确保你的项目包含以下文件：

```
fisi-calculator/
├── index.html          # 主页面 ✓
├── data/
│   └── foods.json      # 食物数据 ✓
├── README.md           # 项目说明 ✓
├── .gitignore         # Git忽略文件 ✓
└── vercel.json        # Vercel配置 ✓
```

## 🚀 部署方法

### 方法1：GitHub Pages（推荐）

#### 步骤1：创建GitHub仓库

1. 登录 [GitHub](https://github.com)
2. 点击右上角 "+" → "New repository"
3. 填写仓库信息：
   - Repository name: `fisi-calculator`
   - Description: `食物炎症指数评估工具`
   - Public（公开）
4. 点击 "Create repository"

#### 步骤2：上传文件

**方法A：使用Git命令行**

```bash
# 初始化Git仓库
git init

# 添加所有文件
git add .

# 提交
git commit -m "Initial commit: FISI Calculator"

# 添加远程仓库
git remote add origin https://github.com/your-username/fisi-calculator.git

# 推送到GitHub
git branch -M main
git push -u origin main
```

**方法B：使用GitHub网页上传**

1. 在仓库页面点击 "uploading an existing file"
2. 拖拽所有文件到页面
3. 点击 "Commit changes"

#### 步骤3：启用GitHub Pages

1. 进入仓库的 "Settings"
2. 左侧菜单找到 "Pages"
3. Source 选择 "Deploy from a branch"
4. Branch 选择 "main" 和 "/ (root)"
5. 点击 "Save"
6. 等待几分钟，页面会显示访问链接

#### 访问地址

```
https://your-username.github.io/fisi-calculator/
```

---

### 方法2：Vercel（最快）

#### 步骤1：准备Vercel账号

1. 访问 [Vercel](https://vercel.com)
2. 使用GitHub账号登录

#### 步骤2：部署项目

**方法A：从GitHub导入**

1. 点击 "Add New..." → "Project"
2. 选择你的GitHub仓库 `fisi-calculator`
3. 点击 "Import"
4. 保持默认设置，点击 "Deploy"
5. 等待部署完成（约1-2分钟）

**方法B：直接上传**

1. 点击 "Add New..." → "Project"
2. 选择 "Deploy from template" 或直接拖拽文件夹
3. 上传整个项目文件夹
4. 点击 "Deploy"

#### 访问地址

```
https://fisi-calculator.vercel.app
或
https://your-project-name.vercel.app
```

#### 自定义域名（可选）

1. 在项目设置中找到 "Domains"
2. 添加你的域名
3. 按照提示配置DNS记录

---

### 方法3：Netlify

#### 步骤1：准备Netlify账号

1. 访问 [Netlify](https://www.netlify.com)
2. 使用GitHub账号登录

#### 步骤2：部署项目

**方法A：从GitHub导入**

1. 点击 "Add new site" → "Import an existing project"
2. 选择 "GitHub"
3. 选择你的仓库 `fisi-calculator`
4. 保持默认设置，点击 "Deploy site"

**方法B：拖拽部署**

1. 点击 "Add new site" → "Deploy manually"
2. 直接拖拽整个项目文件夹
3. 自动部署完成

#### 访问地址

```
https://random-name.netlify.app
```

可以在设置中修改为自定义子域名。

---

### 方法4：自己的服务器

#### 使用Nginx

1. 上传文件到服务器：

```bash
scp -r fisi-calculator/ user@your-server:/var/www/
```

2. 配置Nginx：

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/fisi-calculator;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # 启用Gzip压缩
    gzip on;
    gzip_types application/json text/css application/javascript;
}
```

3. 重启Nginx：

```bash
sudo nginx -t
sudo systemctl restart nginx
```

#### 使用Apache

1. 上传文件到服务器

2. 配置Apache：

```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /var/www/fisi-calculator

    <Directory /var/www/fisi-calculator>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

3. 重启Apache：

```bash
sudo systemctl restart apache2
```

---

## 🔧 部署后配置

### 启用HTTPS

#### GitHub Pages
- 在仓库设置的Pages页面勾选 "Enforce HTTPS"

#### Vercel/Netlify
- 自动提供HTTPS，无需配置

#### 自己的服务器
使用Let's Encrypt：

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

### 性能优化

#### 1. 启用Gzip压缩

大多数平台自动启用，如果使用自己的服务器，确保配置了Gzip。

#### 2. 使用CDN

- **Cloudflare**: 免费CDN，提升全球访问速度
- **jsDelivr**: 用于CDN加速静态资源

#### 3. 缓存策略

在服务器配置中添加缓存头：

```nginx
location ~* \.(json)$ {
    expires 1d;
    add_header Cache-Control "public, immutable";
}
```

---

## 📊 监控和分析

### Google Analytics

在 [`index.html`](../index.html) 的 `</head>` 前添加：

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Vercel Analytics

在Vercel项目设置中启用Analytics功能。

---

## 🐛 常见问题

### Q: 部署后显示404错误
A: 检查：
- 文件路径是否正确
- `index.html` 是否在根目录
- `data/foods.json` 是否存在

### Q: JSON数据加载失败
A: 检查：
- 浏览器控制台的错误信息
- JSON文件路径是否正确（应该是 `./data/foods.json`）
- 服务器是否正确配置MIME类型

### Q: GitHub Pages显示空白页面
A: 
- 等待几分钟让部署完成
- 检查浏览器控制台错误
- 确认所有文件都已上传

### Q: 如何更新部署的网站？
A: 
- **GitHub Pages**: 推送新代码到仓库即可
- **Vercel/Netlify**: 推送到GitHub或重新部署
- **自己的服务器**: 重新上传文件

---

## 📝 部署检查清单

部署前确认：

- [ ] 所有文件已准备好
- [ ] `data/foods.json` 文件存在且大小正常（约1.2MB）
- [ ] [`index.html`](../index.html) 中的路径都是相对路径
- [ ] 测试本地运行正常
- [ ] 已创建Git仓库（如果使用GitHub Pages）
- [ ] 已准备好部署平台账号

部署后检查：

- [ ] 网站可以正常访问
- [ ] 搜索功能正常
- [ ] 可以添加食物
- [ ] FISI计算正确
- [ ] 移动端显示正常
- [ ] HTTPS已启用
- [ ] 性能表现良好

---

## 🎉 部署成功！

恭喜！你的FISI计算器已成功部署。

### 下一步

1. 分享你的网站链接
2. 收集用户反馈
3. 持续改进功能
4. 考虑添加更多功能

### 需要帮助？

- 查看 [README.md](../README.md)
- 提交 [Issue](https://github.com/your-username/fisi-calculator/issues)
- 查看平台官方文档

---

**祝你部署顺利！** 🚀
