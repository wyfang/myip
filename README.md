# MyIP

由 Wang Yifang 维护的自托管网络诊断工具箱。它将常用的 IP、DNS、连通性、路由和浏览器隐私检查集中在一个页面中，方便快速判断当前网络环境。

[在线访问](https://ip.wangyifang.com/) · [上游项目](https://github.com/jason5ng32/MyIP) · [上游文档](https://docs.ipcheck.ing/developer/zh)

## 关于这个分支

本仓库是 [jason5ng32/MyIP](https://github.com/jason5ng32/MyIP) 的个人维护分支，主要用于 `ip.wangyifang.com` 的部署和日常维护。

- 保持核心功能与上游兼容
- 根据个人部署环境调整配置和文档
- 定期同步上游的功能、安全更新与问题修复

如需通用产品文档或向原项目贡献代码，请前往[上游仓库](https://github.com/jason5ng32/MyIP)。

## 主要功能

- 检测公网 IPv4、IPv6、地理位置、ASN 和上游网络路径
- 检查 DNS 泄漏、WebRTC 地址暴露及代理规则
- 测试网站连通性、服务状态、全球延迟、网速和 MTR
- 查询 IP、DNS、Whois、MAC 地址及网络封锁情况
- 查看浏览器指纹、匿名性和网络安全检查清单
- 支持 PWA、深色模式、键盘快捷键和多语言界面

## 部署当前分支

运行环境要求：

- Node.js 24 或更高版本
- pnpm（版本由 `package.json` 固定）

```bash
git clone --branch wyfang https://github.com/wyfang/myip.git
cd myip
corepack enable
pnpm install --frozen-lockfile
cp .env.example .env
pnpm build
pnpm start
```

启动后访问 `http://localhost:18966`。前端服务默认监听 `18966`，后端 API 默认监听 `11966`。

### Docker

以下方式会从当前 `wyfang` 分支构建镜像，而不是直接使用上游发布的镜像：

```bash
git clone --branch wyfang https://github.com/wyfang/myip.git
cd myip
cp .env.example .env
docker build -t wyfang/myip:local .
docker run -d \
  --name myip \
  --restart unless-stopped \
  -p 18966:18966 \
  --env-file .env \
  wyfang/myip:local
```

运行前请编辑 `.env` 并完成必要配置。

## 必要配置

部署到真实域名时，至少需要关注以下配置：

```dotenv
ALLOWED_DOMAINS="ip.example.com"
MAXMIND_ACCOUNT_ID="your-account-id"
MAXMIND_LICENSE_KEY="your-license-key"
MAXMIND_AUTO_UPDATE="true"
VITE_SITE_URL="https://ip.example.com"
```

- `ALLOWED_DOMAINS`：允许访问后端 API 的域名；未配置时仅允许 localhost。
- `MAXMIND_ACCOUNT_ID`、`MAXMIND_LICENSE_KEY`：用于下载 IP 地理位置和 ASN 数据。
- `MAXMIND_AUTO_UPDATE`：设为 `true` 后自动更新 MaxMind 数据库。
- `VITE_SITE_URL`：站点的公开访问地址，属于构建时配置，修改后需要重新构建。

其他 API 密钥、日志、安全限制、Sentry 和分享功能均为可选配置，详见[环境变量说明](https://docs.ipcheck.ing/developer/reference/zh/environment-variables)。凭据只应保存在本地 `.env` 或部署平台的 Secret 中，不要提交到仓库。

## 本地开发

```bash
pnpm dev       # 同时启动 Vite 和后端服务
pnpm test      # 运行测试
pnpm build     # 构建生产版本
pnpm check     # 运行测试并构建
```

本仓库只使用 pnpm。提交修改前应确保 `pnpm check` 通过。

## 许可与归属

本项目基于 [MIT License](./LICENSE) 发布。原始项目版权归 Jason Ng 及其贡献者所有；本分支中的原创修改版权归 Wang Yifang 所有。

完整归属信息见 [NOTICE](./NOTICE)，许可适用范围见 [LICENSE_SCOPE.md](./LICENSE_SCOPE.md)。第三方数据、品牌、图标、截图和依赖仍遵循各自的许可条款。
