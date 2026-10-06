<div align="center">

# AffProof

[English](README.md) · 中文 · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **本仓库仅用于展示，不公开源码。** AffProof 是私有项目，所以这里没有代码，只介绍它做什么、怎么构建、长什么样。想聊聊它，请通过我的 [GitHub 主页](https://github.com/frommmmmg)联系我。

**一个公开的多语言目录，替联盟项目做尽调，让人知道哪些项目真的会付款。** 每个条目都有带证据的尽调档案、社区评价、出金凭证和纠纷记录。

![AffProof 架构](assets/affproof-architecture.svg)

**亮点**

- **边缘 Serverless。** 整站跑在 Cloudflare Workers 上，数据库用 D1（SQLite），静态资源由边缘直接提供，没有常驻服务器进程需要维护。
- **为搜索而做的服务端渲染。** 页面在 Worker 内渲染，自动输出 JSON-LD 结构化数据、`hreflang` 标签，并按语言生成站点地图。
- **8 种语言**，有一套翻译流程让各语言与英文原文保持同步。
- **分级的公开 API。** 密钥以 SHA-256 哈希存储并在中间件里校验，Free、Pro、Enterprise 三档控制分页上限和返回字段。
- **以证据为门槛的数据。** 尽调条目在导入前要经过评分与门禁，数据库写入方式也避免了静默丢数据。
- **动态 SVG 徽章**，可嵌入其他网站。
- **决策有文档。** 架构决策记录和 bug 复盘与代码放在一起。

**技术栈：** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

## 截图

![线上站点的公开首页](assets/affproof-home.png)
*线上站点的公开首页*

![线上站点上的一份尽调档案页](assets/affproof-dossier.png)
*线上站点上的一份尽调档案页*

## 工作原理

![每个条目都要先过证据门禁，才会被导入并翻译。](assets/affproof-evidence-pipeline.svg)
*每个条目都要先过证据门禁，才会被导入并翻译。*

![公开 API 先在边缘层防护，再由 Worker 做密钥与套餐校验。](assets/affproof-api-flow.svg)
*公开 API 先在边缘层防护，再由 Worker 做密钥与套餐校验。*

---

<div align="center">

<sub>截图只使用示例或公开数据。© 保留所有权利。描述文字可注明出处后引用，软件本身不可再分发。</sub>

</div>
