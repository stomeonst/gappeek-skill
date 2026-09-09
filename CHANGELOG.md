# 版本记录 / Changelog

## v0.1.1-20260909.2 · 2026-09-09

- 每次商品研究只查询用户明确选择的一个平台，国家范围同步限制。
- 取消新报告的其他平台补充，未指定平台时先请求选择。
- 客户端提前检查单平台范围，保留已有报告读取、请求编号和账号连接。

Each new product research task targets one selected platform, with matching country filters. Reports focus on that platform. The client validates the selected scope before submission while preserving saved reports and account linking.

## v0.1.1-20260909.1 · 2026-09-09

- 补齐首次连接、官网注册和设备绑定指引。
- 清理过时实验登记与开发进度，保留实际报告范围和证据要求。
- 拒绝 API 跳转，保护本机安装凭据；账号权限、余额不足和服务不可用时提供明确提示。

This release clarifies first-time account linking, removes obsolete experiment notes, blocks API redirects, and explains service errors without exposing response internals.

## v0.1.1-20260908.1 · 2026-09-08

- 分析提交携带唯一请求编号，支持通过 `--request-id` 安全重试同一分析。
- 连接失败时保留重试编号，收到任务编号后只查询状态。
- 沿用原有提问意图与报告篇幅规则，保留旧版本以便回档。

Analysis submissions carry an idempotency key. Reuse the returned request ID after a connection failure to recover the same analysis without creating another job. Existing question routing and report rules are unchanged.

## v0.1.1-20260907.6 · 2026-09-07

- 同步跨平台商品研究入口与全球市场报告合同。
- 根据用户提问分配报告篇幅：指定平台时约 85% 聚焦该平台，其他平台约 15%；未指定平台时使用全球发现模式；排他查询遵从指定范围。
- 保留商品匹配、研究队列和事实证据边界。
- 更新中英文介绍，展示 Temu、TikTok Shop、Amazon、Shopee、Walmart。
- 增加可下载安装包、版本标签与回档说明。

This release updates cross-platform research, question-aware report focus, product matching and public documentation. An explicit platform focus uses approximately 85% of the report for that platform and 15% for supplementary opportunities. Open queries use global discovery; exclusive queries retain their requested limits.

服务能力以实际返回为准；客户端归档不代表所有市场都有可返回的数据。

## archive-before-20260907 · 2026-09-07

保留更新前的公开仓库状态，原提交 f755407。该标签用于恢复此前客户端与双语文档。
