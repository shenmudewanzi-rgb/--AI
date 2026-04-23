# 小程序接入说明

当前工作区已经包含两套手机端小程序骨架：

- `wechat-miniprogram/`：微信小程序
- `alipay-miniprogram/`：支付宝小程序

## 当前能力

- 直接复用“AI圈今日要闻”的日报数据结构
- 适配手机端单页阅读
- 展示今日导读、今日爆点、公众号选题池、全量资讯
- 默认支持本地 mock 数据预览
- 支持切换为远程 HTTPS API

## 先本地预览

先生成最新日报和 mock 数据：

```powershell
.\generate-daily-brief.ps1
.\generate-miniapp-mock.ps1
```

然后：

- 用微信开发者工具打开 `wechat-miniprogram`
- 用支付宝小程序开发者工具打开 `alipay-miniprogram`

即使还没部署远程接口，也能先看到样例数据页面。

## 接远程真实数据

小程序不能访问 `localhost`，正式接入时要做这几步：

1. 把当前 PowerShell 后端部署到一个可公网访问的 HTTPS 域名。
2. 确保该域名能返回：
   - `/api/health`
   - `/api/report/latest`
3. 在：
   - `wechat-miniprogram/utils/config.js`
   - `alipay-miniprogram/utils/config.js`
   中填入 `apiBaseUrl`
4. 在微信/支付宝后台把该 HTTPS 域名加入合法请求域名白名单。

## 你下一步最适合做的事

如果你想真正上架到微信/支付宝生态，建议继续做：

- 把本地 PowerShell API 迁到云函数或正式后端
- 给小程序补原文跳转、分享卡片和订阅消息
- 加“今日一图”“一分钟读懂版”“适合发公众号/视频号”的二次包装
- 接企业微信/飞书/公众号素材库统一分发
