<div align="center">

# AffProof

[English](README.md) · 中文 · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

🌐 **[affproof.com](https://affproof.com)** · [GitHub @frommmmmg](https://github.com/frommmmmg)

✍️ 作者 **姜芊泽** · 微信公众号: **Pin海引航**

</div>

> **本仓库仅用于展示，不公开源码。** AffProof 不开源，所以这里没有代码，只介绍它做什么、怎么构建、长什么样。想聊聊它，请通过我的 [GitHub 主页](https://github.com/frommmmmg)联系我。

**一个公开的多语言目录，替联盟项目做尽调，让人知道哪些项目真的会付款。** 每个条目都有带证据的尽调档案、信誉评分、出金凭证和纠纷记录。

联盟营销里到处是这样的项目：落地页看着很慷慨，规模一上来就悄悄不付钱。大多数目录只是照抄厂商自己的说法。AffProof 从另一头做起：只记录能被核实的东西（真实的联盟页面、实际提供的出金渠道、白纸黑字的佣金条款），再让社区补上只有他们才知道的信息，比如钱到没到账。口号是 *Proof of payout. Zero fluff.*（有据可查，绝无虚标）。

![架构](assets/affproof-architecture.svg)

| | |
|---|---|
| **网站** | **[affproof.com](https://affproof.com)**，支持 8 种语言 |
| **我的角色** | 一个人完成产品、数据流水线、前端、边缘后端和运维 |
| **状态** | 已在生产环境运行 |
| **规模** | 已收录 380 个项目，其中 377 个有完整审计档案（2026 年 10 月） |
| **技术栈** | Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions |

### 它能做什么

**给站长**
- **快速找到合适的项目。** 实时搜索，可按平台、出金渠道、时间范围筛选，有四种排序（推荐、点击、排名飙升、凭证数），还有金牌尽调筛选。
- **用严格的渠道网格代替营销话术。** 每张卡片都用同样的固定格子展示 USDT、PayPal、Payoneer、Stripe 和联系渠道，有则点亮，没有就划掉，所以卡片整齐对齐，也没法包装。
- **看得懂的信誉。** 满分 1000 的评分，来自尽调档案、滚动 30 天的出金凭证与评价、带衰减的活跃度，以及厂商 48 小时内未回应纠纷所扣的分。厂商把纠纷处理掉，分数会自动恢复。
- **两套完整的界面主题，实时切换：** 一套密集的黑金风格，一套 8 位像素街机风格，还有可选音效。宽度开关（1200、768、390 px）可以预览平板和手机尺寸。

**给厂商**
- **约十秒钟认领自己的条目**，并把动态的 *Verified by AffProof* SVG 徽章嵌到自己的网站上。

**给搜索引擎和开发者**
- **为搜索而做的服务端渲染。** 页面在 Worker 内渲染，自动输出 JSON-LD 结构化数据、`hreflang` 标签，并按语言生成站点地图。
- **8 种语言**，有一套翻译流程让各语言与英文原文保持同步。
- **分套餐的公开 API。** 密钥以 SHA-256 哈希存储并在中间件里校验，Free、Pro、Enterprise 三档控制分页上限和返回字段。

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

<!--notes-->
## 工程笔记

- **选择边缘原生，是决策，不是赶时髦。** 没有 VPS，没有容器，没有常驻进程。理由写成了架构决策记录：零冷启动、全球扩展，以及几乎为零的闲置成本。
- **API 有两层防护。** 边缘规则先挡掉扫描和洪水请求；Worker 再校验哈希后的密钥，套用套餐配额，只返回该套餐可见的字段。列表用游标分页，从不使用深度 `OFFSET`。
- **运维放在零信任之后。** 管理端和自动化脚本都在 Cloudflare Access 后面，用服务令牌接入，未授权的流量在边缘就被拒绝，到不了 Worker。
- **会自我恢复的信誉分。** 纠纷截止时间在读取分数时惰性判定，扣分总是按当前纠纷重新计算。一个无视纠纷的项目会被自动关闭，纠纷解决后又会自动重开。
- **一条从事故里学到的硬规则。** 有一次批量导入用了先删后插的写法，悄悄清掉了关联数据。现在导入一律原地更新，并先与表结构对账。复盘和规则都写在代码旁边。
- **一切都有文档。** 架构决策、bug 记录、翻译指南和数据质量规范都在仓库里，下一次改动从理由出发，而不是靠猜。

<!--author-->
## 关于作者

<img src="assets/wechat-qr.png" alt="微信公众号 Pin海引航 的二维码" width="200" align="right">

**姜芊泽** 是我的笔名。我是一名独立开发者，致力于为出海品牌、商家和创作者提供工具、数据和自动化方案。这些展示里的每个项目，从产品想法到服务器和文档，都是我一个人设计、构建并运营的。

我在微信公众号 **Pin海引航** 上写这方面的内容。扫码关注，或者到 [GitHub](https://github.com/frommmmmg) 找我。

<br clear="right">
<!--/author-->

**其他项目展示:** [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AutoPin-CS](https://github.com/frommmmmg/AutoPin-CS-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>截图只使用示例或公开数据。© 保留所有权利。描述文字可注明出处后引用，软件本身不可再分发。</sub>

</div>
