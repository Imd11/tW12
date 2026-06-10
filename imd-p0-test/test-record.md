# IMD P0 数据动作测试记录

测试文件：`/Users/yang/Desktop/imd-p0-test/p0.csv`

测试目的：先验证 App 已有的数据动作是否稳定，再决定哪些动作可以接入 CLI。不要先测试删除字段这类高风险动作。

## 原始测试数据特征

| 特征 | 覆盖内容 |
|---|---|
| 字段名不标准 | `Channel Name`、`Signup Count`、`GMV`、`Ad Cost`、`Conv %`、`Retention %`、`Order Key` |
| 日期格式混杂 | `2026/06/01`、`06/02/2026`、`2026-06-03` |
| 金额格式混杂 | `$5,320.50`、`$5,610`、`4200.75`、`invalid` |
| 百分比格式 | `2.83%`、空值、`41%` |
| 缺失值 | `Signup Count`、`Visitors`、`Orders`、`Conv %`、`Retention %` |
| 文本清理 | ` Paid Search `、空白 `Note` |
| 重复行 | `Order Key = A-005` 有两行 |

## 运营日报模板字段

当前代码中的 `operations_daily` 模板要求的标准字段如下：

| 模板字段 | 类型 | 级别 | 可能匹配到的测试字段 |
|---|---|---|---|
| `date` | date | core | `Date` |
| `channel` | category | recommended | `Channel Name` |
| `campaign` | text | recommended | `Campaign` |
| `visits` | count | recommended | `Visitors` |
| `signups` | count | recommended | `Signup Count` |
| `active_users` | count | recommended | `Active Users` |
| `orders` | count | recommended | `Orders` |
| `revenue` | currency | recommended | `GMV` |
| `cost` | currency | recommended | `Ad Cost` |
| `conversion_rate` | percentage | recommended | `Conv %` |
| `retention_rate` | percentage | recommended | `Retention %` |
| `owner` | text | recommended | `Owner` |

## P0-1 字段重命名

| 记录项 | 内容 |
|---|---|
| 操作 | 把 `Channel Name` 重命名为 `channel_name_test` |
| 预期 | 表头立即更新；原有值不变；History 记录重命名；Restore 后能恢复 |
| 实际结果 | 待填写 |
| History 是否记录 | 待填写 |
| Restore 是否成功 | 待填写 |
| 是否通过 | 待填写 |

## P0-2 类型转换

| 字段 | 建议转换 | 预期 |
|---|---|---|
| `Date` | 日期 | 能识别多种日期格式，非法日期不应乱转 |
| `GMV` | 金额 | `$5,320.50`、`$5,610`、普通数字能转；`invalid` 应保留为空或失败提示明确 |
| `Ad Cost` | 金额 | 普通数字能转为金额/数值 |
| `Conv %` | 百分比 | `2.83%` 能按百分比处理；空值不应变成 0 |
| `Visitors` / `Orders` | 整数或计数 | 数字能转；空值仍为空 |

| 记录项 | 内容 |
|---|---|
| 实际结果 | 待填写 |
| History 是否记录 | 待填写 |
| Restore 是否成功 | 待填写 |
| 是否通过 | 待填写 |

## P0-3 缺失值填充

| 字段 | 建议测试策略 | 预期 |
|---|---|---|
| `Signup Count` | 中位数或固定值 | 只填空值，不改已有值 |
| `Visitors` | 中位数或固定值 | 两个空值被填充，其他行不变 |
| `Orders` | 固定值或中位数 | 空值被填充，其他行不变 |
| `Conv %` | 固定值或留空 | 不应把所有空白误填成异常格式 |

| 记录项 | 内容 |
|---|---|
| 实际结果 | 待填写 |
| History 是否记录 | 待填写 |
| Restore 是否成功 | 待填写 |
| 是否通过 | 待填写 |

## P0-4 模板标准化：运营日报

操作：点击 `[模板 ▼]`，选择 `运营日报`。

重点观察：

| 检查点 | 预期 |
|---|---|
| 字段匹配 | 上表中的 12 个模板字段尽量被正确匹配 |
| 字段命名 | 输出字段应是模板标准字段，不是原始乱字段名 |
| 未匹配字段 | `Status`、`Region`、`Note`、`Order Key` 不应默认混入标准输出，除非产品规则明确保留 |
| 类型转换 | 日期、金额、百分比、计数字段不应被误转 |
| 异常值 | `GMV = invalid` 不应导致整次转换崩溃 |
| History | 记录为模板标准化动作，并可以 Restore |

| 记录项 | 内容 |
|---|---|
| 实际输出字段 | 待填写 |
| 未匹配字段处理 | 待填写 |
| 类型转换结果 | 待填写 |
| History 是否记录 | 待填写 |
| Restore 是否成功 | 待填写 |
| 是否通过 | 待填写 |

## P1 可选测试

| 动作 | 测试建议 | 是否测试 |
|---|---|---|
| 去重 | 按 `Order Key` 去重，观察 `A-005` 是否只保留一行 | 待填写 |
| 去空格 | 清理 `Channel Name` 和 `Note` 前后空格 | 待填写 |
| 大小写统一 | 将 `Channel Name` 统一为 lower 或 title case | 待填写 |
| 批量替换 | 把 `paid search`、` Paid Search ` 统一成 `Paid Search` | 待填写 |

