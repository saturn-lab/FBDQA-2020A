# 第二次课总结

## 1. 知识普及

- 量化交易：通过**系统性方法**和**程序化手段**，进行交易**模式发现**及交易**策略构造**，并借助**计算机系统**进行验证和执行的交易过程。

- 模型

  Alpha模型

  风险模型

  交易成本模型

- 5种典型投资

| 投资模式 | 价格-价值关系        | 时间尺度              | 方法                                                 |
| -------- | -------------------- | --------------------- | ---------------------------------------------------- |
| 价值投资 | 不定的，可以是确定的 | 月-年                 | 关注价值，寻找定价低于内在价值的投资对象             |
| 成长投资 | 不定的，可以是确定的 | 月-年                 | 关注增长，寻找价值增长速度快鱼价格增长速度的投资对象 |
| 指数投资 | 不能确定             | 月-年                 | 忽略价格-价值关系，而购买整个市场的一部分            |
| 技术投资 | 可能有联系，但不相关 | s, min, h, 数日，数周 | 关注价格趋势                                         |
| 组合投资 | 相互独立             | 数日到月、年          | 将风险偏好于价格-价值风险水平相匹配                  |

- 投资逻辑的一些参考指标：年化收益、最大回撤、夏普比率

- 稳定绩效

  - 股票投资是最佳的长期投资方式
  - 需要认识到风险和收益的平衡，盈亏是同源的；量化的本质是用程序守住你的运气
  - 系统性、程序化的手段有利于追求稳定的绩效

- 交易体系的关键要素

  - 胜率 percent profitable，盈亏时间的比例
  - 赔率 Odds/P&L：在最小单位进行交易时，相对于亏损而言，盈利水平的相对规模
  - 成本 Costs：每笔交易的成本
  - 频率 Frequency：获得交易机会的频率
  - 头寸 Position：一次交易多少个单位
  - 本金 Capital

- 做自我评估并清楚自己的风险偏好

- 理论普及

  **有效市场假说（EMH）**

  - 弱式有效市场假设
  - 半强式有效市场假设：基本面已经在市场价格中表现出来了，内部消息可能可以获得超额收益
  - 强式有效市场假设

  > Friedman：理性交易者会立即纠正由非理性交易者引发的市场扰动

  例子：当中国平安的股价因为部分非理性交易者的过分悲观估计而下跌时，理性交易者会低价买入，同时卖空替代性证券做套期保值，从而使股价恢复。

  > 质疑：即使资产定价发生较大错误，由于纠正定价错误的策略需要承担的风险和成本，使策略不在吸引人，错误定价依然存在

  **行为金融学**

  - 一些偏好

  > - 前景理论
  > - 模糊厌恶

  - 禀赋效应：一旦拥有则会高估其价值（损失厌恶）

  > 对避害考虑大于趋利

  - 跨期选择

  > 短视冲动 vs 长远理智

  - 心理账户：对每一块钱并非一视同仁，视不同来源去往何处采取不同态度

  - 启示

  > - 避免自己非理性
  > - 抓住别人非理性的机会
  > - 识别主力陷阱并回避它（主力指市场的复合力，由”聪明“的资金在某些特定阶段共同构成）
  >   - 先拉高到成本线附近，再突然打到亏损空间，信心遭到摧残，割掉？
  > - 平时顺大众，关键逆大众

  **套利**：严格意义上，指零成本、无风险利润的投资策略

  - 风险和成本：

  > - 基本面风险（fundamental risk）：替代性证券不完美
  > - 噪音交易者风险（Noise trader risk）
  > - 实施成本（implementation risk）：费用+选择成本

  - 非理性行为-信念

  > - 过度自信
  > - 乐观主义和wish thinking
  > - 代表性
  > - 保守主义
  > - 信念固执和确认偏误
  > - 锚定
  > - 易得性偏误

  **偏好和信念影响到投资决策**

  - 分散化不足
  - 过度交易
  - 买入和卖出决策

  **两种交易者**

  - 套利者-理性交易者
  - 噪音交易者-非理性交易者

  

- 针对**投资者行为中典型的有规律的非理性现象**制定策略

- 

## 2. 工具类学习

## Markdown学习

1. **粗体** `**粗体**`

2. *斜体*`*斜体*`

