# 部署计划

## 1. 部署目标

`rmrm.me` 第一版网站是纯静态站。部署目标是：

```text
让用户可以稳定访问 rmrm.me
让应用市场可以访问隐私政策和支持页面
让后续运营内容有一个可信落点
```

第一版不需要服务器，不需要数据库，不需要对象存储，不需要自建 API。

优先保证：

- 页面能访问。
- HTTPS 正常。
- 手机端打开正常。
- 隐私政策 URL 稳定。
- 支持反馈 URL 稳定。

## 2. 推荐部署方式

第一版推荐优先考虑：

```text
Cloudflare Pages
或
Vercel
```

这两种方式都适合纯静态站，能绑定自定义域名，并自动提供 HTTPS。

备选：

```text
GitHub Pages
对象存储静态网站
```

但第一版不优先推荐对象存储，因为它会引入更多云服务配置，对当前阶段没有必要。

## 3. 部署方式对比

### 3.1 Cloudflare Pages

优点：

- 适合静态站。
- 全球 CDN。
- HTTPS 配置方便。
- 绑定自定义域名体验好。
- 可以直接连接 GitHub 仓库。
- 后续如果要加轻量函数，可以使用 Cloudflare Workers。

适合当前阶段。

注意：

- 需要 Cloudflare 账号。
- 如果 DNS 也托管到 Cloudflare，域名解析会更顺。

### 3.2 Vercel

优点：

- 部署静态站很方便。
- 连接 GitHub 简单。
- 自动 HTTPS。
- 预览部署方便。
- 后续如果升级成 Next.js 也比较顺。

适合当前阶段。

注意：

- 第一版不要因为用了 Vercel 就上 Next.js。
- 仍然可以部署纯静态 HTML。

### 3.3 GitHub Pages

优点：

- 免费。
- 适合简单静态站。
- 和 GitHub 仓库绑定直接。

缺点：

- 自定义域名和 HTTPS 配置有时需要多一点检查。
- 部署体验不如 Cloudflare Pages/Vercel 直观。

如果想极简，也可以用。

### 3.4 对象存储静态网站

例如 TOS、OSS、COS 等对象存储。

优点：

- 适合放大量静态资源。
- 后续如果有音频、图片、下载包分发，可能会用到。

当前不推荐作为第一版网站方案。

原因：

- 第一版网站只有几个 HTML/CSS/图片文件。
- 没有大量静态资源分发需求。
- 对象存储配置、HTTPS、CDN、权限容易增加心智负担。
- 当前更需要快上线，而不是云服务架构。

## 4. 当前阶段是否需要 TOS

结论：

```text
第一版 rmrm.me 不需要 TOS。
```

原因：

- 网站是纯静态小站。
- 页面数量少。
- 图片资源少。
- 暂时不提供音频下载。
- 暂时不做用户上传。
- 暂时不做内容包远程分发。
- 暂时不做 App 行为数据存储。

什么时候再考虑 TOS 或其他对象存储：

- 需要分发大量音频文件。
- 需要提供 App 安装包下载。
- 需要远程内容包。
- 需要用户上传资源。
- 网站图片/文件资源明显变多。
- 需要和 CDN 做更细的资源分发。

当前不要为了“以后可能用”提前开复杂服务。

## 5. 当前阶段是否需要服务器

结论：

```text
第一版 rmrm.me 不需要服务器。
```

原因：

- 没有登录。
- 没有数据库。
- 没有支付。
- 没有后台管理。
- 没有用户数据提交接口。
- 反馈入口使用飞书表单。
- 隐私政策和支持页都是静态内容。

什么时候再考虑轻后端：

- App 需要匿名行为统计上传。
- App 需要远程配置。
- App 需要付费状态校验。
- App 需要音色服务。
- App 需要 AI 代理接口。
- 用户反馈不再满足于飞书表单。

即使后续需要，也优先考虑轻量云函数或边缘函数，不要一开始就维护完整服务器。

## 6. 推荐上线流程

建议流程：

```text
1. 完成 rmrm_me 静态站源码
2. 将 rmrm_me 文件夹移出当前 Flutter 项目
3. 把 rmrm_me 改名为独立项目目录
4. 初始化独立 Git 仓库
5. 推送到 GitHub
6. 连接 Cloudflare Pages 或 Vercel
7. 配置构建设置
8. 绑定 rmrm.me 域名
9. 开启 HTTPS
10. 验证首页、隐私政策、支持页
11. 更新 App / 应用市场中的 URL
```

