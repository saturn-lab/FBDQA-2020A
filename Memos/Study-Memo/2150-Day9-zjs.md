# 第九堂课总结

**<font size=4>航71  朱洁松  2017012150</font>**

## 积分

### 数值积分

函数库：scipy.integrate

> 包含一组精选的函数，可以计算给定上下限和数学函数下的数值积分
>
> 包含用于固定高斯求积的 fixed_quad、用于自适应求积的 quad 和用于勒贝格积分的 romberg 程序库
>
> 还有一些积分函数以输入列表或者包含函数值和输入值的 ndarray 对象作为输入。包括使用梯形法则的 trapz，和实现辛普森法则的 simps 程序库

scipy.integrate 只能求定积分

```python
import scipy.integrate as sci
def f(x):
    return np.sin(x) + 0.5 * x
a = 0.5  # left integral limit
b = 9.5  # right integral limit
sci.fixed_quad(f, a, b)[0]
sci.quad(f, a, b)[0]
sci.romberg(f, a, b)
xi = np.linspace(0.5, 9.5, 25)
sci.trapz(f(xi), xi)
sci.simps(f(xi), xi)
```

### 蒙特卡洛积分

通过蒙特卡洛模拟的期权和衍生品的估值依赖于通过模拟求取积分

> 在积分区间内取1个随机的 x 值，并计算每个随机 x 值处的积分函数值。
>
> 加总所有函数值并求其平均值，就可以得到积分区间中的平均函数值。
>
> 将该值乘以积分区间长度，得到估算的积分值。

积分值随着提取的随机数个数的增加而收敛。

```python
for i in range(10, 100, 10):
    np.random.seed(1000)
    x = np.random.random(i) * (b - a) + a
    print(np.sum(f(x)) / len(x) * (b - a))
```



## 符号数学

### 符号计算—SymPy库

> 引入新的对象类，最基本的是Symbol类
>
> SymPy中的函数定义中，x没有数字值
>
> SymPy通常自动简化给定的数学表达式

```python
import sympy as sy
x = sy.Symbol('x')  # 需要先定义（创建）符号对象
y = sy.Symbol('y')
```

```python
3 + sy.sqrt(x) - 4 ** 2
```

​		 $\sqrt{x}-13$

```python
f = x ** 2 + 3 + 0.5 * x ** 2 + 3 / 2
sy.simplify(f)
```

​		$1.5x^2+4.5$

### 符号计算—方程式

Sympy求解的是使指定表达式为0的方程解。必要时方程式需要改写，才能得出结果。但是不保证有解。

```python
sy.solve(x ** 2 - 1)
[-1,1]
sy.solve(x ** 2 - 1 - 3)
[-2,2]
sy.solve(x ** 2 + y ** 2)
[{x: -I*y}, {x: I*y}]  # x与y满足这样的条件，I是虚数单位
sy.solve(x ** 3 + 0.5 * x ** 2 - 1)
[0.858094329496553, -0.679047164748276 - 0.839206763026694*I, -0.679047164748276 + 0.839206763026694*I]
```

### 符号计算—积分

SymPy可以求出积分函数的反导数（不定积分、原函数）

```python
a, b = sy.symbols('a b')
# sinx + 0.5x 在区间（a,b）上关于x的定积分
int_func_limits = sy.Integral(sy.sin(x) + 0.5 * x, (x, a, b))
int_func_limits.subs({a : 0.5, b : 9.5}).evalf()

# sinx + 0.5x 关于x的不定积分
int_func = sy.integrate(sy.sin(x) + 0.5 * x, x)

Fb = int_func.subs(x, 9.5).evalf()
Fa = int_func.subs(x, 0.5).evalf()
# 计算sinx + 0.5x 在区间（a,b）上关于x的定积分
Fb - Fa 

sy.integrate(sy.sin(x) + 0.5 * x, (x, 0.5, 9.5))
# 注意要用 sy.sin() 而不是 np.sin()
```

### 符号计算—微分

全局最小值的必要（但不充分）条件之一是两个偏微分都为0。但是不能保证有符号解。算法和存在性问题都会影响问题的解。

