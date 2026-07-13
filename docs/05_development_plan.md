# 开发计划

## 当前状态

项目已经完成静态网站第一版，不再处于“只写规划文档”的阶段。

当前站点包含：

```text
index.html

tingting.html
notes.html
notes/why-parent-english-player.html
about.html
assets/css/style.css
assets/images/favicon.svg
```

已移除：

```text
privacy.html
support.html
```

原因：隐私政策由 App 在其他位置调取，反馈表在 App 内已有入口。

## 技术原则

继续保持纯静态：

- 不引入前端框架。
- 不引入构建工具。
- 不接数据库。
- 不做登录、支付、评论、社区或后台。
- 不添加无真实目标的按钮。

## 后续开发顺序

后续每次修改建议按小步进行：

1. 先确认本次要改的页面或文档。
2. 阅读相关现有文件。
3. 只修改必要文件。
4. 检查链接、SEO 和移动端可读性。
5. 用静态服务器做本地验证。
6. 提交并推送到 GitHub。

## 本地验证

项目没有构建命令。使用静态服务器作为完整验证：

```powershell
python -m http.server 8080 --bind 127.0.0.1
```

至少访问：

```text
/
/index.html
/tingting.html
/notes.html
/notes/why-parent-english-player.html
/about.html
/assets/css/style.css
/assets/images/favicon.svg
```

## 验收清单

- 所有内部链接有效。
- 每页只有一个 `h1`。
- 每页有独立 title、description、canonical 和 Open Graph 信息。
- 没有 `href="#"`。
- 没有“待补充”“链接待替换”。
- 没有站内反馈表。
- 页面展示公开邮箱 `runmu@rmrm.me`。
- 产品页展示真实网盘链接。
