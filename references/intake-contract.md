# 公开 Intake 合同

Skill 只能生成下列结构。数组没有内容时使用空数组。美元价格偏好未知时使用 `null`。禁止添加联系方式、姓名、店铺标识、登录信息或其他个人身份字段。

```json
{
  "schema_version": "1.0",
  "intake_kind": "m1_free_skill",
  "requested_at": "2026-08-12T10:00:00+08:00",
  "operating_scope": "us",
  "seller_stage": "preparing",
  "first_order_budget_cny": 5000,
  "fulfillment_model": "semi_managed",
  "maximum_package_class": "small",
  "excluded_traits": [
    "liquid"
  ],
  "qualification_ids": [],
  "current_categories": [
    "women-clothing"
  ],
  "preferred_price_min_usd": 10,
  "preferred_price_max_usd": 30,
  "research_consent": true
}
```

## 固定值

- `schema_version`：`1.0`
- `intake_kind`：`m1_free_skill`
- `operating_scope`：`us`、`global` 或 `both`
- `research_consent`：只有用户明确同意时才能设为 `true`

## 输出规则

1. 只输出一个符合合同的 JSON 对象。
2. 数组值去重，禁止空字符串。
3. 最低价格不得高于最高价格。
4. 不确定的可选价格使用 `null`，其他必填项继续向用户确认。
5. 生成 Intake 不代表已经入选实验，也不代表报告已经批准。