## 7. 移出独立项目后的建议

当 `rmrm_me/` 从当前 Flutter 项目中移出后，建议改成一个独立仓库。

独立项目建议名称：

```text
rmrm_me
```

或：

```text
rmrm-site
```

如果未来网站只服务 `rmrm.me`，可以使用：

```text
rmrm.me
```

但部分工具对点号目录名支持一般，所以更稳的是：

```text
rmrm_me
```

独立仓库初始结构：

```text
rmrm_me/
  index.html
  tingting.html
  about.html
  privacy.html
  support.html
  assets/
    css/
      style.css
    images/
  docs/
  README.md
```

## 8. Git 初始化流程

移出后，在 `rmrm_me/` 目录执行：

```powershell
git init
git add .
git commit -m "init rmrm.me static site"
```

如果使用 GitHub：

```powershell
git remote add origin <your-github-repo-url>
git branch -M main
git push -u origin main
```

注意：

- 不要把 Flutter App 项目的 `.git` 一起移动。
- 不要把 App 的 build、assets/audio、SQLite 数据库等内容带进网站项目。
- 网站项目只保留网站源码、图片和文档。

## 9. Cloudflare Pages 部署建议

如果使用 Cloudflare Pages：

1. 登录 Cloudflare。

2. 进入 Workers & Pages。

3. 创建 Pages 项目。

4. 连接 GitHub 仓库。

5. 选择 `rmrm_me` 仓库。

6. 构建设置：

   ```text
   Framework preset: None
   Build command: 留空
   Build output directory: /
   ```

   如果平台要求输出目录，可以根据实际仓库结构填写根目录。

7. 部署后先访问 Cloudflare 提供的临时域名。

8. 确认页面正常后绑定自定义域名：

   ```text
   rmrm.me
   www.rmrm.me
   ```

9. 开启 HTTPS。

10. 验证：

   ```text
   https://rmrm.me/
   https://rmrm.me/privacy.html
   https://rmrm.me/support.html
   ```

如果希望使用无后缀 URL：

```text
https://rmrm.me/privacy
https://rmrm.me/support
```

可以后续再配置重写规则。第一版先保证 `.html` 可访问也可以。

## 10. Vercel 部署建议

如果使用 Vercel：

1. 登录 Vercel。

2. New Project。

3. 导入 GitHub 仓库。

4. Framework Preset 选择：

   ```text
   Other
   ```

5. Build Command 留空。

6. Output Directory 留空或使用根目录。

7. 部署后访问 Vercel 临时域名。

8. 绑定自定义域名：

   ```text
   rmrm.me
   www.rmrm.me
   ```

9. 根据 Vercel 提示配置 DNS。

10. 验证 HTTPS。

Vercel 也可以部署纯静态 HTML，不需要为了部署而引入 Next.js。

## 11. GitHub Pages 部署建议

如果使用 GitHub Pages：

1. 推送网站仓库到 GitHub。

2. 进入仓库 Settings。

3. 打开 Pages。

4. Source 选择：

   ```text
   Deploy from a branch
   ```

5. Branch 选择：

   ```text
   main
   ```

6. Folder 选择：

   ```text
   /root
   ```

7. 配置自定义域名：

   ```text
   rmrm.me
   ```

8. 按 GitHub 提示配置 DNS。

9. 勾选 HTTPS。

GitHub Pages 可以用，但后续如果希望部署体验更顺，Cloudflare Pages 或 Vercel 更适合。

## 12. DNS 和域名建议

域名：

```text
rmrm.me
```

建议同时配置：

```text
rmrm.me
www.rmrm.me
```

最终访问可以统一到一个主域。

推荐：

```text
https://rmrm.me
```

`www.rmrm.me` 可以重定向到 `rmrm.me`。

具体 DNS 记录取决于部署平台。不要手写固定记录到文档里，实际部署时按平台提示配置。

## 13. URL 规划

第一版核心 URL：

```text
https://rmrm.me/
https://rmrm.me/tingting.html
https://rmrm.me/about.html
https://rmrm.me/privacy.html
https://rmrm.me/support.html
```

