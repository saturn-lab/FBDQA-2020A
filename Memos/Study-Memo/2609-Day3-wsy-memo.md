# 第三次课总结

## 知识普及

#### 多因子模型

- 美股因子分析：市场，规模，价值，动量，风险，质量

  - 市值：股本*股票价

  - 价值：账面价值比Book-to-market Ratio

    越高表示越被低估（并不一定，只是相对来说可以这样判断）

  - 高动量：市场上过去12月总回报高

  - 低波动：市场是相对于大盘的beta低（0<beta<1，beta<0的话则是逆着市场变动）

  - 高质量：利润率高

  美股因子回报测试：高价值-EW年化回报最大

  每种因子都有周期性，不可能短时间内跑赢大盘，选择哪个因子要与投资人的风险承受能力匹配。在可靠的投资框架内坚持自己的投资理念，与认知缺陷抗衡，才可能在较长的投资期限跑赢大盘

  - VW和EW：两种加权方式

    VW：购买等市值

    EW：市值加权，市值高的买的多

    EW的年化回报高，说明小市值跑赢了大市值

- A股市场

- 历史回测方式：做多指标高的，做空指标低的，——为了对冲市场整体的波动

  即一维零投资组合检验，一维即单因子，零和即当期现金流为0

  <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.41.47.png" style="zoom:50%;" />

- 因子市场：要适应市场特点和投资者行为风格（清楚投资者结构和主要投资者的特点）

- 量化投资策略的多因子框架

  <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.44.14.png" style="zoom:50%;" />

  补充：

  规模+价值，可以规避小公司中的烂公司

  价值投资很难规避价值陷阱（深套），为了规避可以尝试价值+动量组合，找已经开始反弹的股票

- 利用行为金融学解释多因子

  - 小市值：前景理论
  - 高价值：反应过激和风险厌恶
  - 高动量：反应不足和注意力偏差

#### 趋势跟随模型——海龟交易

- 趋势跟随策略：

  - 发现趋势苗头（在启动阶段）——对应高动量因子
  - 顺着趋势方向下注
  - 遵循“截断亏损，让利润奔跑”的哲学

  如果趋势延续，就持有头寸，直到趋势完结；（判断掉头的时机）

  如果一上来就错了及时认错止损

- 交易策略要点

  - 市场：买卖什么——海龟选择高流动性的市场
  - 头寸规模
  - 入市：何时买卖
  - 止损：何时放弃亏损头寸
  - 退出：何时退出盈利头寸
  - 战术：怎么买卖

- 头寸规模

  头寸规模**单位** = 账户的1% / (N*每一点数所代表的美元)

  - 每一点数所代表的美元为每一最小交易单位的资金（1手股票）

  - 波动性N：$N = (19 \times PDN + TR) / 20$

  - PDN：前一天的N值

  - TR：当日的真实波动幅度

    $= \max \{H-L,H-PDC,PDC-L\}$

    H = 当日最高价，L = 当日最低价，PDC = 前一天收盘价

- 头寸规模的进一步限制

  | 层面 | 限制范围            | 头寸单位上限 |
  | ---- | ------------------- | ------------ |
  | 1    | 单个市场            | 4            |
  | 2    | 高度关联的多个市场  | 6            |
  | 3    | 松散关联的多个市场  | 10           |
  | 4    | 单个方向（多/空头） | 12           |

- 入市信号

  - 系统1：20日突破为基础的短期系统

    如果上次突破为盈利性突破，则忽略当期入市信号：可能已经到尾声了，之前在同样级别的信号已经赚到钱了

    55日突破点保障性信号：相较于20日，55日是更高的级别

  - 系统2：55日突破为基础的长期系统

  何为突破？

- 建仓：在突破点建立1个单位的头寸，按N/2的价格间隔逐步扩大头寸，直到达到规模上限

- 止损：任何一笔交易的风险程度不超过账户的2%

  价格变动的上限是2N，对于加仓情况，止损点上浮

- 退出：系统1：10日反向突破退出；系统2：20日反向突破退出

- 对复杂情况的应对

- K线图

  高开低收（矩形开盘、收盘），收盘高于开盘（空心），收盘低于开盘（实心）

  最底下是量

  前复权：（一般看图用这种）

  后复权：以上市第一天的价格为基准

####评估策略的指标

- 夏普比率：$Sharpe Ratio = \frac{E(R_p)-R_f}{\sigma_P}$

  每承受一单位总风险，会产生多少超额报酬

- 最大回撤：在选定周期内任一历史时点往后退，产品净值走到最低点时的收益率回撤幅度的最大值

  减少回撤，回撤幅度及回撤时间

- 其他值得关注的：交易次数，信息率，年化收益，日均仓位，alpha，beta

## 工具应用-Python

### 包的介绍和应用

- Numpy

  `import numpy as ny`

  - 创建数组

    `np.array()`

    `np.arange(4)` `np.arange(4,8,1)`，从4开始，到8前一位截止，距离为1  `np.ones((3,3))` `np.arange(0.9).reshape(3,3)`

    `a=np.random.random(12)`

    `np.pi` 即 $\pi$

  - Element-wise operation

    `a+b` `a*b`   `A*B`(A、B为矩阵，对应位置的元素相乘)

    `a +=4` `a *=4`

    `np.sin(a)` `np.sqrt(b)`

  - 矩阵操作

    `np.dot(A,B)` (点乘) 

    `A.transpose()`(转置)

    `A.shape=(3,4)` `A.shape=(12)`(对A的操作)

    `A.ravel()`(恢复成单行向量)

    `a=A.reshape(3,4)`(对a的操作，对A无影响)

  - 其他

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午4.05.11.png" alt="1" style="zoom:60%;" />

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午4.05.22.png" alt="2" style="zoom:50%;" />

