# dsh-my-mobile · 我的DSH移动端

自托管的 DSH Mobile 插件分支（fork 自 [saya-ch/dsh-mobile](https://github.com/saya-ch/dsh-mobile)，Apache-2.0）。

## 与上游的差异
- 管理面板（移动访问）可经公网域名访问，但所有管理接口都要求有效的 DSH 登录会话
- 网关证书自动包含自定义域名 SAN（配对校验端到端自洽）
- 网关监听 127.0.0.1，由外部 TCP 透传（nginx stream）代理公网入口

## 安全说明
- `/api/mobile-access/*` 的所有方法都要求有效的 DSH 登录会话；公网访问同样如此。
- 公开分发请使用私有 keystore 签名的 release 构建，不要分发 debug 包。

## 版本
0.6.15-my.1（基于上游 v0.6.15）

## Android App
- 源码：`apps/mobile/android`
- 最新安装包：[Releases](https://github.com/wond03/dsh-my-mobile/releases)
- 当前版本：1.0.1-my（versionCode 84，debug 签名，包名 `io.github.sayach.dshmobile.debug`）
- 本次更新：新鲸鱼应用图标、Android 自适应图标、深浅色配对/设备列表背景

## 许可
Apache-2.0（继承上游）