如果后续配置无后缀路径，则使用：

```text
https://rmrm.me/
https://rmrm.me/tingting
https://rmrm.me/about
https://rmrm.me/privacy
https://rmrm.me/support
```

当前 App 内关于页已经使用：

```text
rmrm.me
rmrm.me/support
rmrm.me/privacy
```

因此正式部署时，建议尽量支持无后缀路径：

```text
/support
/privacy
```

如果部署平台暂时没配置重写，也可以先确保：

```text
/support.html
/privacy.html
```

可访问，然后后续再补重写。

## 14. 上线前检查清单

上线前检查：

- 首页能打开。
- 润木听听产品页能打开。
- 关于页能打开。
- 隐私政策页能打开。
- 支持页能打开。
- 所有导航链接有效。
- 页脚链接有效。
- 飞书表单链接已替换。
- 没有假下载链接。
- 没有未完成 TODO 暴露给用户。
- 隐私政策更新日期正确。
- 页面 title 正确。
- 页面 description 正确。
- 手机端排版正常。
- HTTPS 正常。
- `rmrm.me` 能访问。
- `www.rmrm.me` 能访问或能重定向。

## 15. 应用市场相关检查

如果用于应用市场上架或内测资料，需确认：

隐私政策 URL：

```text
https://rmrm.me/privacy
```

或：

```text
https://rmrm.me/privacy.html
```

支持 URL：

```text
https://rmrm.me/support
```

或：

```text
https://rmrm.me/support.html
```

官方网站：

```text
https://rmrm.me
```

这些 URL 必须：

- 无需登录即可访问。
- 在手机浏览器可正常打开。
- 不跳转到空白页。
- 不要求下载 App 才能查看。
- 不展示未完成占位内容。

## 16. 后续如果增加统计

第一版不接统计。

如果后续需要知道：

- 网站访问量。
- 页面来源。
- 点击反馈按钮次数。

可以考虑：

- Cloudflare Web Analytics。
- Plausible。
- Umami。

但要注意：

- 不要一开始就接重型广告/营销分析。
- 如果统计会设置 Cookie 或收集可识别信息，需要更新隐私说明。
- App 的用户行为统计和网站访问统计应分开设计。

## 17. 后续如果增加 App 行为数据接口

这不属于第一版网站。

如果未来需要 App 上传匿名行为事件，例如：

- app_open
- playback_start
- playback_pause
- pack_set_current

应单独设计轻后端或云函数，并更新 App 隐私政策。

不要把这些接口直接塞进静态网站第一版。

也不要在前端暴露飞书 API token。

## 18. 回滚策略

静态站部署的好处是回滚简单。

建议：

- 每次上线前提交 Git。
- 部署平台使用 Git 记录版本。
- 如果上线后发现问题，回滚到上一 commit。

推荐 commit 信息：

```text
init static site
add privacy and support pages
update homepage copy
fix mobile layout
```

不要直接在部署平台手工改线上文件，避免本地和线上不一致。

## 19. 当前结论

当前最适合的部署策略：

```text
纯静态站
GitHub 仓库管理
Cloudflare Pages 或 Vercel 部署
绑定 rmrm.me
反馈用飞书表单
暂不使用 TOS
暂不自建服务器
```

先让网站成为一个可信、稳定、能被访问的入口。等 App 内测反馈和运营方向更清晰后，再决定是否扩展后端、统计或更多页面。

## 20. 当前 Cloudflare Pages 实际配置与安全提醒

更新时间：2026-07-04。

当前 `rmrm.me` 已经部署到 Cloudflare Pages，并连接 GitHub 仓库：

```text
GitHub 仓库：oceanstudy1203/rmrm
Cloudflare Pages 项目：rmrm
生产分支：main
自动部署：已启用
主域名：https://rmrm.me
www 域名：https://www.rmrm.me
Pages 临时域名：https://rmrm.pages.dev
```

### 20.1 DNS 记录

Cloudflare DNS 当前只保留网站需要的两条记录：

```text
rmrm.me      CNAME  rmrm.pages.dev  已代理
www.rmrm.me  CNAME  rmrm.pages.dev  已代理
```

安全提醒：

