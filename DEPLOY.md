# 项目部署指南

## 最简单的部署方式

### 1. 构建生产版本

```bash
npm run build
```

构建完成后，会在项目根目录生成 `dist` 文件夹，包含所有静态文件。

### 2. 部署到静态服务器

#### 方式一：使用 Vercel（推荐，最简单）

1. 访问 [Vercel](https://vercel.com)
2. 使用 GitHub/GitLab/Bitbucket 账号登录
3. 点击 "New Project"
4. 导入你的项目仓库
5. 配置：
   - Framework Preset: `Vite`
   - Build Command: `npm run build`
   - Output Directory: `dist`
6. 点击 "Deploy" 即可

#### 方式二：使用 Netlify

1. 访问 [Netlify](https://www.netlify.com)
2. 使用 GitHub 账号登录
3. 点击 "Add new site" -> "Import an existing project"
4. 选择你的仓库
5. 配置：
   - Build command: `npm run build`
   - Publish directory: `dist`
6. 点击 "Deploy site"

#### 方式三：使用 GitHub Pages

1. 安装 gh-pages：
```bash
npm install --save-dev gh-pages
```

2. 在 `package.json` 中添加脚本：
```json
{
  "scripts": {
    "deploy": "npm run build && gh-pages -d dist"
  }
}
```

3. 在 `vite.config.ts` 中添加 base 配置：
```typescript
export default defineConfig({
  base: '/你的仓库名/',
  // ... 其他配置
})
```

4. 部署：
```bash
npm run deploy
```

#### 方式四：使用传统服务器（Nginx）

1. 将 `dist` 文件夹内容上传到服务器
2. 配置 Nginx：
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/dist;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

3. 重启 Nginx：
```bash
sudo nginx -s reload
```

### 3. 注意事项

- 确保所有环境变量都已配置
- 检查 `dist` 文件夹中的文件是否完整
- 如果使用路由，确保服务器配置了 SPA 回退到 `index.html`
- 建议启用 HTTPS

### 4. 验证部署

访问部署后的 URL，检查：
- 页面是否正常加载
- 所有功能是否正常
- 控制台是否有错误

