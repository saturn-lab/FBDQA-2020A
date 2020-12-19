###  课堂小结 周航宇 2017010583
### 衍生品估值库——期权估值应用
+ 资产定价基本定理
+ + 鞅测度
在鞅测度下，所有风险因素随无风险短期利率漂移——而不随包含某种无风险短期利率之上风险溢价的任何其他市场利率漂移。
+ 现实世界的概率测度和风险中性的概率测度
+ 三个陈述等价
1.市场模型中没有套利机会（唯一价格）
2.鞅测度（风险中性测度）集合不为空
3.一致线性定价系统集合不为空
+ 衍生品分析库
+ + 风险中立折现
~~~python
from pylab import plt
plt.style.use('seaborn')
import matplotlib as mpl
mpl.rcParams['font.family'] = 'serif’

import numpy as np
import pandas as pd
import datetime as dt
import sys
sys.path.append('../python36/dxa')
#建立衍生品分析库

from dx_frame import *


#Risk-Neutral Discounting
dates = [dt.datetime(2015, 1, 1), dt.datetime(2015, 7, 1), dt.datetime(2016, 1, 1)]
deltas = [0.0, 0.5, 1.0]
csr = constant_short_rate('csr', 0.05)
#短期无风险利率固定为5%
csr.get_discount_factors(dates)
#获取折现因子
array([[datetime.datetime(2015, 1, 1, 0, 0), 0.951229424500714],
       [datetime.datetime(2015, 7, 1, 0, 0), 0.9755103387657228],
       [datetime.datetime(2016, 1, 1, 0, 0), 1.0]], dtype=object)

deltas = get_year_deltas(dates)
deltas
array([0.        , 0.49589041, 1.        ])
csr.get_discount_factors(deltas, dtobjects=False)

#Market Environment

me_gbm = market_environment('me_gbm', dt.datetime(2015, 1, 1))

me_gbm.add_constant('initial_value', 36.)
me_gbm.add_constant('volatility', 0.2)
me_gbm.add_constant('final_date', dt.datetime(2015, 12, 31))
me_gbm.add_constant('currency', 'EUR')
me_gbm.add_constant('frequency', 'M')
me_gbm.add_constant('paths', 10000)
#初始值设置
me_gbm.add_curve('discount_curve', csr)


~~~
#### 衍生品分析库中的三大基本模型
+ BS模型
$dS_t=rS_tdt+\sigma S_tdZ_t$
~~~python
#Geometric Brownian Motion

from dx_frame import *
me_gbm = market_environment('me_gbm', dt.datetime(2015, 1, 1))

#市场环境设置
me_gbm.add_constant('initial_value', 36.)
me_gbm.add_constant('volatility', 0.2)
me_gbm.add_constant('final_date', dt.datetime(2015, 12, 31))
me_gbm.add_constant('currency', 'EUR')
me_gbm.add_constant('frequency', 'M')
 
# monthly frequency (respcective month end)

me_gbm.add_constant('paths', 10000)
csr = constant_short_rate('csr', 0.06)
me_gbm.add_curve('discount_curve', csr)
#初始值设置
~~~
+ 几何布朗运动
~~~python
from geometric_brownian_motion import geometric_brownian_motion
gbm = geometric_brownian_motion('gbm', me_gbm)
gbm.generate_time_grid()
gbm.time_grid

array([datetime.datetime(2015, 1, 1, 0, 0),
       datetime.datetime(2015, 1, 31, 0, 0),
       datetime.datetime(2015, 2, 28, 0, 0),
       datetime.datetime(2015, 3, 31, 0, 0),
       datetime.datetime(2015, 4, 30, 0, 0),
       datetime.datetime(2015, 5, 31, 0, 0),
       datetime.datetime(2015, 6, 30, 0, 0),
       datetime.datetime(2015, 7, 31, 0, 0),
       datetime.datetime(2015, 8, 31, 0, 0),
       datetime.datetime(2015, 9, 30, 0, 0),
       datetime.datetime(2015, 10, 31, 0, 0),
       datetime.datetime(2015, 11, 30, 0, 0),
       datetime.datetime(2015, 12, 31, 0, 0)], dtype=object)
       
       
#Geometric Brownian Motion

%time paths_1 = gbm.get_instrument_values()
#paths_1 volatility = 0.2

gbm.update(volatility=0.5)
%time paths_2 = gbm.get_instrument_values()
import matplotlib.pyplot as plt
%matplotlib inline
plt.figure(figsize=(10, 6))
p1 = plt.plot(gbm.time_grid, paths_1[:, :10], 'b')
p2 = plt.plot(gbm.time_grid, paths_2[:, :10], 'r-.')
plt.grid(True)
l1 = plt.legend([p1[0], p2[0]],
                ['low volatility', 'high volatility'], loc=2)
plt.gca().add_artist(l1)
plt.xticks(rotation=30);
#画出高低波动率的几何布朗运动的图

