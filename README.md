**简体中文** | [English](./README.en.md)

<p align="center"><img src="./assets/gappeek-mark.svg" width="104" alt="GapPeek 标志"></p>
<h1 align="center">GapPeek</h1>
<p align="center"><strong>用市场证据发现机会。</strong></p>

GapPeek 帮助你研究商品需求、竞争和价格，比较 Temu、TikTok Shop、Amazon、Shopee、Walmart 的市场机会。

[访问官网](https://gappeek.com) · [查看报告示例](https://gappeek.com/zh/sample-report) · [版本记录](./CHANGELOG.md)

## 安装

把这条指令发给你的 AI Agent，或在终端运行：

```bash
npx skills add stomeonst/gappeek-skill --yes
```

安装后，在官网注册并验证邮箱。让 Agent“连接 GapPeek”，将它返回的绑定码填入[设备绑定页](https://gappeek.com/zh/account/devices)。账号有积分后即可提交研究。若 Agent 尚未识别新 Skill，请重新启动 Agent。

## 直接说出你的问题

```text
帮我找到 Temu 的男士钱包蓝海。
```

```text
帮我找到男士钱包的蓝海。
```

```text
比较 Amazon 和 TikTok Shop 的宠物清洁用品机会。
```

指定平台时，报告围绕该平台展开，并补充其他平台的相关机会。没有指定平台时，比较不同平台和国家的可用市场证据。也可以指定国家、只看一个平台或比较几个平台。

## 报告能帮助你判断什么

| 关注点 | 报告内容 |
| --- | --- |
| 商品需求 | 销量观测、需求结构和已有变化记录 |
| 市场竞争 | 商品、卖家及竞争集中度 |
| 价格空间 | 对应市场的价格与币种 |
| 商品相关性 | 匹配样本、相邻商品和待核验项 |
| 后续研究 | 值得继续调查的市场及其依据 |

每份报告保留实际平台、国家和观测日期。缺失数据不补零，样本不冒充全市场；研究结果不构成销量或利润保证。

## 安装指定版本与回档

每次发布保留独立标签、变更记录和安装包，旧版本不会被覆盖。需要恢复历史版本时，从 [Releases](https://github.com/stomeonst/gappeek-skill/releases) 选择版本并下载 `gappeek.skill`，交给 Agent 安装。

也可以先将仓库检出到对应标签，再从本地目录安装：

```bash
git clone https://github.com/stomeonst/gappeek-skill.git
cd gappeek-skill
git checkout v0.1.1-20260909.1
npx skills add . --yes
```

客户端版本与服务能力分别演进，回档客户端不会回滚服务中的账号或数据。

## 仓库内容

- [SKILL.md](./SKILL.md)：Agent 研究流程。
- [输入合同](./references/intake-contract.md)与[结果合同](./references/result-contract.md)：请求和报告规则。
- [客户端脚本](./scripts/run-hosted-market-screen)：提交查询与读取报告。
- [历史案例](./examples/us-womens-running-shoes.md)：2026 年 8 月 27 日的冻结观测。

仓库只分发 Skill 客户端和公开合同。服务端代码、账号秘密和原始数据不在此仓库分发。

## 许可证

采用 [GapPeek Skill License 1.0](./LICENSE)。你可以安装未修改的 Skill 用于个人或企业内部研究；修改、再分发、白标、转售或绕过访问控制需要事先取得书面许可。