3. 基本数学公式总结

   查找链接：https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference

   1. 在行内展示公式，用`$...$`

      单列一行展示公式，用`$$...$$`

   2. 希腊字母

      大写`\Delta`，小写`\delta`

      $\alpha,\beta,\omega,\Gamma, \Delta,\Omega$

      `\alpha,\beta,\omega,\Gamma, \Delta,\Omega`

   3. 上下标

      `上标^，下标_`

   4. "{...}"的应用

      X^{Y^Z},{X^Y}^Z$,分别写作`X^{Y^Z},{X^Y}^Z`

   5. 可以调整大小的括号等

      $\left(...\right)$ `\left(...\right)`

      $\left[...\right]$ `\left[...\right]`

      $\left\{...\right\}$ `\left\{...\right\}`

   6. 求和，积分

      `\sum` $\sum$,`\prod` $\prod$, `\int` $\int$ , `\bigcup`  $\bigcup$, `\bigcap`  $\bigcap$, `\iint` $\iint$, `\iiint` $\iiint$, `\idotsint` $\idotsint$

      带上下标，例如：`\sum_{i=0}^\infty i^2`, $\sum_{i=0}^\infty i^2$

   7. 分数

      `\frac{...}{...}`，前者为分子，后者为分母

   8. 开方符号

      `\sqrt{...}`

   9. special functions

      `\sin x, \cos x, \lim_{x\to 0}, \max, \ln x`

      $\sin x, \cos x, \lim_{x\to 0}, \max, \ln x$

   10. special symbolcs and notations

       - 数值关系：$\gt$, `\gt`; $\lt$, `\lt`; $\le$, `\le`; $\ge$, `\ge`; $\neq$, `\n` eq
       - 运算符号：`\times, \div, \pm, \mp, x \cdot y`,  $\times, \div, \pm, \mp, x \cdot y$
       - 集合关系：`\cup`, $\cup$; `cap`, $\cap$; `setminus`, $\setminus$; `\subset`, $\subset$; `subseteq`, $\subseteq$; `\subsetneq`, $\subsetneq$; `\supset`, $\supset$; `\in`, $\in$; `\notin`, $\notin$; `\emptyset`, $\emptyset$; `\varnothing`, $\varnothing$

   11. 分类等式
       $$
       f(n) = 
       \begin{cases}
       n/2, & \text{if $n$ is even} \\
       3n+1, & \text{if $n$ is odd}
       \end{cases}
       $$
       `f(n) = `

       `\begin{cases}n/2, & \text{if $n$ is even} \\`

       `3n+1, & \text{if $n$ is odd}`

       `\end{cases}`

4. 画图

   安装Graphviz

   查找链接：[https://](https://www.graphviz.org/doc/info/lang.html)[www.graphviz.org/doc/info/lang.html](https://www.graphviz.org/doc/info/lang.html)

5. 标题

   # level 1 `#`

   ## level 2 `##`

   ### level 3 `###`

   #### level 4 `####`

6. 插入图片

   <img src="/Users/grace/Desktop/EYES/WechatIMG2581.jpeg" alt="Pic" style="zoom:25%;" />

   `![图片名称](图片地址"鼠标出现在图片上时会显示的名称")`

7. 表格

   | 1    | 2    | 3    |
   | ---- | ---- | ---- |
   |      |      |      |

   `|1|2|3|`, 回车后会直接生成表格

8. 实操

   $r_p = \beta_P \cdot r_B + \alpha_P + \varepsilon_P$



## Python

1. 可以用Jupyter Notebook实现交互式编程，在终端输入jupyter notebook。优势：实时查看代码运行结果

2. 运行Python：在终端输入python3，再输入python *.py（但这样应该有存储位置要求？）

3. 缩进用空格*4

4. Python基本内建类型

   参考链接：https://docs.python.org/3/library/stdtypes.html

   1. 字符串

   2. 列表 [...]

      示例：`a_list = [1,2,'c','four']`

      操作：

      - `a_list.insert(0,'stuff')`，0表示位置，'stuff'为插入的元素

      - 复杂list的简化生成

        `init_a_list = [i ** 2 for i in range(9)]`

         `init_2d_list = [[i + j for i in range(5)] for j in range(9)]`

   3. 字典 mapping

      `my_dict={i:i**2 for i in range(10)}`
      `my_dict.keys()`  返回冒号前的元素按顺序构成的列表

   4. 集合 (...)，无序

      `a_set = set(1,2,'c','four'])`

   5. 元组，有内建索引，从0开始编号

      `a_tuple = (1,2,'3','four')`

5. 条件语句

6. 循环语句

7. 引用包 import * as **

8. 函数

   - 定义函数 

     `def function_name(variable_name)`

     ​    `indent, blahblah`

   - 定义主函数入口

     `if __name__ = '__main__':`

     ​    `function_name(varaible_name)`

9. 类

   example：

   class cat:

   ```
    def __init__(self,color,step):
       self.color=color
       self.step=step
        
       self.c=0
   
   def jump(self,distance):
       self.c+=distance
   ```
   实例化：

   `blackcat=cat(color='black',step=2)`
   `print(blackcat.step)`

## Git

概念与功能：Git上项目操作

- Repo Dir - 建仓库
- Add - 加文件
- Commit - 提交创建或修改Commit Change
- Discard - 丢弃
- Push Remote - 更成员反馈意见
- Repo Remote - 编辑部
- Merge - 编辑汇总、合并等
- Release - 合并发行





 