# FISI 计算器

> 食物炎症指数评估工具 - Food-based Inflammatory Score Index Calculator

一个基于Web的FISI计算器，帮助用户评估饮食的炎症指数。支持在9223种食物中进行模糊搜索，实时计算FISI值，并判定促炎或抗炎状态。

## 🌟 在线演示

- **GitHub Pages**: [https://your-username.github.io/fisi-calculator/](https://your-username.github.io/fisi-calculator/)
- **Vercel**: [https://fisi-calculator.vercel.app](https://fisi-calculator.vercel.app)

## ✨ 功能特性

- 🔍 **模糊搜索**: 基于Fuse.js在9223种食物中快速查找
- 📊 **实时计算**: 使用公式 `FISI = Σ(摄入量/100 × FII)` 实时计算
- 🎯 **结果判定**: 
  - FISI > -11.2：促炎（红色标识）
  - FISI < -11.2：抗炎（绿色标识）
- 📱 **响应式设计**: 完美支持桌面和移动设备
- 🎨 **医学科研风格**: 专业、简洁、直观的UI设计
- ⚡ **零构建工具**: 纯HTML/CSS/JavaScript，无需npm或webpack

## 📦 项目结构

```
fisi-calculator/
├── index.html              # 主页面
├── data/
│   └── foods.json          # 9223种食物数据（1.2MB）
├── convert-csv-to-json.js  # 数据转换脚本
├── README.md               # 项目说明
└── .gitignore             # Git忽略文件
```

## 🚀 快速开始

### 方法1：直接使用

1. 克隆或下载本项目
2. 使用本地服务器运行：

```bash
# 使用 Python
python -m http.server 8000

# 使用 Node.js
npx serve

# 使用 PHP
php -S localhost:8000
```

3. 在浏览器中访问 `http://localhost:8000`

### 方法2：部署到GitHub Pages

1. Fork本项目或创建新仓库
2. 上传所有文件到仓库
3. 在仓库设置中启用GitHub Pages
4. 选择分支（通常是main）和根目录
5. 访问 `https://your-username.github.io/repo-name/`

### 方法3：部署到Vercel

1. 访问 [Vercel](https://vercel.com)
2. 导入GitHub仓库或直接拖拽文件夹
3. 自动部署完成
4. 获得免费的HTTPS域名

## 📖 使用说明

### 1. 搜索食物
- 在搜索框中输入食物名称或代码
- 支持英文模糊搜索（如：milk, chicken, rice）
- 自动显示匹配度最高的前10个结果

### 2. 添加食物
- 点击搜索结果中的食物
- 输入摄入量（克）
- 点击"添加到食谱"按钮

### 3. 查看结果
- **FISI总分**: 实时计算显示
- **炎症状态**: 自动判定促炎或抗炎
- **食谱列表**: 查看已添加的所有食物

### 4. 管理食谱
- 点击 ❌ 删除单个食物
- 点击"清空全部"删除所有食物

## 🧮 计算公式

```
FISI = Σ(摄入量/100 × FII)
```

**示例计算**：
- Milk, whole - 200g, FII = -0.0775
- Chicken, breast - 150g, FII = -0.0520

```
食物1贡献值 = 200/100 × (-0.0775) = -0.155
食物2贡献值 = 150/100 × (-0.0520) = -0.078
FISI总分 = -0.155 + (-0.078) = -0.233
```

结果：FISI = -0.233 < -11.2，判定为**抗炎**

## 🛠️ 技术栈

- **前端框架**: 纯HTML/CSS/JavaScript
- **UI框架**: Tailwind CSS (CDN)
- **搜索引擎**: Fuse.js (CDN)
- **数据格式**: JSON
- **部署**: 静态网站托管

## 📊 数据说明

### 数据来源
- 包含9223种食物的FII数据
- 数据来源于FNDDS（Food and Nutrient Database for Dietary Studies）

### 数据字段
- **Food_code**: 食物代码（8位数字）
- **Main_food_description**: 食物描述（英文）
- **FII**: 食物炎症指数
- **FII_score**: FII分数

## 🔧 开发指南

### 重新生成JSON数据

如果需要更新数据，运行转换脚本：

```bash
node convert-csv-to-json.js
```

这将从 `9229种食物的FII值.csv` 生成 `data/foods.json`

### 修改计算公式

在 [`index.html`](index.html:245) 中找到 `handleAddFood` 函数：

```javascript
// 当前公式：FISI = Σ(摄入量/100 × FII)
const contribution = (amount / 100) * selectedFood.FII;
```

### 修改判定阈值

在 [`index.html`](index.html:295) 中找到 `updateDashboard` 函数：

```javascript
const threshold = -11.2;  // 修改此值
```

## 🌐 浏览器兼容性

- ✅ Chrome/Edge 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ 移动浏览器

## 📝 常见问题

### Q: 为什么搜索没有结果？
A: 请确保：
- 输入至少2个字符
- 使用英文关键词（数据库为英文）
- 尝试更通用的关键词

### Q: 数据加载失败怎么办？
A: 请检查：
- `data/foods.json` 文件是否存在
- 使用本地服务器而不是直接打开HTML文件
- 检查浏览器控制台的错误信息

### Q: 可以保存我的食谱吗？
A: 当前版本不支持数据持久化。刷新页面后数据会丢失。

## 🚧 未来计划

- [ ] 数据持久化（LocalStorage）
- [ ] 导出功能（PDF/CSV）
- [ ] 多日记录和趋势分析
- [ ] 营养成分分析
- [ ] 中英文双语支持
- [ ] PWA支持（离线使用）

## 📄 许可证

本项目仅供学习和研究使用。食物数据来源于公开数据库。

## 🤝 贡献

欢迎提交Issue和Pull Request！

## 📧 联系方式

如有问题或建议，请通过以下方式联系：
- 提交 [Issue](https://github.com/your-username/fisi-calculator/issues)
- 发送邮件
- 提交 Pull Request

## 🙏 致谢

- [Tailwind CSS](https://tailwindcss.com/) - UI框架
- [Fuse.js](https://fusejs.io/) - 模糊搜索库
- [FNDDS](https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/food-surveys-research-group/docs/fndds/) - 食物数据来源

---

⭐ 如果这个项目对你有帮助，请给个Star！
