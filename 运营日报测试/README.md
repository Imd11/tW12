# 运营日报测试数据

这个文件夹用于测试 IMD 的「运营日报」模板标准化转换。

建议在 IMD 里打开这个文件夹，然后选择：

- `daily.csv`

这份表故意包含一些真实工作里常见的复杂情况：

- 字段名同时使用中文、英文和模板别名，例如 `统计日期`、`Channel`、`campaign_name`、`sessions`、`dau`、`order_count`、`sales`、`spend`、`cvr`。
- 日期格式混合了 `2026-05-01`、`2026/05/01`、`05/01/2026`。
- 金额包含 `¥`、千分位逗号、小数。
- 百分比包含 `%`。
- 访问量、收入、成本等字段有千分位逗号。
- 有缺失值、备注、多余业务字段。

用「运营日报」模板标准化后，重点检查是否能稳定映射到这些标准字段：

- `date`
- `channel`
- `campaign`
- `visits`
- `signups`
- `active_users`
- `orders`
- `revenue`
- `cost`
- `conversion_rate`
- `retention_rate`
- `owner`