```python
int_func = sy.integrate(sy.sin(x) + 0.5 * x, x)
# 求微分
int_func.diff()
# 0.5*x + sin(x)

f = (sy.sin(x) + 0.05 * x ** 2 + sy.sin(y) + 0.05 * y ** 2)
del_x = sy.diff(f, x)
# 0.1*x + cos(x) 求得f关于x的偏微分
del_y = sy.diff(f, y)
# 0.1*y + cos(y)
xo = sy.nsolve(del_x, -1.5)
# -1.42755177876459 求x偏微分为0时x的取值，在-1.5附近
yo = sy.nsolve(del_y, -1.5)
f.subs({x : xo, y : yo}).evalf() 
# -1.77572565314742 求得f的全局最小值

xo = sy.nsolve(del_x, 1.5)
# 1.74632928225285 求x偏微分为0时x的取值，在1.5附近
yo = sy.nsolve(del_y, 1.5)
f.subs({x : xo, y : yo}).evalf()
# 2.27423381055640 求得f的局部最小值
```



## 高性能计算库

### numexpr：快速运算

```python
from math import *
def f(x):
    return abs(cos(x))**0.5+sin(2+3*x)
# 1.包含显示循环的标准Python函数
def f1():
    res = []
    for x in range(10000):
        res.append(f(x))
    return res
# 2.包含隐式循环的迭代子方法（list推导）
def f2():
    return [f(x) for x in range(10000)]
# 3.包含隐式循环，使用eval的迭代子方法
def f3():
    ex = 'abs(cos(x))**0.5+sin(2+3*x)'
    return [eval(ex) for x in range(10000)]
# 4.NumPy向量化实现
def f4():
    x = np.range(10000)
    return np.abs(np.cos(x))**0.5+np.sin(2+3*x)
# 5.numexpr单线程实现
import numexpr as ne
def f5():
    ex = 'abs(cos(x))**0.5+sin(2+3*x)'
    ne.set_num_threads(1)
    return ne.evaluate(ex)
# 5.numexpr多线程实现
def f6():
    ex = 'abs(cos(x))**0.5+sin(2+3*x)'
    ne.set_num_threads(16)
    return ne.evaluate(ex)
# 计算速度：6
```

### multiprocessing：并行计算

```python
import multiprocessing as mp
pool = mp.Pool(processes = w)
result = pool.map(function,paralist)
```

### Numba：动态编译

```python
import numba as nb
f_np = nb.jit(f_py)
result = f_np(params)
```

Numba的优势

> 原始函数不需要修改，直接调用 jit 函数即可
>
> 执行速度显著提高，不仅对于纯 Python 相比是如此，对于向量化的 Numpy 实现也是如此
>
> 不需要初始化大型数组对象

### Cython：合并Python和C语言静态编译

传送门：https://www.jianshu.com/p/5d078a4de156

## 如何获取Alpha

### 金融工程模型分类

期货、债券

> CTA趋势
>
> Mean Reversion
>
> 统计套利
>
> 事件驱动
>
> 日内波段

期货策略

> 市场中性 Delta neutral
>
> I.V.strategy
>
> 3V matrix
>
> +Gamma + Theta

股票、ETF

> Alpha
>
> 股票对冲
>
> 期现套利

### 股票型Alpha策略基本逻辑

投资组合

> 一部分是精选A股市场最好的股票，构建现货投资组合；另一部分是做空股指期货，利用股指期货低成本、高杠杆的特性，对冲系统风险。以$\beta$对冲为主要对冲方式，也可市值对冲。

策略收益

> 提供股指期货$\alpha$对冲交易机会，构建股票和股指期货对冲组合

适合投资者

> 该策略为高风险高收益率投资策略，适合高风险偏好、中等资金规模的投资者

读图：![alpha收益特点](C:\Users\Administrator\Desktop\alpha收益特点.png)

做空IF、做多股票。IF 和 HS300 平水交割。升水是对此策略有利。

