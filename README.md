# LitePan - LazyCat App

[LitePan](https://github.com/Ponphil/LitePan)（多网盘聚合挂载：WebDAV、STRM、媒体整理）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`docker.io/ponphil/litepan` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（`v*.*.*-beta` 格式，`channel: beta`），发现新版本自动更新版本号与镜像、构建 LPK、发布商店（包版本号取 prerelease 前的三段，如 `0.5.7`）。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 配置

- 三数据卷：`data`（应用数据）、`strm`（STRM 输出）、`mounts`（本地挂载点）
- **FUSE 挂载**：声明 `fuse.mount` 权限（lzcos v1.6.1+ 注入 fusermount3），`min_os_version: 1.6.1`
- 磁力下载端口 42069 TCP/UDP 通过 `application.ingress` 暴露
- 首次打开：默认管理员账号/密码均为 `admin`，登录后请立即修改
- 健康检查 `/health`

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |
