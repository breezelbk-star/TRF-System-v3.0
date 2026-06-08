# TRF v3.0 - State Mapping Table

Version: RC1
Author: Jimmy Li + GPT
Status: Core Mapping

---

# 0. 文件作用

本文件是：

TRF状态机

↓

QMT执行系统

之间的转换表。

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

# 1. 最高原则

最终仓位：

取最小值原则

---

例如：

Market：

GREEN

80%

---

Sector：

S2

80%

---

Stock：

A

80%

---

最终：

80%

---

# 2. Market Mapping

GREEN

允许仓位：

80%

风险等级：

LOW

---

YELLOW

允许仓位：

50%

风险等级：

MEDIUM

---

RED

允许仓位：

20%

风险等级：

HIGH

---

# 3. Sector Mapping

S0

20%

观察

---

S1

50%

建仓

---

S2

80%

主升

---

S3

50%

高潮

---

S4

20%

退潮

---

# 4. Stock Mapping

A

80%

趋势健康

---

B

70%

预警

---

C

50%

转弱

---

D

30%

防守

---

E

10%

退出观察

---

# 5. 仓位计算公式

Allowed Position

=

MIN

(

Market Limit,

Sector Limit,

Stock Limit

)

---

# 6. 执行动作映射

GREEN + S2 + A

↓

80%

↓

Allow Buy = YES

Allow Add = YES

Allow Reentry = YES

Allow Rolling = YES

---

GREEN + S3 + A

↓

50%

↓

Allow Buy = NO

Allow Add = NO

Allow Rolling = YES

↓

优先卖滚动仓

---

GREEN + S2 + B

↓

70%

↓

Allow Add = NO

↓

观察

---

GREEN + S2 + C

↓

50%

↓

Allow Add = NO

↓

允许减仓

---

GREEN + S2 + D

↓

30%

↓

禁止补仓

↓

滚动仓清零

---

GREEN + S2 + E

↓

10%

↓

观察仓

↓

禁止交易

---

# 7. YELLOW市场

YELLOW + S2 + A

↓

50%

↓

允许试仓

↓

禁止满仓

---

YELLOW + S3 + A

↓

50%

↓

减仓优先

---

YELLOW + S4 + 任意

↓

20%

↓

观察

---

# 8. RED市场

RED + 任意 + 任意

↓

20%

↓

防守优先

↓

现金优先

↓

禁止重仓

---

# 9. 回补权限

允许：

GREEN

+

S2

+

A

---

允许：

GREEN

+

S1

+

A

---

禁止：

RED

---

禁止：

S4

---

禁止：

D

---

禁止：

E

---

# 10. 滚动仓权限

允许：

GREEN

+

S2

+

A

---

允许：

GREEN

+

S2

+

B

---

禁止：

C

D

E

---

# 11. 龙头特殊规则

龙头股：

允许提前试仓

---

条件：

S2

+

A

+

靠近MA30

---

允许：

总资产10%

试仓

---

普通股：

必须重新站回MA20

---

# 12. TRF最终决策树

Step 1

判断Market

---

Step 2

判断Sector

---

Step 3

判断Stock

---

Step 4

计算Allowed Position

---

Step 5

判断：

Allow Buy

Allow Add

Allow Reentry

Allow Rolling

---

Step 6

执行QMT

---

# 13. 拓荆科技案例

阶段1

GREEN

S2

A

↓

80%

↓

主仓

---

阶段2

GREEN

S3

A

↓

50%

↓

卖滚动仓

---

阶段3

GREEN

S3

C

↓

50%

↓

禁止补仓

---

阶段4

GREEN

S4

D

↓

20%-30%

↓

防守

---

阶段5

GREEN

S4

E

↓

10%

↓

观察仓

---

# 最终铁律

市场决定仓位。

板块决定方向。

个股决定执行。

状态机决定动作。

QMT只执行结果。
