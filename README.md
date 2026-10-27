# 浩记 · AI 密钥管家（PWA）

这是一个无需后端的静态 PWA，适合在 iPhone Safari 中使用并添加到主屏幕。

## 功能
- PBKDF2-SHA-256（310,000 次迭代）派生密钥，AES-256-GCM 加密保险箱内容
- 添加、编辑、删除、搜索、复制 API Key
- 加密备份与恢复
- PWA / 基础离线缓存

## 重要安全说明
- 应用代码不会主动上传密钥；数据保存在当前浏览器的 localStorage 中，并以 AES-GCM 加密。
- 这不是经过第三方安全审计的产品。请先用测试密钥验证，不要一开始就存放高权限生产密钥。
- 请牢记主密码并保管加密备份。忘记主密码无法解密数据。
- 清理 Safari 网站数据、换设备或浏览器可能导致本地数据丢失；请定期备份。
- 静态托管仓库只包含应用代码，不要把 API Key 或备份文件提交到 GitHub。
- 通用 API 余额查询/在线测试未实现：不同平台接口、鉴权方式和 CORS 政策不同，需要后续逐个平台适配。
- 建议通过 HTTPS 发布。GitHub Pages 可免费托管公开仓库中的静态站点。

## 用 iPhone 发布（GitHub Pages）
1. 登录 GitHub，在网页创建一个新的 **Public** repository，例如 `haoji-ai-vault`。
2. 进入仓库，点 **Add file → Create new file**。
3. 依次创建并提交这三个文件，内容分别复制自本目录：
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
4. 打开仓库的 **Settings → Pages**。
5. 在 **Build and deployment** 里选择 **Deploy from a branch**，分支选 `main`，目录选 `/(root)`，保存。
6. 等待发布完成，页面会显示 `https://你的用户名.github.io/haoji-ai-vault/`。
7. iPhone Safari 打开该 HTTPS 地址，点分享按钮 → **添加到主屏幕**。

## 数据模型
本机 localStorage key: `haoji-vault-v1`。主密码不存储，只有 salt、加密校验块和加密数据块被保存。
