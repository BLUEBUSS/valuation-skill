---
name: company_valuation
description: 专业公司估值分析技能。根据行业属性和生命周期选择估值方法，输出券商研报标准的估值报告。
---

# 公司估值分析技能

## 一、估值方法选择矩阵

### 1.1 按行业选择

| 行业 | 首选方法 | 辅助方法 | 核心指标 |
|------|----------|----------|----------|
| 科技/互联网 | EV/Revenue, EV/ARR | DCF | ARR, NRR, MAU |
| 银行 | PB, DDM | — | ROE, NIM, 不良率 |
| 保险 | PEV, P/EV | PB | 内含价值, NBV |
| 券商 | PB, PE | — | ROE, 市占率 |
| 制造业 | PE, EV/EBITDA | DCF | 产能利用率 |
| 消费品牌 | PE, EV/EBITDA | DCF | 同店增长 |
| 消费零售 | EV/EBITDA, PS | PE | 坪效 |
| 医药创新 | rNPV, 管线估值 | PS | 管线阶段, 成功概率 |
| 医药仿制 | PE, EV/EBITDA | — | 集采影响 |
| 能源/资源 | EV/EBITDA, PB | NAV | 储量, 周期位置 |
| 房地产 | NAV, PB | — | 土储货值 |
| 公用事业 | DDM, PE | — | 股息率 |

### 1.2 按生命周期选择

| 阶段 | 判断标准 | 首选方法 | **禁用** |
|------|----------|----------|----------|
| 初创期 | 无收入/亏损/增长>100% | VC法, 可比交易 | PE, PB, DCF |
| 成长期 | 增长30-100%, 亏损或微利 | DCF, PS, EV/ARR | PE(若亏损) |
| 成熟期 | 增长<20%, 稳定盈利 | PE, EV/EBITDA, DCF | **PS, EV/ARR** |
| 衰退期 | 收入下滑, 利润收窄 | PB, 清算价值 | PS |

> **重要**：成熟期盈利公司禁用PS，必须用PE/EV-EBITDA

### 1.3 大型多元化公司：必须用SOTP

适用：腾讯、阿里、苹果、微软等多业务公司（主营>3个且各占收入20%+）

SOTP步骤：拆分业务 → 各板块选可比公司 → 分别估值 → 加总 → 调整(+净现金 -控股折价10-20%)

详见 `references/comparable_company_selection_and_multiple_adjustment.md`

### 1.4 快速决策流程

1. 大型多元化公司？→ 必须SOTP
2. 确定行业 → 查1.1表
3. 判断生命周期 → 查1.2表，检查禁用方法
4. 特殊检查：亏损→不用PE | 成熟期→禁用PS | 并购→必须DCF | 高负债→用EV类
5. 选主方法+辅助方法（至少2种交叉验证）

---

## 二、核心估值方法

### 2.1 DCF
适用：成长/成熟期、现金流可预测
- 企业价值 = 预测期FCF现值 + 终值现值
- 终值用永续增长法或退出倍数法
- WACC、永续增长率参数详见 `references/wacc_calculation_and_adjustment.md`

### 2.2 相对估值

| 方法 | 适用 | 不适用 |
|------|------|--------|
| PE | 盈利稳定的成熟公司 | 亏损、周期底部 |
| PB | 金融、重资产、周期底部 | 轻资产高ROE |
| PS | **仅限**成长期亏损公司 | **成熟期盈利公司** |
| EV/EBITDA | 资本密集、高折旧、跨国比较 | — |

可比公司选择详见 `references/comparable_company_selection_and_multiple_adjustment.md`

### 2.3 行业特殊方法
- **DDM**：稳定分红公司（银行、公用事业）
- **NAV**：房地产
- **PEV**：保险（内含价值法）
- **rNPV**：创新药（风险调整净现值）

详见 `references/financial_valuation.md` 和 `references/pharma_valuation.md`

---

## 三、行业要点速查

| 行业 | 关键指标 | 参考倍数 |
|------|----------|----------|
| SaaS | ARR, NRR>120%优秀, LTV/CAC>3 | EV/ARR 8-20x |
| 银行 | ROE与PB匹配：ROE<10%→PB<1x | PB 0.5-1.2x |
| 保险 | 内含价值、新业务价值率 | P/EV 0.6-1.2x |
| 制造 | 周期顶用PB，周期底用正常化PE | PE 12-25x |
| 白酒 | 品牌力、提价能力 | PE 25-40x |
| 创新药 | 管线成功概率(I期12%/II期28%/III期55%) | rNPV |
| 房地产 | NAV折价(央企0-20%/民企20-60%) | PB 0.3-0.8x |

详细参数见 `references/industry_parameters.md`

---

## 四、估值输出规范

### 4.1 报告结构
1. **估值摘要**：目标价、评级、方法
2. **关键假设**：列表说明依据
3. **估值计算**：主方法+辅助方法过程
4. **敏感性分析**：核心变量±10-20%影响
5. **可比公司**：对比表
6. **风险提示**：至少3条

### 4.2 投资评级
| 评级 | 预期涨幅 |
|------|----------|
| 买入 | >15% |
| 增持 | 5-15% |
| 持有 | -5%~+5% |
| 减持 | -5%~-15% |
| 卖出 | <-15% |

---

## 五、校验与风险控制

### 5.1 交叉验证
- 至少2种方法，偏差应<20%
- 偏差>30%需剔除异常方法或检查假设

### 5.2 合理性检验
- 永续增长率不超过GDP+通胀(2-4%)
- 隐含PE应在行业历史10%-90%分位
- WACC与同行业差异<2%

### 5.3 币种规则
- A股用CNY，港股用HKD，美股用USD
- 跨市场需统一折算并注明汇率

### 5.4 常见错误
- 锚定偏差：不要从股价反推假设
- 周期陷阱：周期顶部不用当期PE
- 增长陷阱：高增长不能无限外推

---

## 六、References

- 生命周期判断：`references/lifecycle_assessment.md`
- 可比公司与SOTP：`references/comparable_company_selection_and_multiple_adjustment.md`
- WACC计算：`references/wacc_calculation_and_adjustment.md`
- 行业参数：`references/industry_parameters.md`
- 金融估值：`references/financial_valuation.md`
- 医药估值：`references/pharma_valuation.md`
- 房地产估值：`references/real_estate_valuation.md`
- 周期性行业估值：`references/cyclical_valuation.md`
- 估值案例：`references/valuation_cases.md`
