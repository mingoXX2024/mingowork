# 📦 Mingo 2026 部署指南

## 🎯 打包信息

- **打包时间**: 2026年6月2日
- **打包大小**: 1.23 GB (1264.39 MB)
- **文件数量**: 653个文件
- **状态**: ✅ 已验证完整

## 📂 文件夹结构

```
mingo2026/
├── index.html                    ← 主页面
├── portfolio-*.html              ← 作品集页面 (5个)
├── README.md                     ← 项目说明
├── PACKAGING_INFO.md             ← 打包详情
├── DEPLOYMENT_GUIDE.md           ← 本文档
└── assets/                       ← 资源文件夹
    ├── css/                      ← CSS样式
    ├── js/                       ← JavaScript脚本
    ├── fonts/                    ← 字体文件
    ├── icon/                     ← 图标资源
    ├── images/                   ← 图片资源
    ├── video/                    ← 视频资源
    ├── 模特照片/                ← 模特照片
    ├── 三维动态/                ← 三维动画视频
    ├── 三维静态/                ← 三维静态图片
    ├── 社媒视频/                ← 社交媒体视频
    ├── 产品图片/                ← 产品图片
    ├── AIGC/                     ← AI生成图片
    └── 简历/                     ← 简历PDF文件
```

## 🚀 部署方式

### 方式1: 直接部署（推荐）

1. **上传文件夹**
   - 将整个 `mingo2026` 文件夹上传到服务器
   - 确保保持完整的文件夹结构

2. **配置Web服务器**
   ```
   • Apache: 将mingo2026设置为Document Root
   • Nginx: 配置root指向mingo2026文件夹
   • Node.js: 使用任何静态文件服务（Express、http-server等）
   ```

3. **访问网站**
   - 在浏览器中输入你的域名或服务器地址
   - 例如: `https://yourdomain.com`

### 方式2: 本地测试

1. **使用Python内置服务器**
   ```bash
   cd D:\BaiduSyncdisk\mingo2026
   python -m http.server 8000
   ```
   然后访问: `http://localhost:8000`

2. **使用Node.js http-server**
   ```bash
   cd D:\BaiduSyncdisk\mingo2026
   npx http-server
   ```

3. **直接打开HTML**
   - 双击 `index.html` 在浏览器中打开
   - ⚠️ 某些功能可能受到浏览器安全限制

### 方式3: Docker容器部署

创建 `Dockerfile`：
```dockerfile
FROM nginx:latest
COPY mingo2026 /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## ⚙️ 服务器配置建议

### Nginx 配置示例

```nginx
server {
    listen 80;
    server_name your-domain.com www.your-domain.com;
    
    # 重定向到HTTPS（如需要）
    # return 301 https://$server_name$request_uri;
    
    root /path/to/mingo2026;
    index index.html;
    
    # 缓存静态资源
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 30d;
        add_header Cache-Control "public, immutable";
    }
    
    # SPA路由
    location / {
        try_files $uri /index.html;
    }
}
```

### Apache 配置示例

在 `.htaccess` 中：
```apache
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.html$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.html [L]
</IfModule>
```

## 🔒 安全建议

1. **HTTPS配置**
   - 使用Let's Encrypt免费SSL证书
   - 配置自动HTTPS重定向

2. **安全头设置**
   ```
   X-Content-Type-Options: nosniff
   X-Frame-Options: SAMEORIGIN
   X-XSS-Protection: 1; mode=block
   ```

3. **CORS配置**
   - 根据需要配置跨域资源共享

## 📊 性能优化

1. **启用Gzip压缩**
   ```nginx
   gzip on;
   gzip_types text/plain text/css text/xml text/javascript 
              application/x-javascript application/xml+rss;
   ```

2. **CDN加速**
   - 将 `assets/` 文件夹的媒体文件上传到CDN
   - 在HTML中修改资源路径指向CDN地址

3. **图片优化**
   - 已包含的图片已经过优化
   - 考虑使用WebP格式进行进一步压缩

## 📋 检查清单

部署前请确认：

- [ ] 所有HTML文件存在
- [ ] assets文件夹完整
- [ ] CSS样式正常加载
- [ ] JavaScript脚本正常执行
- [ ] 视频和图片能正常播放/显示
- [ ] 所有链接有效
- [ ] 移动端响应式显示正常
- [ ] 表单提交功能正常（如需要）
- [ ] SEO元标签完整

## 🔧 常见问题排查

### 问题1: 资源加载失败
**原因**: 相对路径不正确
**解决**: 检查 assets 文件夹是否与HTML文件在同级目录

### 问题2: 视频无法播放
**原因**: 服务器未配置视频MIME类型
**解决**: 在服务器配置中添加：
```
video/mp4 mp4
```

### 问题3: 页面样式错乱
**原因**: CSS文件未加载
**解决**: 
- 检查浏览器控制台是否有404错误
- 清空浏览器缓存重新加载

### 问题4: 某些功能无法使用
**原因**: JavaScript错误或路径问题
**解决**:
- 检查浏览器控制台错误信息
- 查看Network标签中是否有失败的请求

## 📞 支持和反馈

如在部署过程中遇到问题，请检查：

1. 文件权限是否正确
2. 服务器是否有足够的磁盘空间
3. 网络连接是否正常
4. 浏览器兼容性（推荐使用最新版Chrome、Firefox、Safari）

## 📝 更新日志

### v2026.06
- ✓ 完整的Mingo作品集网站
- ✓ 5个专业作品集页面
- ✓ 响应式设计
- ✓ 高质量媒体资源
- ✓ 现代化UI设计

---

**打包版本**: mingo2026  
**最后更新**: 2026年6月2日  
**验证状态**: ✅ 已验证完整无错误