~~~
+ 跳跃扩散
$dS_t=(r-r_J)S_tdt+\sigma S_tdZ_t+J_tS_tdZN_t$
~~~python
#Jump Diffusion

me_jd = market_environment('me_jd', dt.datetime(2015, 1, 1))
me_jd.add_constant('lambda', 0.3)
#跳跃密度（概率）
me_jd.add_constant('mu', -0.75)
#预期跳跃规模
me_jd.add_constant('delta', 0.1)
#跳跃规模的标准差
me_jd.add_environment(me_gbm)
#添加GBM 模拟类的完整环境
from jump_diffusion import jump_diffusion
jd = jump_diffusion('jd', me_jd)
#导入跳跃扩散的库，设置基本参数


#Jump Diffusion

%time paths_3 = jd.get_instrument_values()
jd.update(lamb=0.9)
#改变跳跃概率
%time paths_4 = jd.get_instrument_values()
plt.figure(figsize=(10, 6))
p1 = plt.plot(gbm.time_grid, paths_3[:, :10], 'b')
p2 = plt.plot(gbm.time_grid, paths_4[:, :10], 'r-.')
plt.grid(True)
l1 = plt.legend([p1[0], p2[0]],
                ['low intensity', 'high intensity'], loc=3)
plt.gca().add_artist(l1)
plt.xticks(rotation=30);
#改变参数，画出跳跃扩散的图

~~~
+ 平方根扩散
$dx_t=k(\theta-x_t)dt+\sigma\sqrt{x_t}dZ_t$
~~~python
#Square-Root Diffusion

me_srd = market_environment('me_srd', dt.datetime(2015, 1, 1))
me_srd.add_constant('initial_value', .25)
me_srd.add_constant('volatility', 0.05)
me_srd.add_constant('final_date', dt.datetime(2015, 12, 31))
me_srd.add_constant('currency', 'EUR')
me_srd.add_constant('frequency', 'W')
me_srd.add_constant('paths', 10000)

me_srd.add_constant('kappa', 4.0)
#设置均值回归因子
me_srd.add_constant('theta', 0.2)
#设置过程长期均值
me_srd.add_curve('discount_curve', constant_short_rate('r', 0.0))
from square_root_diffusion import square_root_diffusion
srd = square_root_diffusion('srd', me_srd)
srd_paths = srd.get_instrument_values()[:, :10]
#导入单位根扩散的库，设置基本参数



#Square-Root Diffusion

plt.figure(figsize=(10, 6))
plt.plot(srd.time_grid, srd.get_instrument_values()[:, :10])
plt.axhline(me_srd.get_constant('theta'), color='r', ls='--', lw=2.0)
plt.grid(True)
plt.xticks(rotation=30);
#画出单位根扩散的图

~~~

#### 衍生品分析库在期权估值方面的应用
+ 欧式期权
~~~python
#European Options

from dx_simulation import *
me_gbm = market_environment('me_gbm', dt.datetime(2015, 1, 1))
me_gbm.add_constant('initial_value', 36.)
#设置初始值36
me_gbm.add_constant('volatility', 0.2)
me_gbm.add_constant('final_date', dt.datetime(2015, 12, 31))
me_gbm.add_constant('currency', 'EUR')
me_gbm.add_constant('frequency', 'M')
me_gbm.add_constant('paths', 10000)
csr = constant_short_rate('csr', 0.06)
me_gbm.add_curve('discount_curve', csr)
gbm = geometric_brownian_motion('gbm', me_gbm)

#配置市场环境



#European Options