- 不要添加陌生的 `A` 记录。
- 不要添加指向陌生域名的 `CNAME`。
- 如果看到不认识的 IP、域名或跳转相关记录，需要先暂停修改并排查。
- Cloudflare 提示“邮件无法送达”可以暂时忽略，除非后续要使用 `@rmrm.me` 邮箱收发邮件。

### 20.2 域名与跳转

当前推荐主入口：

```text
https://rmrm.me
```

已配置 `www` 到根域名的 301 重定向：

```text
https://www.rmrm.me/* -> https://rmrm.me/${1}
```

安全提醒：

- 对外发布、测试和应用市场资料中优先使用完整的 `https://rmrm.me`。
- 不建议只写 `rmrm.me` 进行安全排查，因为不同浏览器可能先尝试 HTTP、搜索联想或读取旧缓存。
- Cloudflare 规则里不应出现跳转到陌生外部域名的 Redirect Rule。

### 20.3 SSL/TLS 与 HTTPS 设置

Cloudflare `SSL/TLS` 当前建议保持：

```text
加密模式：Full 或 Full (strict)
始终使用 HTTPS：开启
最低 TLS 版本：TLS 1.2
TLS 1.3：开启
自动 HTTPS 重写：开启
Universal SSL：保持启用
```

不要点击“禁用通用 SSL”。

### 20.4 HSTS 设置

Cloudflare 边缘证书中已启用 HSTS，当前建议配置：

```text
启用 HSTS：开启
max-age：6 个月
includeSubDomains：开启
Preload：关闭
```

安全提醒：

- `includeSubDomains` 开启后，未来新增 `api.rmrm.me`、`test.rmrm.me` 等子域名时，这些子域名也必须支持 HTTPS。
- 在确认所有长期子域名都稳定支持 HTTPS 前，不要开启 HSTS Preload。
- 代码中的 `_headers` 也已经添加 `Strict-Transport-Security`，Cloudflare 面板和静态文件响应头可以共同起到加固作用。

### 20.5 静态站响应头

Cloudflare Pages 根目录的 `_headers` 已添加安全响应头：

```text
Strict-Transport-Security
Content-Security-Policy
X-Frame-Options
X-Content-Type-Options
Referrer-Policy
Permissions-Policy
Cross-Origin-Opener-Policy
Cross-Origin-Resource-Policy
```

其中 `rmrm.pages.dev` 临时域名额外设置：

```text
X-Robots-Tag: noindex
```

目的是让搜索引擎优先收录正式域名 `rmrm.me`，而不是 Pages 临时域名。

### 20.6 Workers 路由

当前 `rmrm.me` 的 Workers 路由为空。

安全提醒：

- 不要随意给 `rmrm.me/*` 或 `www.rmrm.me/*` 绑定 Worker。
- 如果后续确实需要 Worker，必须先确认 Worker 源码、路由范围和回滚方案。
- 如果出现陌生 Worker 路由，优先怀疑该路由可能接管了访问流量。

### 20.7 异常跳转排查记录

曾在个别手机浏览器、特定网络环境下看到过跳转到陌生博彩页面的截图，但后续在多浏览器、多网络下未能复现。当前已检查：

```text
源码中没有发现恶意 script、iframe、window.location 或 location.href 跳转。
DNS 记录正常。
Workers 路由为空。
Cloudflare Pages 部署正常。
线上响应头正常。
www 到根域名跳转正常。
HTTP 到 HTTPS 跳转正常。
```

如果未来再次出现异常跳转，应记录：

- 发生时间。
- 使用的网络：Wi-Fi、4G、5G。
- 使用的浏览器。
- 输入的是 `rmrm.me` 还是 `https://rmrm.me`。
- 最终跳转到的完整域名。
- 是否出现证书不可信提示。

排查顺序：

1. 使用完整 `https://rmrm.me` 重新测试。
2. 切换 Wi-Fi 和手机流量测试。
3. 使用无痕模式测试。
4. 换浏览器测试。
5. 检查 Cloudflare DNS、Redirect Rules、Workers 路由。
6. 检查源码中是否新增了外链脚本或跳转代码。

如果只有某个 Wi-Fi 或某个浏览器复现，优先排查网络 DNS、路由器、浏览器安全拦截或缓存；如果所有网络和浏览器都稳定复现，再排查站点源码和 Cloudflare 配置。
