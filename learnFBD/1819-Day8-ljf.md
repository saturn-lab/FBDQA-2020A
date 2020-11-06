# Day8-1819-ljf

## 金融大数据

### Python数据访问

#### 基本IO

```python
file = open(file_path, 'r') #打开文件 b二进制 w只写 r只读 +写读
file.close() # 关闭

file.write('input something')

for line in file:
    print(line.strip()) # 删除末尾
```

pickle模块

```python
import pickle
pkl_file = open(path + 'data.pkl', 'wb')
pickle.dump(a, pkl_file) # 写入磁盘
b = pickle.load(pkl_file) # 读取
```

csv

```python
csv_file = open(path + 'data.csv', 'r')
print(csv_file.readline(), end='')
```

SQLite

```python
import sqlite3 as sq3
con = sq3.connect(path + 'data.db')
query = 'CREATE TABLE numbs (Date date, No1 real, No2 real)'
con.execute(query)
import datetime as dt
con.execute('INSERT INFO numbs VALUES(?, ?, ?)',(dt.datetime.now(),0.12,7.3))
con.execute('SELECT * FROM numbs')
# 输出[('time',0.12, 7.3),]
```

Numpy

```python
np.save(path + 'name', data) # 自动添加.npy后缀
np.load(path)
```

#### Pandas

支持

* CSV
* SQL
* XLS/XLSX
* JSON
* HTML

```python
data.to_csv(filename) # np转csv
pd.read_csv(filename)[['No1','No2','No3']] #pd读取csv
pd.read_sql('SELECT * FROM numbers', con) #读取sql
```



### Python数学模型工具

#### 凸优化

```python
import scipy.optimize as spo
# 2个函数
# 全局优化
b = spo.brute(f,((-10,10,0.1),(-10,10,0.1)),finish=None) # f优化函数，取值范围；输出最优解
fm(b) # 输出值
# 局部优化
spo.fmin(f,(2,2), maxiter=250) # f, 起始值
# 可以在全局找到一个解之后局部优化，避免局部最小
```

有约束凸优化

```python
constraints=({'type':'ineq','fun':lambda p: 100-p[0]*10 - p[1]*10})
bounds = ((0,10000),(0,10000))
result = spo.minimize(f,[5,5],method='SLSQP',constraints=,bounds = )
```

#### 积分

#### 符号运算

#### 逼近法

> 求函数的近似表示

* 插值比较复杂
* 回归比较高效快速，需要确定基函数

```python
reg = np.polyfit(x,f(x),deg=5)#拟合次数
ry = np.polyval(reg)

#误差检验
np.allclose(f(x),ry)
np.sum((f(x)-ry))/len(x) # MSE
```

练一练

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

def f(x):
    return cos(x)+sin(2*x)+x**2
x= linspace(-2*np.pi, 2*np.pi, 200)
plt.plot(x,f(x)) # 画出
reg = np.polyfit(x, f(x), deg=23)
ry = np.polyval(reg, x)
np.allclose(f(x),ry)
# True
np.sum((f(x)-ry)**2)/len(x)
# 2.7061888537481193e-12
```

指定基函数

```python
matrix = np.zeros((3 + 1, len(x)))
matrix[3, :] = x ** 3
matrix[2, :] = x ** 2
matrix[1, :] = x
matrix[0, :] = 1
# 最小二乘优化
reg = np.linalg.lstsq(matrix.T, f(x))[0]
ry = np.dot(reg, matrix)
```



其他意义：

* 回归在一定程度上平均了噪声
* 无缝处理未排序的数据
* 可以迅速应用到多维的情况中

多维

```python
matrix = np.zeros((len(x), 6 + 1))
matrix[:, 6] = np.sqrt(y)
matrix[:, 5] = np.sin(x)
matrix[:, 4] = y ** 2
matrix[:, 3] = x ** 2
matrix[:, 2] = y
matrix[:, 1] = x
matrix[:, 0] = 1
model = sm.OLS(fm((x, y)), matrix).fit()
a = model.params
RZ = reg_func(a, (X, Y))
```



## 量化：经典资金管理模型以及股票池筛选的量化避险问题讨论

### 资金管理模型

头寸决定赚多赚少，亏多亏少；初学者常遇到的问题是，头寸管理，即使有90%的胜率，但头寸管理不佳实际亏损。

* 模型1：固定交易单位（每只股票买入100股）
* 模型2：等价值交易单位（每只股票买入10w）
* 模型3：百分比风险模型（买入 总资金×总风险/ 股价×单只风险 股）
* 模型4：百分比波动幅度模型
  * 风险：3倍ATR（历史平均波动）
  * 购买 总资金×总风险/ 股价×单只风险

###### 流动性风险

* 持仓头寸不超过该股票流通市值2%
  * 买到5%就要持牌了，不要买成大股东
* 日交易量不超过该股票成交量的10%

###### 细节考虑

* 单日可用资金上限
* 单个交易标的资金上限
* 总可用资金上限

CPR公式
$$
P = C/R
$$
C现金风险



> 根据客户的偏好
>
> * 预警线：大多数产品0.9
> * 清盘线：大多数0.85

#### 单个头寸的风险

一次交易资金比例 = 总风险比率/单个头寸风险比率

解决方法：

* 最大持仓上限
  * 一次交易资金比例 < 最大持仓上限
* 平均分配风险
  * 资金利用不充分，每一次不一定能够全买下，可能花不出去

##### 头寸规模的定期调整

* 初始风险
* 持续风险

每隔固定时间评估当前持仓；如果风险上升，应该减仓

ATR

### 股票池筛选中的避险问题

* 资产负债表
  * 货币资金余额比短期负债小很多：短期偿债危机
  * 货币资金充裕，但有较多的有息或高息负债
  * 定期存款多，其他货币多，流动资金少
  * 其他货币数额大，但没有合理解释
  * 造假：临时的，虚构的，被冻结的，早就被大股东占用的资金
* 现金流表
* 利润表
* 所有者权益变动表

#### 本福特定律

越大的数，以它为首几位数出现的概率就越低

![](https://qn-st0.yuketang.cn/FhcP-yt_COoUCEgMM9jkjCrl8zA3)