- Scipy

  <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午4.05.30.png" alt="3" style="zoom:50%;" />

- Matplotlib

  `import matplotlib.pyplot as plt`

  - Scatter plot

    `plt.scatter(x,y,color='r')` x为横坐标，y为纵坐标

    `plt.show()`

  - 线图

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午9.01.35.png" style="zoom:50%;" />

  - 虚线和图标

    `ax.plot(x,y,dashes=[2,2,10,2],label='Using set_dashes')` 两点连线两点断，十点连线两点断

    `ax.plot(x,y-0.2,dashes=[6,2],label='Using the dashes parameter')`

    `ax.legend`

  - 绘制子图

    `plt.subplot(2,1,1)` 第一个数是长，第二个数是宽，第三个数是位置（最上面的子图）

    `plt.plot(x,y1)`

    `plt.title('plot_1')`

    `plt.subplot(2,1,2)` 

    `plt.plot(x,y2)`

    `plt.title('plot_2')`

- Pandas

  `import pandas as pd`

  - Series 一维数据，同类

    `pd.Series(data,index=index)` index是一维坐标轴的索引列表，如果不写index则为[0,1, ...]

    

  - DataFrame 二维数据，每列类型可以不同

    > 从Series构造：第一列命名为one，第二列命名为two

    `d={'one' : pd.Series([1.,2.,3.],index=['a','b','c'])`

    `    'two' : pd.Series([1.,2.,3.,4.],index=['a','b','c','d'])}`

    `df = pd.DataFrame(d)`

    `df`

    `df.index` 横坐标

    `df.colomns` 纵坐标

    > 查找

    `pd.DataFrame(d,index=['a','b'],columns=['one'])`

    `df['one']`

    > 列操作

    新建列

    值：`df['three']=df['one']*df['two']`

    判断：`df['flag']=df['one']>2`

  - Panel 3D

- Seaborn

  相比于matlablib更简洁，但matlablit更灵活

  参考：http://seaborn.pydata.org/api.html 

  `import seaborn as sns`

  `tips = sns.load_dataset("tips")`

  `names = sns.get_dataset_names()` ?

  - 三种类型

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午9.54.57.png" style="zoom:50%;" />

  **displot**

  - 直方图

    `sns.histplot(tips,x="total_bill")`

    `sns.histplot(tips,x="total_bill",hue="sex")` 累积

    `sns.histplot(tips,x="total_bill",hue="sex",col="sex")` 分开

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午10.51.02.png" style="zoom:50%;" />

  - kdeplot

    `sns.kdeplot(data=tips,x="total_bill",hue='sex')` 纵轴为density

    `sns.displot(data=tips,x="total_bill",ked=True)`同时绘制直方图和概率密度图

  - ecdf

    `sns.ecdfplot(tips,x="total_bill",hue='sex')` cdf

    `sns.kdeplot(data=tips,x="total_bill",hue='sex',kind="ecdf")`

  - 多变量

    `sns.displot(tips,x="total_bill",y="tip",hue='sex')`

    `sns.displot(tips,x="total_bill",y="tip",kind="kde")` 等高线？

  **replot**

  - scatterplot

    `sns.scatterplot(x="total_bill",y="tip",data=tips)`

    `sns.replot(x="total_bill",y="tip",data=tips,hue="smoker",style="smkoer")` 分类，style为形状区分，hue是颜色分类

    `sns.replot(x="total_bill",y="tip",data=tips,hue="sex",col='smoker')` 图按类别分列

  - lineplot

    `sns.replot(x="total_bill",y="tip",data=tips,hue="smoker",style="smoker",kind="line")`

  - Jointplot, pairplot

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.07.03.png" style="zoom:50%;" />

  **catplot**

  - scatter

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.10.17.png" style="zoom:50%;" />

  -  箱线图

    `sns.catplot(x="sex",y="survived",hue="class",kind="box",data=titanic)` 

    `sns.catplot(x="sex",y="survived",kind="box",data=titanic)` 

  - violin?

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.13.51.png" style="zoom:50%;" />

  - Statistic

    1. 

    `sns.catplot(x="sex",y="survived",hue="class",kind="bar",data=titanic)` 

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.15.37.png" style="zoom:50%;" />

    ?

    2. 

    `sns.catplot(x="sex",y="survived",kind="class",data=titanic)`

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.17.19.png" style="zoom:50%;" />

  **回归分析**

  `sns.regplot(x="total_bill",y="tip",data=tips)`

  `sns.lmplot(x="x",y="y",data=anscombe.query("dataset == 'II'"),order=2)` 二阶回归

  `sns.lmplot(x="x",y="y",data=anscombe.query("dataset == 'III'"),ci=None)`

  `sns.lmplot(x="x",y="y",data=anscombe.query("dataset == 'III'"),ci=None,robust=TRUE)` 设置robust = True可以忽略特异点

  ci?

  - 通过设置kind参数在其他图形级绘图函数中做回归分析

    `sns.jointplot(x="total_bill",y="tip",date=tips,kind="reg")`

    <img src="/Users/grace/Desktop/屏幕快照 2020-10-01 下午11.25.20.png" style="zoom:50%;" />

    