me_call = market_environment('me_call', me_gbm.pricing_date)
me_call.add_constant('strike', 40.)
#设置行权价
me_call.add_constant('maturity', dt.datetime(2015, 12, 31))
#设置到期日
me_call.add_constant('currency', 'EUR’)
payoff_func = ‘np.maximum(maturity_value - strike, 0)’  
#内在价值
from valuation_mcs_european import valuation_mcs_european
eur_call = valuation_mcs_european('eur_call', underlying=gbm,
                        mar_env=me_call, payoff_func=payoff_func)
%time eur_call.present_value()
2.140776
%time eur_call.delta()
0.5148
%time eur_call.vega()
14.2782
#计算期权价值


#European Options

%%time
s_list = np.arange(34., 46.1, 2.)
p_list = []; d_list = []; v_list = []
for s in s_list:
    eur_call.update(initial_value=s)
    p_list.append(eur_call.present_value(fixed_seed=True))
    d_list.append(eur_call.delta())
    v_list.append(eur_call.vega())
from plot_option_stats import plot_option_stats
%matplotlib inline
plot_option_stats(s_list, p_list, d_list, v_list)

#底层标的的初试价格不同时，期权价值的变化
~~~

+ 美式期权
~~~python
#American Options

from dx_simulation import *
me_gbm = market_environment('me_gbm', dt.datetime(2015, 1, 1))
me_gbm.add_constant('initial_value', 36.)
#设置初始价值为36
me_gbm.add_constant('volatility', 0.2)
me_gbm.add_constant('final_date', dt.datetime(2015, 12, 31))
me_gbm.add_constant('currency', 'EUR')
me_gbm.add_constant('frequency', ‘W')
me_gbm.add_constant('paths’, 50000)
csr = constant_short_rate('csr', 0.06)
me_gbm.add_curve('discount_curve', csr)
gbm = geometric_brownian_motion('gbm', me_gbm)

#配置市场环境


#American Options

payoff_func = 'np.maximum(strike - instrument_values, 0)’
me_am_put = market_environment('me_am_put', dt.datetime(2015, 1, 1))
me_am_put.add_constant('maturity', dt.datetime(2015, 12, 31))
me_am_put.add_constant('strike', 40.)
me_am_put.add_constant('currency', 'EUR’)
from valuation_mcs_american import valuation_mcs_American
am_put = valuation_mcs_american('am_put', underlying=gbm,
                    mar_env=me_am_put, payoff_func=payoff_func)

#标的资产仍然是根据GBM模型模拟的股票
%time am_put.present_value(fixed_seed=True, bf=5)

#构建看跌美式期权



#American Options

%%time
ls_table = []
for initial_value in (36., 38., 40., 42., 44.): 
    for volatility in (0.2, 0.4):
        for maturity in (dt.datetime(2015, 12, 31),
                         dt.datetime(2016, 12, 31)):
            am_put.update(initial_value=initial_value,
                          volatility=volatility,
                          maturity=maturity)
            ls_table.append([initial_value,
                             volatility,
                             maturity,
                             am_put.present_value(bf=5)])
#底层标的的不同的初始价格


#American Options

print("S0  | Vola | T | Value")
print(22 * "-")
for r in ls_table:
    print("%d  | %3.1f  | %d | %5.3f" % 
          (r[0], r[1], r[2].year - 2014, r[3]))

#计算看跌美式期权价值
am_put.update(initial_value=36.)
am_put.delta()
am_put.vega()
~~~

+ 投资组合
~~~python
#Portfolios

#这是欧式看涨期权和美式看跌期权的投资组合
portfolio.get_statistics(fixed_seed=False)
portfolio.get_statistics(fixed_seed=False)[['pos_value', 'pos_delta', 'pos_vega']].sum()
  # aggregate over all positions
pos_value    27.489253
pos_delta     1.271000
pos_vega     73.308100


#Portfolios

plt.figure(figsize=(10, 6))
plt.hist([pv1, pv2], bins=25,
         label=['European call', 'American put']);
plt.axvline(pv1.mean(), color='r', ls='dashed',
            lw=1.5, label='call mean = %4.2f' % pv1.mean())
plt.axvline(pv2.mean(), color='r', ls='dotted',
            lw=1.5, label='put mean = %4.2f' % pv2.mean())
plt.xlim(0, 80); plt.ylim(0, 10000)
plt.legend();

#期权投资组合的各自仓位价值


#Portfolios

pvs = pv1 + pv2
plt.figure(figsize=(10, 6))
plt.hist(pvs, bins=50, label='portfolio');
plt.axvline(pvs.mean(), color='r', ls='dashed',
            lw=1.5, label='mean = %4.2f' % pvs.mean())
plt.xlim(0, 80); plt.ylim(0, 7000)
plt.legend();

#期权投资组合的总价值

~~~


### 人工智能驱动下的金融创新实践

#### 何为人工智能
+ 弱人工智能和强人工智能
#### 人工智能的边界
+ 优势
+ + 大数据：loT产生的图片、语音、文本、活动数据等
+ + 高算例：CPU、GPU、TPU
+ + 强算法：数据多了，算力便宜了，才能支持更强的算法
+ 人工智能与人类智能
#### 人工智能与交易
+ 第一原理思考
平稳随机过程是在固定时间和位置的概率分布与所有时间和位置的概率分布相同的随机过程，即随机过程的统计特性不随时间的推移而变化，因此数学期望和方差这些参数不随时间和位置变化。
#### 务实的战略
+ 解决标准化自动化问题、解决认知宽度和效率问题、人工+智能
+ 拟合指数
+ 交易细节处理
+ 高频：做市、套利
+ + Market Making
持仓：ms~s~min
定价模型相对简单
报单执行系统复杂
策略环境超低延迟
一般不持隔夜仓
+ + Arbitrage
直接套利 Direct Arbitrage：持仓：ms~s~min~h~day；速度游戏；定价模型相对简单
统计套利Statistical Arbitrage：持仓：min~hour~day；定价模型相对复杂
+ + 高频交易经典模型
1.线性模型
AR、MA、ARMA
Cointegration
2.波动率模型
3.非线性模型
双线性模型、非参量型模型、神经网络模型

