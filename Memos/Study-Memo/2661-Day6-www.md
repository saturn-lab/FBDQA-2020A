2020.10.30
## 上节课报告的总结
- 应该对交易记录进行分析：e.g. 可能收益只来自于某几笔交易，或者是程序的问题
- 交易型策略：可以有日回撤，但是每个月结算报账的时候没有回撤。尽管年化收益不高。←无法靠选股做成，因为无法保证不回撤

## 股票型Alpha策略
- 做多股票组合+做空股指期货 = Alpha
- IF：沪深300的股指期货：指数*300 = 一手的名义本金，但是保证金交易带杠杆，保证金率为10% → 花10+w即可做多/做空IF；e.g. 10+w在3700买，到3800卖，则相当于10+w收益3w; 贴水：IF价格显著低于指数价格；期货交割价是最后时间段内股指的均价，如果长期处于贴水的状态，交割价高于做空时short的价格，是亏损的，会腐蚀alpha的收益。
- 做空（Short sale），是一个投资术语，是金融资产的一种操作模式。与做多相对，做空是先借入标的资产，然后卖出获得现金，过一段时间之后，再支出现金买入标的资产归还。
- 信息率：alpha/omega(残差风险)： if < 0.5  不要买； > 1: 对每单位风险可以有1单位的超额收益，应该买入


## 常见技术指标
- 技术指标不是很可靠233，除非了解了背后的物理含义，能够和当前的目标结合去使用
- 也可以把大家都用的技术指标反向使用
- 本质上都是对交易量、价格序列的滤波器，生成的结果怎么利用才是重要的，构造方式不管多复杂都随便
- e.g. MACD：diff = 短时均线EMA - 长时均线EMA；如果上涨，前者比后者变大速度快，diff>0;  DEA = diff的EMA，反应比diff慢；如果DEA被diff上穿，则是止跌上涨信号（金叉）; MACD = 2 * (dif - DEA): *2：因为软件画图的时候*2看着舒服
- e.g. KD: 给出当前价格位置处于过去n天价格区间的什么位置。==100：当前是最高价；0==现在是跌倒了最低点。
- 技术指标一般都做两根线，一根快线，一根慢线；通过相对值的变化来判断走势。
- 用途：预警（不要继续加仓）/确认（确认之前的买入卖出动作是正确与否，要不要止损）/预测（未来涨跌概率 & 空间多大）
- 决策：取决于动量/反转观点
- 背离：有二次验证（突破，交叉，都是一个点作为信号），有两个参考点。（e.g. 价格创了新高，但是反应强弱的RSI指标没有创新高）→出现背离，后面大概率会下跌/上涨
-  及时性 vs 准确性（稳定性）：短均线、长均线在这两者里权衡取舍。

- 北向资金：通过沪股通、深股通可以在港股交易；北向资金指在港交所主动买沪深股票的资金；

- 主力：是指主要的力量，一般也指股票中的庄家。形容市场上或一只股票里有一个或多个操纵价格的人或机构，以引导市场或股价向某个方向运行。一般股票主力和股市庄家有很大的相似性