# 养老助手网页版部署指南

## 本地开发环境配置

1. 安装 Node.js
   - 访问 [Node.js 官网](https://nodejs.org/)
   - 下载并安装 Node.js 18.x 或更高版本

2. 克隆项目
   ```bash
   git clone <项目仓库地址>
   cd shijiazhuang-elderly-care
   ```

3. 安装依赖
   ```bash
   npm install
   ```

4. 启动开发服务器
   ```bash
   npm run dev
   ```
   启动后可以在浏览器访问 http://localhost:3000 查看项目

## GitHub Pages 部署步骤

1. 创建 GitHub 仓库
   - 在 GitHub 上创建新仓库或使用现有仓库
   - 确保仓库是公开的（public）

2. 推送代码到 GitHub
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

3. 自动部署
   - 项目已配置 GitHub Actions 自动部署
   - 每次推送到 main 分支时会自动触发部署
   - 部署过程包括：
     1. 安装依赖
     2. 构建项目
     3. 部署到 gh-pages 分支

4. 查看部署状态
   - 访问仓库的 Actions 标签页查看部署进度
   - 部署完成后，访问 Settings > Pages 确认部署设置
   - 确保 Source 选择为 gh-pages 分支

5. 访问网站
   - 部署成功后可以通过以下地址访问：
   - https://<用户名>.github.io/shijiazhuang-elderly-care/

## 注意事项

- 确保 package.json 中的依赖版本正确
- 本地测试通过后再推送到 GitHub
- 如遇部署问题，查看 Actions 日志排查原因