牛市初期，微涨。在对冲，收益很高来自价差。可以赚点升水钱。

中期，IF大幅升水，有浮亏。因为是做空IF，赚不到上涨带来的收益。此时收益会回撤。考验alpha风控能力。

在熊市，收益有波动，但是基本是持平的。熊市初期，下跌时放空（做空IF）赚钱是违规的。

升贴水

> 升水：IF > HS300
>
> 贴水：IF < HS300
>
> 熊市长期处于贴水状态。

### 商品期货策略

基础知识

> 品种：大宗商品（棉花、大豆）、金融资产（股票、债券）。用作标的
>
> 交易所：上期所/上期能源、郑商所、大商所、中金所
>
> 板块：农产品、能源化工、黑色、基本金属、重金属
>
> 交易规则：保证金交易、交割、涨跌停、主力合约、报价与行情数据特点

商品套利（配对）交易策略原来

> 利用基本面分析和量化方法寻找同一种产业链或板块中商品品种间价格波动相关规律，通过做多一个品种同时，做空另外一个配对品种的交易，获得相对稳定的价差波动收益
>
> 策略一半选择品种间联动性较强的板块，如黑色、化工、基本金属和油粕板块，精选板块中多个品种作为样本池

跨品种套利

> RB螺纹钢、HC热卷相关性很大
>
> 做多价差。当螺纹钢先下跌后，做多螺纹钢，做空热卷。当热卷也随之下跌后获利平仓（反向操作）。

跨期套利

> 不同到期日的合约价差在一个相对稳定的区间。一旦价差出现大的波动就可以进场开仓，等待价差回归后平仓止盈。

产品特性跨期

> 橡胶的一月和九月合约的价差在过去的几年中一直存在单方向的套利机会。主要是由于每年新老橡胶的基本面差异导致。可以利用此规律做多价差。

### 多空策略

交易标的：单个品种、配对价差

基本逻辑：强者恒强，做价差的发散

HANS123策略逻辑

> 日内交易策略，趋势突破系统
>
> 开盘30分钟后准备入场
>
> 上轨：开盘30分钟内的高点
>
> 下轨：开盘30分钟内的低点
>
> 价格突破上轨，买入开仓。价格跌穿下轨，卖出平仓。
>
> 突破时如已有持仓，则先止损再反手。收盘前无条件平仓
>
> 最怕大幅波动

### 回归策略

交易标的：配对价差、同一标的不同表现形式

基本逻辑：均值回复，做价差的收敛

一二级市场套利

> 反映一级市场净值的IOPV：基金份额参考净值（IOPV）是指交易时间内，申购、赎回清单中组合证券（含预估现金部分）的实时市值，主要供投资者交易、申购、赎回基金份额时参考
>
> 反映二级市场的交易价格：行情软件中实时看到的最新成交价
>
> 套利空间：实时交易价格相对于IOPV产生了较大偏离，形成折价或者溢价
>
> 套利方法：折价（交易价格小于IOPV）：买入ETF（二级市场，低价），赎回ETF份额（一篮子等同ETF的股票，一级市场，得高价），卖出股票获利（在二级市场卖出赎回的股票）。溢价（交易价格高于IPOV）:买入股票（二级市场买入成分股），申购ETF份额（用买入的股票申购），卖出ETF份额获利（二级市场）
>
> 更多细节：现金替代&资金利用率、交易成本&量化误差

二级市场轮动

> 以沪深300为例，对应的ETF产品有若干只
>
> 每个产品的交易价格与IOPV之间的折溢价可能有很大差别：流动性、资金利用率、交易习惯、考核方式
>
> 套利方式：利用各ETF的折溢价差，买入折价高的，同时卖出溢价高的。

期限套利

> 根据沪深300股指期货与沪深300指数基差到期时必定收敛的特性，当期货指数与沪深300指数基差足够大时，可以通过构建一个反向组合获得基差收敛过程中产生的收益
>
> 利用：局部交易时的投机行为的贪婪与恐惧

对冲工具的使用

> 股指期货
>
> ETF期权
>
> 股指期权