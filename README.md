# WeFlow Focus

一个仅在本机运行的 Windows 白名单群聊监控器。WeFlow 6.1.0 负责读取微信并通过 SSE 推送消息，本应用负责干净展示、关键词提醒和 OpenAI 兼容接口的周期摘要。

## 功能

- 从 WeFlow API 读取群聊并建立关注白名单
- SSE 断线自动重连，按 `event + rawid` 去重
- 仅保存关注群消息，关键词命中时发出 Windows 通知
- 支持 OpenAI 兼容 `/chat/completions` 接口
- 定时或手动生成交易信息摘要
- Token 与 AI Key 使用 Electron `safeStorage` 加密保存
- 原始消息自动按保留天数清理
- 最小化到系统托盘、可选随 Windows 启动

## 使用前准备

1. 启动微信和 WeFlow。
2. 在 WeFlow 设置中开启 HTTP API、主动推送和推送白名单。
3. 地址保持 `127.0.0.1`，默认端口 `5031`。
4. 生成 Access Token。

## 应用内设置

1. 填写 WeFlow API 地址和 Access Token。
2. 点击“测试连接”。
3. 点击“读取群聊”，勾选关注群。
4. 填写关键词。
5. 如需 AI 摘要，填写兼容 OpenAI 的 API 地址、API Key 和模型名称。
6. 点击“保存并连接”。

## 本地开发

```bash
npm install
npm start
```

## 构建 Windows 安装包

### 在 Windows 本机

```powershell
npm install
npm run dist:win
```

安装包输出到 `dist`。

### 使用 GitHub Actions

将本目录上传到 GitHub 仓库，打开 Actions，运行 `Build Windows Installer`，完成后下载 `WeFlow-Focus-Windows-Installer` 构建产物。

## 隐私说明

- 应用仅连接 `127.0.0.1` 上的 WeFlow。
- 只有应用内勾选的群会被保存和分析。
- 不会主动上传图片、语音、视频或文件。
- 开启 AI 摘要后，摘要周期内的白名单群文字会发送给用户配置的 AI 服务商。
- 本应用不会将 AI 输出视为交易建议。
