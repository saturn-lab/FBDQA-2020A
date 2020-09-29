import numpy as np
c=np.array([[1,2,3],[4,5,6]])
c
import matplotlib.pyplot as plt
classA_grade=[40,20,50,70,10]
grades_range=[10,20,40,60,100]
plt.scatter(grades_range,classA_grade,color='b')
plt.show()
import matplotlib.pyplot as plt
import numpy as np
t=np.arange(0.0,2.0,0.01)
s=1+np.cos(2*np.pi*t)
fig,ax=plt.subplots()
ax.plot(t,s)
ax.set(xlabel='time(s)',ylabel='voltage(mV)')
ax.grid()
fig.savefig("test.png")
plt.show()
import seaborn as sns
tips=sns.load_dataset("tips")
tips
sns.relplot(data=tips,x="total_bill",y="tip",hue="sex",col="smoker")
sns.jointplot(data=tips, x="total_bill", y="tip",hue='sex')
sns.pairplot(data=tips,hue='sex')
类
	类名.变量名
	
Numpy array 可以接受数组/元组（tuples）/元组列表组合

矩阵相乘 np.dot(A,B)

pandas和numpy区别：pandas按行操作

Index_col=0 将第一列设置为index值

趋势跟随 追涨杀跌
均值回复 高抛低吸

多因子模型
市场 规模 价值（BtoM） 动量 风险 质量
EW>VW  因为长期看小市值股票收益更高

同时构造两个 一个大市值一个小市值 做多大市值 做空小市值 对冲市场整体的波动 限制因子本身的作用

美股 价值因子
A股 市值因子 小市值 炒小抄烂
	反转因子
	
因子的作用如何要看市场特点
投资者结构 主要投资者的市场行为

一维零投资组合检验

规模+价值   避免踩到小的烂公司 买有前景的小（有潜力）公司
价值+动量   被低估的股票中短期已经开始出现反弹的 避免长期被套
价值+质量   价格便宜/公允+公司竞争优势

以上因子都是从历史数据出总结出的 未来会怎样不一定 要找基本逻辑（找不理性行为）

海龟交易

监管层期待慢牛，但A股散户为主，只有疯牛

趋势 高动量因子 本身没有方向
试图跟随趋势时如果错了要即使认错止损
掉头多少认为趋势已经被破坏了/结束了
试图用策略保证选择合适的要点
	市场
	头寸规模 那个公式 波动性N 头寸单位规模
	入市 突破20日or突破55日
	逐步减仓 N/2
	止损 从加仓的位置下跌2N
	退出 10日反向突破（10日新低）or20日反向突破  弊端是利润的回吐
	
看图时习惯用前复权

Sharpe ratio 1块风险带来的超额回报

我们希望减少回撤的幅度和时间

如何修饰
