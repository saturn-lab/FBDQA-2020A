# 第八堂课总结

**<font size=4>航71  朱洁松  2017012150</font>**

## Python本地数据访问

### 原始文件读取 File I/O

文件打开关闭函数

```python
file = open(file_path,'r')
file.close()
```

读取函数

```python
with open(file_path,'r') as file:
    for line in file:
        print(line.strip())
```

写入函数

```python
with open(file_path,'w') as file:
    file.write('This is my first file')
```



### 将对象写入磁盘

```python
import pickle
pkl_file = open(path + 'data.pkl','wb')
pickle.dump(a,pkl_file)
```

### 从磁盘读取对象

```python
pkl_file = open(path + 'data.pkl','rb')
b = pickle.load(pkl_file)
```

### 写入文本文件

```python
import pandas as pd
csv_file = open(path + 'data.csv','w')
header = 'date,no1,no2'
csv_file.write(header)
for t_,(no1,no2) in zip(t,a):
    s = '%s,%f,%f\n' %(t_,no1,no2)
csv_file.close()
```

### 读取文本文件

```python
csv_file = open(path + 'data.csv','r')
for i in range(5):
    print(csv_file.readline(),end='')
```

### 使用SQLite数据库

```python
import sqlite3 as sq3
con = sq3.connect(path + 'numbs.db')
query = 'CREATE TABLE numbs(Date date,No1 real,No2,real)'
con.execute(query)
import datetime as dt
con.execute('INSERT INTO numbs VALUES(?,?,?)',(dt.datetime.now(),0.12,7.3))
con.execute('SELECT * FROM numbs')
```

### 读写NUMPY数组



```python
import numpy as np
dtimes = np.arange('2015-01-01 10:00:00','2021-12-31 22:00:00',dtype='datetime64[m]')
dty = np.dtype([('Date','datetime64[m]'),('No1','f'),('No2','f')])
data = np.zeros(len(dtimes),dtype=dty)
data['Date'] = dtimes
a = np.random.standard_normal((len(dtimes),2)).round(5)
data['No1'] = a[:,0]
data['No2'] = a[:,1]
np.save(path + 'array',data)
np.load(path + 'array.npy')
```

### Pandas的I/O

读取csv文件

```python
data.to_csv(filename + '.csv')
pd.read_csv(filename + '.csv')[['No1','No2']].hist(bins = 20)
```

读取excel文件

```python
data[:10000].to_excel(filename + '.xlsx')
pd.read_excel(filename + '.xlsx','Sheet1').cumsum().plot()
```

使用SQLite数据库

```
data = pd.read_sql('SELECT * FROM numbers',con)
data.head()
```



## 凸优化

全局最小优化：brute函数（import scipy.optimize as spo）

局部最小优化：fmin函数

凸优化的前提条件是函数是凸函数，算的值是最小值。最大值可以转化成最小值。

### 全局优化

通过一个选项输出当前参数值和函数值

brute函数以参数范围作为输入

通过给定的函数初始参数化条件得到最优参数

通过微调达到更好的结果

### 局部优化

利用全局优化的结果

fmin函数输入需要最小化的函数和起始参数值

此外可以定义输入参数宽容度和函数值宽容度，以及最大迭代及函数调用次数

建议在局部优化之前进行全局优化。主要原因是局部凸优化算法容易陷入某个局部最小值，而忽略“更好”的局部最小值和全局最小值

### 有约束优化

约束可能采取等式或不等式形式

例：两种证券今天的价格均为 10 美元。一年之后，状态 u 下的价格分别为 15美元和 5美元，状态 d 下的价格分别为 5美元和12美元。两种状态的可能性相同。假设投资预算为100美元，效用函数为 u(w) = sqrt(w)

最优化问题公式

> $$
> \max_{a,b}E(u(w))=p\sqrt{w_u}+(1-p)\sqrt{w_d}\\
> p = 0.5\\
> w_u = 15a+5b\\
> w_d = 5a+12b\\
> 100\geq 10a+10b\\
> a,b \geq 0
> $$

minimize函数，设置约束条件和边界

## 逼近

在给定区间通过回归和插值求取函数的近似值

### 回归

单项式作为基函数：1、x、x^2...

polyfit函数

| 参数 | 描述                         |
| ---- | ---------------------------- |
| x    | x坐标（自变量）              |
| y    | y坐标（因变量）              |
| deg  | 多项式拟合度                 |
| full | 如果为真，返回额外的诊断信息 |
| w    | 应用到y坐标的权重            |
| cov  | 如果为真，返回协方差矩阵     |

单独的基函数，必须使用np ndarray对象，通过一个矩阵方法定义

numpy.linalg子库提供lstsq函数，以解决最小二乘优化问题，应用lstsq函数可以得到单个基函数的最优参数

```python
matrix = np.zeros((3+1,len(x)))
matrix[3,:] = x**3
matrix[2,:] = x**2
matrix[1,:] = x
matrix[0,:] = 1
reg = np.linalg.lstsq(matrix.T,f(x))[0] # 获得权系数向量w
y_hat = np.dot(reg,matrix) # 获得回归预测结果
```

