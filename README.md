# DSH Mobile Community · DSH 移动端社区版

自托管的 DSH Mobile 插件与 Android App 社区版（fork 自 [saya-ch/dsh-mobile](https://github.com/saya-ch/dsh-mobile)，Apache-2.0）。

## 与上游的差异
- 管理面板（移动访问）可经公网域名访问，但所有管理接口都要求有效的 DSH 登录会话
- 不写死任何个人域名或服务器地址；公网入口由你自己的反向代理/远程通道提供
- Android App 使用独立包名 `com.dshmobile.community`，可与社区其他版本并存
- 移动访问面板默认显示「下载最新 Android App」，直接指向本仓库对应版本的 APK，而不是上游 Release 或过期版本

## 安全说明
- `/api/mobile-access/*` 的所有方法都要求有效的 DSH 登录会话；公网访问同样如此。
- 公开分发请使用私有 keystore 签名的 release 构建，不要分发 debug 包。

## 版本
0.6.16-community.3（基于上游 v0.6.16），Android App 1.0.3（versionCode 87）。

- 插件包 SHA-256：`d93d296f7f013ff157f0b6b9cdf6c989a1d046a5b4312d1a998324246c0af608`
- App APK SHA-256：`1fd6d7ae978593fb57a9d27022276a7320cd018f10a4bb70091257dfaa938a53`

## 插件安装
从 [Releases](https://github.com/wond03/dsh-my-mobile/releases/tag/community-v1.0.3) 下载 `dsh-my-mobile-0.6.16-community.3.tgz`，然后安装到你的 DSH profile：
```bash
dsh plugin --profile web add /path/to/dsh-my-mobile-0.6.16-community.3.tgz
```
重启 DSH 后，进入「移动访问」即可看到面板。管理接口需要 DSH 登录会话。
同一个 Release 同时提供 App APK 和插件 tgz；面板顶部的「下载最新 Android App」会直接打开对应的 APK，而不是上游页面。

公网自定义域名（可选）：
```bash
# 在使用 managed 局域网网关时，为证书和配对地址增加该 DNS 名称
Environment=DSH_MOBILE_PUBLIC_HOST=your.domain.example
```
不设置时只使用局域网 IP；也可以用 cpolar/cloudflared/FRP/自有反向代理等远程方式。

如果公网 3443 端口由 nginx 等反向代理占用，让插件只监听回环即可（代理转发到 `127.0.0.1:3443`）：
```ini
Environment=DSH_MOBILE_LISTEN_HOST=127.0.0.1
```
管理接口在公网 DSH 域名下同样可用，但每个请求都要求有效的 DSH 登录会话。

## Android App
- 源码：`apps/mobile/android`
- 最新安装包：[`dsh-community-1.0.3.apk`](https://github.com/wond03/dsh-my-mobile/releases/download/community-v1.0.3/dsh-community-1.0.3.apk)
- 当前版本：**1.0.3（versionCode 87，release 签名）**，包名 `com.dshmobile.community`
- 签名证书 SHA-256：`18:A8:5F:8B:6B:1C:7E:32:BF:8D:02:0B:8F:F6:43:15:5B:4D:D3:CA:1D:E9:9C:D2:7C:F5:99:A3:61:81:B5:63`
- 功能：切回前台自动重连；配对链接先确认再连接；新鲸鱼图标与自适应图标；深浅色配对/设备列表背景；移动端面板默认只显示常用项和 App 下载入口；App 连接页新增「下载新版」入口

## Android 构建
```bash
cd apps/mobile/android
./gradlew :app:assembleDebug   # 调试版，包名 com.dshmobile.community.debug
```
Release 构建需要私有 keystore 环境变量（不要提交到仓库）：
```bash
export DSH_ANDROID_KEYSTORE_FILE=/path/to/release.jks
export DSH_ANDROID_KEYSTORE_PASSWORD=...
export DSH_ANDROID_KEY_ALIAS=...
export DSH_ANDROID_KEY_PASSWORD=...
./gradlew :app:assembleRelease
```
配对链接自动打开需要构建时指定自己的域名；不指定时默认不绑定任何域名，仍可扫码或粘贴配对链接：
```bash
./gradlew :app:assembleRelease -PdshPairHost=your.domain.example
```

## 插件源码
完整插件 TypeScript 源码、构建脚本、测试和 Android 工程在 [`community-source` 分支](https://github.com/wond03/dsh-my-mobile/tree/community-source)。`main` 分支保留已构建的 `lib/` 与发布用 Android 源码。

## 许可
Apache-2.0（继承上游）
