# rmrm.me 网站项目说明

`rmrm_me` 是 `rmrm.me` 的静态网站项目，用来承接“润木同学”的个人品牌主页、产品入口和开发记录。

当前网站不是复杂公司官网，也不是内容平台。它的第一版目标是：让用户快速理解润木同学是谁、润木听听是什么、为什么做这个产品，以及后续在哪里阅读开发笔记。

## 当前定位

```text
润木同学的个人品牌主页 + 润木听听产品入口 + 开发笔记
```

品牌关系：

```text
润木同学 = 个人品牌 / 创作者身份
润木听听 = 第一个 App 产品
亲子英语包播放器 = 润木听听的品类说明
rmrm.me = 官方网站 / 可信落点
```

首页主表达：

```text
用 AI，把真实的小需求做成能用的产品。
```

## 当前页面

```text
index.html                         首页

tingting.html                      润木听听产品页
notes.html                         开发笔记列表
notes/why-parent-english-player.html  首篇开发笔记
about.html                         关于润木同学
```

已删除的站内页面：

```text
privacy.html
support.html
```

隐私政策已由 App 在其他位置调取，网站不再维护独立隐私政策页。反馈表也不放在网站里，App 内已有反馈入口。网站公开联系方式为：`runmu@rmrm.me`。

## 技术路线

本项目保持纯静态实现：

```text
HTML
CSS
少量静态资源
```

当前不使用 React、Vue、Next.js、构建工具、数据库、登录系统、支付系统、评论系统或后台管理。

## 目录结构

```text
rmrm_me/
  index.html
  tingting.html
  notes.html
  about.html
  assets/
    css/
      style.css
    images/
      favicon.svg
  notes/
    why-parent-english-player.html
  docs/
    00_project_brief.md
    01_brand_positioning.md
    02_site_structure.md
    03_visual_design_direction.md
    04_page_copywriting.md
    05_development_plan.md
    06_deployment_plan.md
    07_privacy_and_support.md
    08_agent_work_rules.md
  rmrm-homepage-copy.md
  rmrm-website-structure-codex-spec.md
  润木听听开发笔记.md
```

## 资源与链接

- 润木听听网盘下载链接：`https://pan.baidu.com/s/54fekx11pCHH0ssUu3yIpbg`
- 公开邮箱：`runmu@rmrm.me`
- GitHub 仓库：`oceanstudy1203/rmrm`

所有按钮必须指向真实可访问目标。不要在页面中留下 `href="#"`、`链接待替换`、`待补充` 等占位内容。

## 本地预览与检查

项目没有构建步骤。可用静态服务器预览：

```powershell
python -m http.server 8080 --bind 127.0.0.1
```

然后访问：

```text
http://127.0.0.1:8080/
```

每次修改后应检查：

- 所有内部链接有效。
- 每页只有一个 `h1`。
- 每页有独立 title、description、canonical 和 Open Graph 信息。
- 手机宽度下文字和按钮不溢出。
- 不出现虚构用户数据、评价、下载量或媒体背书。

## 后续扩展原则

后续可以继续增加开发笔记、产品复盘或新的小工具页面，但仍应保持真实、克制、可维护。新增页面前先确认它是否帮助用户理解“润木同学是谁、正在做什么、产品如何获取、如何联系”。