回归对于有噪声的数据和未排序的数据都有很好的处理

多维回归（x,y）

```python
matrix = np.zeros((len(x),6+1))
matrix[:,6] = np.sqrt(y)
matrix[:,5] = np.sin(x)
matrix[:,4] = y**2
matrix[:,3] = x**2
matrix[:,2] = y
matrix[:,1] = x
matrix[:,0] = 1
import statsmodels.api as sm
model = sm.OLS(f(x,y),matrix).fit()
model.rsquared
model.summary
model.params
```



## 经典资金管理模型

### 资金管理的意义

策略成败的3个核心变量

> 方向、时机、头寸

头寸决定了赚取何亏钱的量

模型1：每一固定金额交易一个单位

> 总资金：一百万 平均分为10份，每份金额：10万 
>
> 交易实例一： 待买入标的：工商银行  价格：5元   一个交易单位 = 100股  买入数量 = 100股 买入金额 = 5 * 100 = 500元 
>
> 交易实例二： 待买入标的：贵州茅台 价格：750元  一个交易单位 = 100股 买入数量 = 100股 买入金额 = 750 * 100 = 7.5万

模型2：等价值交易单位

> 总资金：一百万 平均分为10份，每份金额：10万 
>
> 交易实例一： 待买入标的：工商银行 价格：5元  买入数量 = 100000 / 5 = 20000股 买入金额 = 10万 
>
> 交易实例二： 待买入标的：贵州茅台 价格：750元  买入数量 = 100000 / 750 = 100股 买入金额 = 7.5万

模型3：百分比风险模型

> 总资金：一百万  总风险：1%  单个交易标的风险：5% 
>
> 交易实例： 待买入标的：海康威视 价格：40元 买入数量 = （ 1000000 * 1% ）/（40 * 5%）= 5000股 买入金额 = 40 * 5000 = 20万

模型4：百分比波动模型

> 总资金： 一百万 总风险：1%   单个交易标的风险：3倍ATR 
>
> 交易实例： 待买入标的：海康威视 价格：40元 ATR = 0.8 买入数量 = （ 1000000 * 1% ）/（0.8 * 3）= 4100股 买入金额 = 40 * 4100 = 16.4万

### 细节考虑

流动性风险

> 持仓头寸：不超过该股票流通市值的2%，避免成为大股东
>
> 日成交量：不超过该股票成交量的10%
>
> 商品期货：风险为被逼多或逼空。

资金

> 单日可用资金上限
>
> 单个交易标的资金上限
>
> 总可用资金上限
>
> CPR公式：P（头寸风险）= C（总风险）/R（每股风险）

总风险

> 根据个人的容忍程度确定
>
> 资金的强制平仓线

预警线0.9、清盘线0.85

单个头寸的风险

> 固定风险、波动率
>
> 头寸数量 = 总风险 / 单个头寸风险
>
> 总风险 = 总资产*总风险比率 
>
> 单个头寸风险 = 交易标的价格 * 单个头寸风险比率 
>
> 头寸数量 = （总资产*总风险比率）/（交易标的价格 * 单个头寸风险比率） 
>
> （头寸数量*交易标的价格 ）/ 总资产 = 总风险比率 /单个头寸风险比率 
>
> 一次交易资金比例 =总风险比率 /单个头寸风险比率
>
> 假设总风险比率为3%，单个头寸风险比率为6%，一次交易资金比例为50%

解决办法

> 最大持仓上限：一次交易资金比例 < 最大持仓上限
>
> 平均分配风险：头寸数量 = （总风险 / N）/ 单个头寸风险。资金利用不充分

头寸规模定期调整

> 初始风险：投资组合建立之初所指定的总风险
>
> 持续风险：投资组合存续执行过程中所暴露的总风险
>
> 每隔固定的时间评估当前持仓的持续风险，如果风险暴露大于总风险，则需要进行减仓

实例

>  风险定义：总资金200,000   初始风险2%，4,000   持续风险暴露上限3%
>
> 价格每股400元时建仓4手：使用资金160,000 
>
> 止损390，风险暴露(400-390) * 400 = 4,000
>
> 如果价格涨到每股440元 ，止损410（假设按照波动率计算），风险暴露12,000  
>
> 允许风险暴露（ 200000+40 * 400 ）*3%=6,480 
>
> 结论：平仓2手，风险暴露降一半为 6,000

加减仓

> 价格每上涨一定的幅度（如一个ATR），执行加仓一次
>
> 针对加仓部分和原有持仓，根据新的ATR调整为相同的止损位置(价格减去ATR)， 降低单位头寸的风险
>
> 保证加仓后的风险暴露<总风险

### 股票池避险

资产负债表

> 陷阱一：货币资金余额比短期负债小很多，短期偿债危机
>
> 陷阱二：货币资金充裕，但有较多的有息或高息负债
>
> 陷阱三：定期存款多，其他货币多，流动资金少
>
> 陷阱四：其他货币数额大，但没有合理解释

现金流量表

利润表

所有者权益变动表

本福特定律

> 自然数出现的频率有规律