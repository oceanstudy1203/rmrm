# 部署计划

## 项目类型

当前项目是纯静态站点，没有构建步骤。

可部署到：

- Cloudflare Pages。
- Vercel。
- GitHub Pages。
- 其他支持静态文件托管的平台。

## GitHub 仓库

当前目标仓库：

```text
oceanstudy1203/rmrm
```

提交前应先检查工作区，避免把无关文件混入提交。

## 部署前检查

部署前确认：

- `index.html` 可以访问。
- `tingting.html` 可以访问。
- `notes.html` 可以访问。
- `notes/why-parent-english-player.html` 可以访问。
- `about.html` 可以访问。
- CSS 和 favicon 路径正确。
- 产品页网盘链接是真实地址。
- 邮箱为 `runmu@rmrm.me`。
- 没有站内隐私页和支持反馈页的旧入口。
- 没有 `href="#"`、`链接待替换`、`待补充`。

## 本地验证

使用：

```powershell
python -m http.server 8080 --bind 127.0.0.1
```

访问：

```text
http://127.0.0.1:8080/
```

至少检查以下路径返回 200：

```text
/index.html
/tingting.html
/notes.html
/notes/why-parent-english-player.html
/about.html
/assets/css/style.css
/assets/images/favicon.svg
```

## URL 建议

上线后主要 URL：

```text
https://rmrm.me/
https://rmrm.me/tingting.html
https://rmrm.me/notes.html
https://rmrm.me/notes/why-parent-english-player.html
https://rmrm.me/about.html
```

如果部署平台支持无后缀路由，可以后续再做重写规则。当前静态文件以 `.html` 路径可访问为准。

## 隐私与反馈

网站不再部署独立 `privacy.html` 和 `support.html`。

- 隐私政策由 App 在其他位置调取。
- 反馈表在 App 内已有入口。
- 网站公开联系邮箱：`runmu@rmrm.me`。

## 后续可能需要

如果未来增加统计、表单、下载计数、后台或用户系统，必须重新评估隐私政策、数据收集说明和部署架构。当前版本不需要服务器、数据库或对象存储。
