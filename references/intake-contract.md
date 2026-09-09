# 公开 Intake 合同

## 提交与重试

每次提交自动生成 UUID 请求编号，通过 `Idempotency-Key` 请求头发送。也可用 `--request-id <UUID>` 指定编号。相同分析遇到超时或连接错误时，沿用脚本错误中返回的编号及原参数重试；禁止改编号重复提交。参数变化或用户明确发起新的分析时使用新编号。收到 `analysis_id` 后只查询状态。

请求编号不包含积分数量，费用由服务端决定。余额不足或账号未绑定时，提示用户在官网处理，不索取账号密码或支付信息。脚本不自动重试。

## 全球机会发现

商品机会研究使用全球商品入口，再按用户意图区分呈现重点和排他筛选。未指定平台时默认全球；聚焦某个平台且允许补充时获取全球数据，主平台约 85%、补充约 15%；明确只看某个平台时筛选该平台、全文聚焦。呈现重点只保留在对话上下文，不新增请求字段。

“帮我找到 Temu 的男士钱包蓝海”和“帮我找到男士钱包的蓝海”都可使用 `submit --mode cross_platform --query "男士钱包"`，分别按平台聚焦和全球结构呈现。请求为：

```json
{"query_mode":"cross_platform","query":"男士钱包","target_scope":"available_markets"}
```

| CLI 参数 | 请求字段 | 规则 |
| --- | --- | --- |
| `--query` | `query` | 必填，商品或类目名称，去掉首尾空白后 1 至 120 字。 |
| `--current-platform` | `current_platform` | 可选的真实经营背景；不限制目标市场，不自动优先该平台。不得把用户要研究的平台当成经营背景。 |
| `--platforms` | `platforms` | 用于明确排他平台或限定的多平台比较，允许多个平台、不重复。仅聚焦平台的 85/15 请求不加此筛选。 |
| `--market` | `markets` | 可重复的市场筛选，例如 `amazon:US` 对应 `platform=amazon, market_code=US, scope_kind=country`；`temu:region:EU` 对应区域范围，不能当作国家。 |

全球模式不要求国家，也不默认美国。目标范围由服务的已核实市场目录确定；筛选只缩小范围，不创建新的数据能力。全球参数与单平台 `--platform`、`--country`、`--category`、`--submarket` 互斥。全部参数错误在登记及网络请求前停止。旧调用不发送 `query_mode`，payload 保持原样。

提交和 status 使用相同 analysis_id 流程。候选、供货与讨论材料以服务实际返回为准；跨市场查询不代表所有平台已接入或启动实时付费采集。


## 托管市场查询

`scripts/run-hosted-market-screen submit` 使用下列参数。仅发送下表的查询字段。

| CLI 参数 | 请求字段 | 规则 |
| --- | --- | --- |
| `--platform` | `platform` | 仅 `temu`、`tiktok_shop`、`ozon`、`amazon`、`shopee`、`walmart`；明确传参时才发送该字段。旧调用省略时保持 Temu 请求兼容。 |
| `--country` | `country_code`、`market_scope` | 使用已确认的两位国家代码，并发送 `market_scope=regional`。所有非 Temu 查询必填，缺失或空白时在任何网络请求前停止。 |
| `--category` | `category` | 整体市场可省略；具体商品父类目未知时使用商品名称。 |
| `--submarket` | `submarket` | 已知父类目时传入细分方向，须同时指定 `--category`。 |

本节旧入口用于指定平台的整体市场、类目统计或已知父子类目报告。商品机会问题按前面的全球商品入口和意图筛选处理，不能因提到平台就自动改成旧类目查询。旧入口先确定平台，只澄清缺失的信息；非 Temu 查询不得默认美国或使用 Temu 整体市场范围，未知平台不得回落到 Temu。平台入口不代表该平台已有可用报告，按服务返回状态处理。
