### 课程小结4 周航宇 2017010583
### 金融基础知识
##### 金融学
+ 狭义：资金融通
+ 广义：跨期配置稀缺资源
#####  分类
+ 公司金融：公司财务决策、融资行为、IPO
+ 资产定价：投资者的投资行为、资产收益率
+ 宏观金融、行为金融、金融科技等
##### 假设
+ 基本假设：理性人假说
+ 边界条件：资源稀缺性、制度费用
+ 重要概念：选择、机会成本、偏好、效用、信息、预测
+ 基本原理：收益与风险的权衡、边际效用递减
+ 四大理论假说：有效市场假说、均值方差组合、CAPM模型、期权定价BS公式
##### 金融市场
+ 定义：交易金融资产确定价格的一种机制
+ 功能：资源配置、风险再分配、宏观经济调节
+ 分类：
+ + 直接融资、间接融资
+ + 一级、二级
+ + 股票、债权、衍生品
+ 参与者：银行、券商、保险、基金、信托、私募
+ 监管机构：央行、证监会、银保监会
##### 金融资产
现金、股票、债权、期货、齐全、基金、外汇、房地产，也称为投资标的
流动性：现今>债券>基金>股票>房地产（流动性减少，风险递增）
##### 交易制度
+ T+1
+ 涨跌停
+ 卖空限制
+ 交易成本
+ 竞价原则：价格优先、时间优先
+ 竞价方式：集合竞价、连续竞价
+ 交易所：上海、深圳
+ 股票价格指数：上证综指、沪深300
##### 资产价格
$P=\sum_{t=1}^{n}\frac{E(CF_t)}{(1+r)^t}$
不同资产、不同时期的折现率r不一样。
##### 资产收益率的影响因素
+ 债权收益率：信用和久期
+ 股票收益率=无风险收益率+风险溢价
+ CAPM：
$E(R_t)-R_f=\beta \times [E(RM_t)-R_f]$
$E(R_t)=\alpha+\beta\times[E(RM_t)]$
+ Fama-French三因子
+ Carhat四因子
+ Fama-French五因子
##### 投资组合理论
有效边界
##### 资产选择
##### 风险分析
+ 总风险=股票月度收益率的标准差
+ 系统性风险=回归预测值的标准差
+ 公司风险=残差部分的标准差
+ $总风险^2=系统性风险^2+公司风险^2$
推荐书：革命新金融思想：费希尔布莱克

### JoinQuant
##### 本地
~~~python
from jqdatasdk import *
auth('username','passwd')
is_auth = is_auth()
print(is_auth)
~~~
~~~python
df=get_price('000001.XSHG')
df
~~~
~~~python
q=query(valuation).filter(valuation.code=='000001.XSHE')	
df=get_fundamentals(q),'2015-10-15'
df
~~~
~~~python
df=get_price('000001.XSHE',start_date='2020-09-01',end_date='2020-09-30',frequency='daily',fields=['close'])
Rt=df.pct_change().dropna()
Rt
~~~
##### 在线
+ 初始化函数
~~~python
# 初始化函数，设定基准
def initialize(context):
	set_benchmark('000300.XSHG')
	set_option('use_real_price',True)
	set_slippage(FixedSlippage(0))
	set_order_cost(...)
	#other user functions
~~~
+ 股票池选择
~~~python
def pl_stock_pool(context):
	pl_raw_data=pl_load_fundamentals_data(context)
	pl_raw_data_array=[]
	pl_current_datas=get_current_data()
	for pl_item in pl_raw_data:
		pl_code=pl_item['code']
		# codes that filter the stocks
		pl_raw_data_array.append(pl_item)
	pl_raw_data=pl_raw_data_array
	pl_filtered_pe=[]
	for pl_stock in pl_raw_data:
		if pl_stock['pe_ratio']==None: continue
		if math.isnan(pl_stock['pe_ratio]) or float(pl_stock['pe_ratio']) < 10 or float(pl_stock['pe_ratio'])>30:
			continue
		pl_filtered_pe.append(pl_stock['code'])
		log.info(pl_stock['code'],pl_stock['pe_ratio'])
	
	g.pl_stock_pool = []
    for pl_stock in pl_filtered_pe:
        g.pl_stock_pool.append(pl_stock)
    log.info('调整股票池,筛选出的股票池：',g.pl_stock_pool)
    pass
~~~

### 量化交易策略开发案例
&emsp;交易逻辑vs策略实现
&emsp;细节
##### 程序框架
+ 启动
~~~python 
Initialize()
~~~
+ 开盘前
~~~python
run_daily(pl_before_market_open,time='before_open')
~~~
+ 盘中 
~~~python
run_daily(pl_trade,time='every_bar')
~~~
+ 收盘后
~~~python
run_daily(pl_after_market_close,time='after_close')
~~~
##### 交易逻辑的时间级别
&emsp;在每个单位时间内只执行一次
##### 股票池
&emsp;股票池+择时
&emsp;选股条件、再平衡、容量
e.g.选股条件——PE：0～30；市值：10亿～100亿 容量——50  再平衡周期——10个交易日
##### 股票池策略
股票池
选股条件——PE：10～30 容量——不限 再平衡周期——20个交易日
交易时机：再平衡时卖出原股票池中的股票，买入新股票池中的股票三
##### 如何选择交易时间
上涨、下跌、金叉死叉
+ 均线型：MA、EXPMA
+ 趋势型：MACD、SAR、ASI、DMI
+ 摆动型：KDJ、RSI、CCI、WR、BOLL
+ 能量型：OBV、VOL、VR
##### 简单择时策略
+ 单只股票：贵州茅台
+ 买入：5日均线上穿30日均线
+ 卖出：5日均线下穿30日均线
+ 金叉：短时均线上穿长时均线
+ 死叉：短时均线下穿长时均线






