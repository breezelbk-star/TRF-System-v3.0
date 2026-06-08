# TRF v3.0 - State Mapping Table

Version: RC1 Final
Author: Jimmy Li + GPT
Status: Core Mapping

---

# 0. 文件定位

本文件负责：

State

↓

Execution

之间的映射关系。

---

输入：

Market State

Sector State

Stock State

---

输出：

Allowed Position

Allow Buy

Allow Add

Allow Reentry

Allow Rolling

Risk Level

---

QMT未来直接读取本文件。

---

# 1. 状态来源

状态定义统一由：

00_ARCHITECTURE/
TRF-Master-State-Machine.md

负责。

---

本文件不负责定义状态。

只负责映射。

---

# 2. Market Mapping

| State | Position Limit | Risk |
|---------|---------|---------|
| GREEN | 80% | LOW |
| YELLOW | 50% | MEDIUM |
| RED | 20% | HIGH |

---

# 3. Sector Mapping

| State | Position Limit | Description |
|---------|---------|---------|
| S0 | 20% | 萌芽 |
| S1 | 50% | 启动 |
| S2 | 80% | 主升 |
| S3 | 50% | 高潮 |
| S4 | 20% | 退潮 |

---

# 4. Stock Mapping

| State | Position Limit | Description |
|---------|---------|---------|
| A | 80% | 趋势健康 |
| B | 70% | MA5预警 |
| C | 50% | MA10转弱 |
| D | 30% | MA20防守 |
| E | 10% | MA30退出观察 |

---

# 5. 仓位计算规则

最终允许仓位：

MIN(

Market Limit,

Sector Limit,

Stock Limit

)

---

示例：

Market = GREEN

80%

---

Sector = S2

80%

---

Stock = C

50%

---

最终允许仓位：

50%

---

示例：

Market = YELLOW

50%

---

Sector = S2

80%

---

Stock = A

80%

---

最终允许仓位：

50%

---

# 6. Buy Permission

允许建仓：

Market = GREEN

AND

Sector = S1 或 S2

AND

Stock = A

---

否则：

Allow Buy = NO

---

# 7. Add Permission

允许加仓：

Market = GREEN

AND

Sector = S2

AND

Stock = A

---

否则：

Allow Add = NO

---

# 8. Reentry Permission

允许回补：

Market ≠ RED

AND

Sector ≠ S4

AND

Stock ≠ D

AND

Stock ≠ E

---

否则：

Allow Reentry = NO

---

# 9. Rolling Permission

允许滚动仓：

Market = GREEN

AND

Sector = S2

AND

Stock = A 或 B

---

否则：

Allow Rolling = NO

---

# 10. Exit Priority

Stock = B

↓

预警

↓

观察

---

Stock = C

↓

减仓至50%

---

Stock = D

↓

减仓至30%

---

Stock = E

↓

减仓至10%

---

# 11. Sector Priority

S2

↓

允许主仓

---

S3

↓

允许减仓

禁止追高

---

S4

↓

禁止主仓

禁止回补

---

# 12. Market Priority

RED

优先级最高

---

当：

Market = RED

---

无论：

Sector

Stock

状态如何

---

最终允许仓位：

20%

---

现金优先。

---

# 13. QMT Output

系统输出：

Current Market State

Current Sector State

Current Stock State

Allowed Position

Allow Buy

Allow Add

Allow Reentry

Allow Rolling

Risk Level

---

QMT只执行输出结果。

---

# 14. Future Upgrade

Stock State

未来升级方向：

A = 趋势健康

B = 短期转弱

C = 结构转弱

D = 趋势破坏

E = 退出观察

---

均线不再作为唯一判断依据。

---

Version:

TRF v3.1 Planned
