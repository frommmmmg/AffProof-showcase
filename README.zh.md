<div align="center">

# AffProof

[English](README.md) · 中文 · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **本仓库仅用于展示，不公开源码。** AffProof 是私有项目，所以这里没有代码，只介绍它做什么、怎么构建、长什么样。想聊聊它，请通过我的 [GitHub 主页](https://github.com/frommmmmg)联系我。

**一个公开的多语言目录，替联盟项目做尽调，让人知道哪些项目真的会付款。** 每个条目都有带证据的尽调档案、信誉评分、出金凭证和纠纷记录。

![架构：边缘过滤、Hono Worker 和 D1。](assets/affproof-architecture.svg)

**亮点**

- **边缘 Serverless。** 整站跑在 Cloudflare Workers 上，数据库用 D1（SQLite），静态资源由边缘直接提供，没有常驻服务器进程需要维护。
- **两套完整的界面主题，实时切换。** 一套密集的黑金风格，一套 8 位像素街机风格，还有可选的音效。宽度开关（1200、768、390 px）可以预览平板和手机尺寸。
- **为快速找到合适项目而做。** 实时搜索，可按平台、出金渠道、时间范围筛选，有四种排序（推荐、点击、排名飙升、凭证数），还有金牌尽调筛选。
- **用严格的渠道网格代替营销话术。** 每张卡片都用同样的固定格子展示 USDT、PayPal、Payoneer、Stripe 和联系渠道，有则点亮，没有就划掉，所以卡片整齐对齐，也没法包装。
- **看得懂的信誉。** 满分 1000 的评分、已核实的出金记录和 48 小时公开纠纷窗口，不用编造的通过率。
- **为搜索而做的服务端渲染。** 页面在 Worker 内渲染，自动输出 JSON-LD 结构化数据、`hreflang` 标签，并按语言生成站点地图。
- **8 种语言**，有一套翻译流程让各语言与英文原文保持同步。
- **分套餐的公开 API。** 密钥以 SHA-256 哈希存储并在中间件里校验，Free、Pro、Enterprise 三档控制分页上限和返回字段。
- **以证据为门槛的数据。** 每份尽调档案在导入前都要经过评分与质量门禁，数据库写入方式也避免了静默丢数据。
- **动态 SVG 徽章**，可嵌入其他网站；**决策有文档**：架构决策记录和 bug 复盘与代码放在一起。

**技术栈：** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

**数据（2026 年 10 月）：** 已收录 380 个项目，其中 377 个有完整的审计档案，支持 8 种语言。

## 截图

![默认黑金主题下的首页。](assets/affproof-home.jpg)
*默认黑金主题下的首页。*

![项目目录：筛选、排序和固定的渠道网格。](assets/affproof-matrix.jpg)
*项目目录：筛选、排序和固定的渠道网格。*

![同样的页面，换成 8 位街机主题。](assets/affproof-arcade-home.jpg)

![同样的页面，换成 8 位街机主题。](assets/affproof-arcade-matrix.jpg)
*同样的页面，换成 8 位街机主题。*

![一份尽调档案页，以及它的商业条款和流量部分。](assets/affproof-dossier.jpg)

![一份尽调档案页，以及它的商业条款和流量部分。](assets/affproof-dossier-seo.jpg)
*一份尽调档案页，以及它的商业条款和流量部分。*

![中文和德语的首页。](assets/affproof-languages.jpg)
*中文和德语的首页。*

![手机上：搜索与筛选，以及一张项目卡片。](assets/affproof-mobile.jpg)
*手机上：搜索与筛选，以及一张项目卡片。*

## 工作原理

![每个条目都要先过证据门禁，才会被导入并翻译。](assets/affproof-evidence-pipeline.svg)
*每个条目都要先过证据门禁，才会被导入并翻译。*

![公开 API 先在边缘层防护，再由 Worker 做密钥与套餐校验。](assets/affproof-api-flow.svg)
*公开 API 先在边缘层防护，再由 Worker 做密钥与套餐校验。*

![一个 Worker 渲染所有语言。](assets/affproof-locale-render.svg)
*一个 Worker 渲染所有语言。*

---

<div align="center">

<sub>截图只使用示例或公开数据。© 保留所有权利。描述文字可注明出处后引用，软件本身不可再分发。</sub>

</div>
