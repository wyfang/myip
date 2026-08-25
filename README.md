# MyIP

自托管的网络诊断工具箱，用一个页面检查 IP、DNS、WebRTC、连通性、路由与浏览器信息。

[在线使用](https://ip.wangyifang.com/) · [上游文档](https://docs.ipcheck.ing/developer/zh) · [English](https://github.com/jason5ng32/MyIP#readme)

## 功能

- 检测 IPv4、IPv6、地理位置、ASN 与上游路径
- 检查 DNS 泄漏、WebRTC、网站与服务可用性
- 提供测速、全球延迟、MTR、DNS、Whois 与封锁测试
- 检查代理规则、浏览器指纹与网络安全项
- 支持 PWA、快捷键、深色模式与多语言

## 部署

Node.js：

```bash
npm install -g pnpm
pnpm install
pnpm run build
pnpm start
```

Docker：

```bash
docker run -d -p 18966:18966 \
  --name myip --restart always \
  jason5ng32/myip:latest
```

服务默认监听 `18966`。IP 地理位置需要配置 MaxMind GeoLite2；使用真实域名时必须设置 `ALLOWED_DOMAINS`，否则非 localhost 请求会返回 `403`。完整环境变量见[上游配置文档](https://docs.ipcheck.ing/developer/reference/zh/environment-variables)。

## 来源与许可

本仓库是 [jason5ng32/MyIP](https://github.com/jason5ng32/MyIP) 的 Fork，依据 [MIT License](./LICENSE) 发布。部署、贡献与安全说明以当前上游文档为准。

上游版权通知为 Copyright © 2026 Jason Ng。该版权与 MIT 条款必须保留；Fork 关系不会把上游版权转移给仓库所有者。

完整归属与适用范围见 [NOTICE](./NOTICE) 与 [LICENSE_SCOPE.md](./LICENSE_SCOPE.md)。
