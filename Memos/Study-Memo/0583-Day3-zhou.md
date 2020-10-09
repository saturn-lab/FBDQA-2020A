### 课程小结3 周航宇 2017010583
#### python使用
```python
list=[3,5,1,2,3,4]
list.pop(0)
```
```python
print(list)
list.sort()
print(list)
```
```python
#dict set tuple
#tuple has index
a_tuple=(1,2,3)
```
```python
import scipy
scipy.__version__
```
```python
import numpy as np
c=np.array([[1,2],[3,4]])
c
```
```python
d=np.array(((1,2),(3,4)))
d
```
```python
(np.arange(4)+4)**2
```

```python
np.ones((3,3))
```

```python
np.arange(9).reshape(3,-1)
```

```python
A=np.array([1,2])
B=np.array([3,4])
np.dot(A,B)
```
```python
import matplotlib.pyplot as plt
b=np.array([40,20,50,70,10])
a=np.array([10,20,40,60,100])
plt.scatter(a,b)
plt.plot(a,b,color='r')
plt.show()
```
```python
t=np.arange(-2,2,0.01)
s=np.cos(t)
fig,ax=plt.subplots()
ax.plot(t,s,color='green',dashes=[2,2,10,2],label='test')
ax.set(xlabel='time',ylabel='voltage',title='test')
ax.grid(color='gray')
ax.legend()
plt.show()
```
```python
import pandas as pd
pd.__version__
#series
data=np.arange(9)+3
index=np.arange(9)
s=pd.Series(data,index=index,dtype=float)
print(s)
s+5
```

```python
import seaborn as sns
tip=sns.load_dataset('tips')
sns.displot(tip)
```

```python
sns.displot(tip,x='total_bill')
```

```python
sns.displot(tip,x="total_bill",y="tip",hue='sex')
```

```python
sns.displot(tip,x="total_bill",y="tip",kind='kde')
```

```python
anscombe=sns.load_dataset("anscombe")
sns.lmplot(x='x',y='y',data=anscombe.query("dataset=='III'"),ci=None)
```
#### 多因子模型
单因子，多因子，市场异常回报，因子投资
#### 美股因子分析
市值、规模、价值、动量、风险、质量
大市值、高价值、高动量、低波动、高质量
高价值在美股因子最有效，小市值比大市值好（EW>VW）
#### 因子的特点
周期性
#### 历史回测方式——A股
做多指标最高的股票，做空指标最低的股票组。
高年化回报：小市值股票减大市值股票、短期跌的多的股票减短期涨的多的股票
#### 一维零投资组合检验
选定研究因子、构建股票组合、计算收益差值、统计检验
#### 用行为金融学理解因子回报
小市值：前景理论（彩票效应）
高价值：反应过激和风险厌恶
高动量：反应不足和注意力偏差

### 创建自己的交易策略
#### 趋势跟随型策略
发现趋势，若趋势延续，则持有头寸，直到趋势完结；否则及时止损。
#### 趋势交易策略的要点
市场、头寸规模、入市时间、止损时间、退出时间、战术
#### 头寸规模
1.波动性N $$ N=(19\times PDN+TR)/20$$ PDN为前一日的波动性，TR为当日真实波动幅度 $$TR=Max(H-L,H-PDC,PDC-L)$$
2.头存规模单位=账户的1%/（N×每一点数所代表的美元）
3.头寸规模的限制

| 限制范围               | 头寸单位上线限 |
| ---------------------- | -------------- |
| 单个市场               | 4              |
| 高度关联的多个市场     | 6              |
| 松散关联的多个市场     | 10             |
| 单个方向（多头或空头） | 12             |

#### 海龟交易
系统1：以20日突破为基础的短期系统
系统2：以55日突破为基础的长期系统
##### 逐步建仓
在突破点建立1个单位的头寸，按N/2的价格间隔逐步扩大头寸（以上一份订单的实际成交价为基准），直到头寸达到规模上限。
##### 止损
价格变动的上限就是2N
对于加仓情况，止损点上浮
##### 退出
系统1：10日反向突破退出
系统2：20日反向突破退出
