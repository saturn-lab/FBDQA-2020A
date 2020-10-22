# WW5

## 量化策略

### 股票池

* 选股条件
  * 市值
  * 估值
  * 超跌
  * ST股票（有退市风险）
* 再平衡
* 容量

### 选股因子

各因子加权

单因子评分方法：

* 直接打分
* 排序打分

### 均值回复型策略

小幅震荡，大幅趋势

做多表现最佳组合；做空最糟糕的组合（A股不太能做空）

### 量化交易策略的评价

风险：

* 标准差
* 半方差，目标半方差
* 下行风险
* 损失概率
* ……

风险分散化

夏普比率$[E(R_p)-R_f]/\sigma_p$

最大回撤

#### Alpha

风险对冲，做空股指期货，获得纯α收益

$\beta_P=\frac{Cov\{r_P,r_B\}}{Var(r_B)}$
$$
\sigma_P^2=\frac1T \sum_{t=1}^T r_P^2(t)-\frac1T\sum_{t=1}^Tr_P(t)\cdot\frac1T\sum_{t=1}^Tr_P(t)\\
\omega_P^2=\sigma_P^2-\beta_P^2\cdot \sigma_B^2, 残差风险
$$
$\alpha$需要年化

## SQL

```python
import sqlite3

db = sqlite3.connect("university.db")
cursor = db.cursor()
cursor.execute("""CREATE TABLE IF NOT EXIST students(
id integer PRIMARY KEY,
name text NOT NULL,
class text NOT NULL,
grade integer)
""")
cursor.execute("INSERT INTO students(id, name, class, grade) \
values({},"{}","{}",{})".format(someid,somename,someclass,somegrade)) # 插入数据

cursor.execute("""CREATE TABLE IF NOT EXIST classes(
id integer PRIMARY KEY,
name text ,
grade integer NOT NULL,
number interger NOT NULL
)
""")

## 选择
cursor.execute("SELECT * FROM table_name")
cursor.fetchall() # 所有数据

SELECT id,name FROM table_name \
ODER BY col_name \
WHERE grade > 50 AND name = 'Julia'

UPDATE students SET name = 'Leo' WHERE id = 42

DELETE students WHERE id = 81

db.commit() # 必须commit，更改才会保存下来

db.close() # 操作结束后一定要关闭
```

## DBeaver