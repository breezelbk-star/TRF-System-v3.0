# TRF v3.0 - Master State Machine

Version: 3.0
Author: Jimmy Li + GPT
Status: Core System

---

# 0. 核心思想

TRF不是选股系统。

TRF本质是状态机系统。

---

市场决定仓位。

板块决定方向。

个股决定执行。

---

执行顺序：

Market

↓

Sector

↓

Stock

↓

Position

↓

Execution

---

任何模块发生冲突：

优先服从上一级。

---

# 1. 三层状态结构

Level 1：

Market State

市场状态

---

Level 2：

Sector State

板块状态

---

Level 3：

Stock State

个股状态

---

# 2. Market State

GREEN

市场进攻

---

YELLOW

市场震荡

---

RED

市场防守

---

仓位上限：

GREEN：

100%

---

YELLOW：

70%

---

RED：

30%

---

说明：

市场状态决定仓位天花板。

---

# 3. Sector State

S0

萌芽

---

S1

启动

---

S2

主升

---

S3

高潮

---

S4

退潮

---

说明：

板块状态决定操作方向。

---

仓位上限：

S0：

20%

---

S1：

50%

---

S2：

80%

---

S3：

50%

---

S4：

20%

---

# 4. Stock State

A

趋势健康

MA5 > MA10 > MA20

---

B

预警

跌破MA5

---

C

转弱

跌破MA10

---

D

防守

跌破MA20

---

E

退出观察

跌破MA30

---

说明：

个股状态决定具体执行动作。

---

# 5. 仓位计算规则

最终允许仓位：

取最小值原则

---

例如：

Market：

GREEN

允许：

100%

---

Sector：

S2

允许：

80%

---

Stock：

A

允许：

80%

---

最终：

80%

---

# 6. 状态映射表

GREEN + S2 + A

↓

80%

↓

允许加仓

↓

允许滚动仓

---

GREEN + S3 + A

↓

50%

↓

允许减仓

↓

禁止追高

---

GREEN + S2 + C

↓

50%

↓

禁止补仓

↓

降低仓位

---

GREEN + S4 + D

↓

20%

↓

退出主仓

↓

保留观察仓

---

RED + S2 + A

↓

30%

↓

防守优先

---

说明：

永远取最低风险状态。

---

# 7. 买入权限

只有满足：

Market GREEN

+

Sector S1/S2

+

Stock A

---

允许建立主仓

---

否则：

禁止重仓

---

# 8. 补仓权限

只有满足：

Sector S2

+

Stock A

---

允许加仓

---

Stock C

↓

禁止补仓

---

Stock D

↓

禁止补仓

---

Stock E

↓

禁止补仓

---

# 9. 滚动仓权限

允许：

Market GREEN

+

Sector S2

+

Stock A

---

禁止：

Stock D

Stock E

---

# 10. 情绪高潮处理

Sector S3

触发：

优先卖滚动仓

---

仓位：

80%

↓

50%

---

现金增加

---

# 11. 状态切换

Market

GREEN

↓

YELLOW

↓

RED

---

Sector

S0

↓

S1

↓

S2

↓

S3

↓

S4

---

Stock

A

↓

B

↓

C

↓

D

↓

E

---

禁止跨级恢复。

---

例如：

E

↓

A

禁止

---

必须：

E

↓

D

↓

C

↓

B

↓

A

---

# 12. QMT输出参数

系统最终输出：

Current Market State

Current Sector State

Current Stock State

Allowed Position

Allow Buy

Allow Add

Allow Reentry

Allow Rolling

Allow Exit

---

QMT只执行结果。

不判断逻辑。

---

# 13. 拓荆科技案例

阶段1

GREEN

S2

A

↓

80%

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

仓位管理高于选股。

现金也是仓位。

永远服从状态机。
