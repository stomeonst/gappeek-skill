# 公开 Intake 合同

## 提交与重试

每次提交自动生成 UUID 请求编号，通过 `Idempotency-Key` 请求头发送。也可用 `--request-id <UUID>` 指定编号。相同分析遇到超时或连接错误时，沿用脚本错误中返回的编号及原参数重试；禁止改编号重复提交。参数变化或用户明确发起新的分析时使用新编号。收到 `analysis_id` 后只查询状态。

请求编号不包含积分数量，费用由服务端决定。余额不足或账号未绑定时，提示用户在官网处理，不索取账号密码或支付信息。脚本不自动重试。

## 单平台商品机会研究

每次新查询必须先确认一个目标平台。用户明确提到研究平台时，全部查询与报告都限定该平台；用户未指定平台或要求多平台比较时，先请用户选择本次目标，选择前不提交。经营背景不能代替目标，保留在对话中，不发送 `current_platform`。新查询不附其他平台、1688 或 Reddit 数据。

“帮我找到 Temu 的男士钱包蓝海”使用 `submit --mode cross_platform --query "男士钱包" --platforms temu`。`cross_platform` 沿用已有 API 模式名，唯一 `platforms` 将实际查询限制为单个平台，不新增模式或意图字段。请求为：

```json
{"query_mode":"cross_platform","query":"男士钱包","target_scope":"available_markets","platforms":["temu"]}
```

| CLI 参数 | 请求字段 | 规则 |
| --- | --- | --- |
| `--query` | `query` | 必填，商品或类目名称，去掉首尾空白后 1 至 120 字。 |
| `--platforms` | `platforms` | 必填且仅一个值：`temu`、`tiktok_shop`、`amazon`、`shopee`、`walmart`。缺失、重复或多个值均拒绝。Ozon 当前不提供新查询入口。 |
| `--market` | `markets` | 只接受目标平台的市场。用户明确限定国家或区域时必须传入，不能扩展至其他国家。例如 `--platforms amazon --market amazon:US` 对应 `platform=amazon, market_code=US, scope_kind=country`；`--platforms temu --market temu:region:EU` 对应欧洲区域，EU 不能当作国家。用户明确要求同平台多个市场时可重复，不得重复同一市场。 |

未指定国家时不要求补填，不默认美国，使用目标平台已核实市场范围。明确的国家或区域缺少证据时说明不足，不改查其他范围。筛选不创建新的数据能力。`--current-platform` 在新提交中拒绝使用；商品参数与旧统计入口的 `--platform`、`--country`、`--category`、`--submarket` 互斥。这些入口校验在安装登记及网络请求前完成。

提交后使用返回的 `analysis_id` 查询状态。`status` 不重新提交，也不按新的平台入口改写旧报告；已有多平台报告、Ozon 报告和旧请求字段仍按原数据读取。


## 托管市场查询

`scripts/run-hosted-market-screen submit` 使用下列参数。仅发送下表的查询字段。

| CLI 参数 | 请求字段 | 规则 |
| --- | --- | --- |
| `--platform` | `platform` | 必填且仅一个：`temu`、`tiktok_shop`、`amazon`、`shopee`、`walmart`。不默认 Temu，不开放 Ozon 新查询。 |
| `--country` | `country_code`、`market_scope` | 使用已确认的两位国家代码，并发送 `market_scope=regional`。所有非 Temu 查询必填，缺失或空白时在任何网络请求前停止。EU 属于区域，不接受为国家。 |
| `--category` | `category` | 整体市场可省略；具体商品父类目未知时使用商品名称。 |
| `--submarket` | `submarket` | 已知父类目时传入细分方向，须同时指定 `--category`。 |

本节兼容入口只用于明确指定平台的整体市场、类目统计或已知父子类目报告，沿用不发送 `query_mode` 的旧字段格式。商品机会问题使用前面的单平台商品入口。只澄清缺失信息；非 Temu 查询不得默认美国或使用 Temu 整体市场范围，未知平台不得回落到 Temu。平台入口不代表该平台已有可用报告，按服务返回状态处理。
