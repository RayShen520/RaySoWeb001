# 瑞幻智能官网 - RaySo.AI

基于 Vue 3 + Vite 构建的公司官网项目

## 技术栈

- Vue 3 (Composition API)
- Vite
- 纯 CSS（无 UI 框架）

## 项目结构

```
├── src/
│   ├── components/      # 公共组件
│   │   ├── NavBar.vue   # 导航栏
│   │   ├── Footer.vue   # 页脚
│   │   └── Toast.vue    # 提示消息
│   ├── pages/           # 页面组件
│   │   ├── HomePage.vue      # 首页
│   │   ├── ProductsPage.vue  # 产品服务页
│   │   ├── ToolsPage.vue     # 工具下载页
│   │   └── ContactPage.vue   # 联系我们页
│   ├── data/            # 数据文件
│   │   └── tools.js     # 工具数据
│   ├── App.vue          # 根组件
│   ├── main.js          # 入口文件
│   └── style.css        # 全局样式
├── index.html           # HTML 模板
├── package.json         # 项目配置
└── vite.config.js       # Vite 配置
```

## 安装依赖

```bash
npm install
```

## 开发运行

```bash
npm run dev
```

访问 http://localhost:3000

## 构建生产版本

```bash
npm run build
```

构建产物在 `dist` 目录

## 预览生产版本

```bash
npm run preview
```

## 部署

项目可以部署到：
- Netlify（推荐）
- Vercel
- GitHub Pages
- 其他静态网站托管服务

### Netlify 部署步骤

1. 将代码推送到 GitHub
2. 在 Netlify 中连接 GitHub 仓库
3. 构建命令：`npm run build`
4. 发布目录：`dist`
5. 完成部署

## 功能特性

- ✅ 响应式设计（移动端适配）
- ✅ 页面路由切换
- ✅ 工具搜索功能
- ✅ 工具分页显示
- ✅ 联系表单验证
- ✅ Toast 提示消息
- ✅ 平滑滚动动画

## 浏览器支持

- Chrome (最新)
- Firefox (最新)
- Safari (最新)
- Edge (最新)

