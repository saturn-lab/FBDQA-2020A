# 1819-Day4-ljf

第四周学习小结

## 金融基础知识

### 金融基础概念

>  定义：资源的分配

### 金融市场和制度

#### 金融市场

##### 金融资产

有产权的任何物品

流动性：变现的难易程度，成交价格的变动幅度；现金》债券》基金》股票》房产 往往也是风险的顺序

#### 交易制度

### 资产定价与投资学

#### 资产价格的决定

$P=\sum_{t=1}^{n} \frac{E(CF_t)}{(1+r)^t}$

* r是折现率
* $E(CF_t)$是预期现金流

#### 资产收益率的影响因素

* 超额风险收益
* 更多因子模型……

#### 投资组合理论

Efficient Frontier

### CAPM模型

风险：

系统性风险：和市场相关的风险

公司风险：经营风险：破产……



## 聚宽平台的使用

```python
from jqdatasdk import *
auth('13121283966', 'the password')
pd.set_option('display.max_rows',10)
```



## 量化交易策略开发案例

量化策略：

* **股票池** - 买什么
* **买卖信号** - 择时 - 什么时候买
  * 买入
  * 卖出
* 头寸管理 - 买多少
* 风险管理 - 遇到风险怎么办
* 执行

### 选择股票池

低估值 PE：市盈率

小市值低估值

ROE（净资产收益率）是反映公司质量的重要指标

* 选股条件

* 容量
* 再平衡周期



练习一

在174行将原代码改为

```python
if pl_stock['pe_ratio'] == None or math.isnan(pl_stock['pe_ratio']) or float(pl_stock['pe_ratio']) < 20 or float(pl_stock['pe_ratio']) > 40:
```

练习二

在第17行

```python
PL_CHANGE_STOCK_POOL_DAY_NUMBER = 30
```

在`pl_load_fundamentals_data`函数中，扩展`pl_raw_data_item`

```python
        pl_raw_data_item = {
            'code'      :pl_df['code'][pl_index],
            'pe_ratio'  :pl_df['pe_ratio'][pl_index],
            'valuation' :pl_df['market_cap'][pl_index]
            }
```

在更新时`pl_stock_pool`，剔除valuation不足100的公司，条件更新为

```python
        if pl_stock['pe_ratio'] == None or math.isnan(pl_stock['pe_ratio']) 
            or float(pl_stock['pe_ratio']) < 20 or float(pl_stock['pe_ratio']) > 40 or
            pl_stock['valuation'] == None or math.isnan(pl_stock['valuation']) or 
            float(pl_stock['valuation']) < 100:
```





### 择时

* 均线
* 趋势
* 摆动
* 能量

金叉/死叉

* 金叉买入
* 死叉卖出

练习一

```python
# 买入信号中的短时均线长度
PL_BUY_SHORT_MA  = 10
# 买入信号中的长时均线长度
PL_BUY_LONG_MA   = 60
# 卖出信号中的短时均线长度
PL_SELL_SHORT_MA = 10
# 卖出信号中的长时均线长度
PL_SELL_LONG_MA  = 60
```

练习二

```python
# 买入信号中的短时均线长度
PL_BUY_SHORT_MA  = 1
# 买入信号中的长时均线长度
PL_BUY_LONG_MA   = 20
# 卖出信号中的短时均线长度
PL_SELL_SHORT_MA = 1
# 卖出信号中的长时均线长度
PL_SELL_LONG_MA  = 20
```