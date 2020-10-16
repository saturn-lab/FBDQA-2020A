### 课程小结5 周航宇 2017010583
#### 股票池设计思路
+ 市值因子
+ 估值因子
+ 超跌因子
+ ST股票的处理
##### 选股条件
+ 剔除总市值排名最小的10%的股票
+ 剔除PE小于0或大于100的股票
+ 剔除ST股票
+ 取25日跌幅前10%的股票
##### 再平衡周期
+ 25个交易日
##### 容量
+ 无限制
#### 择时信号设计
##### 买入
+ 20分钟K线，MA3上穿MA200
##### 卖出
+ 20分钟K线，MA3下穿MA200

#### 策略的问题
+ 收益 回撤
+ 交易记录分析
+ 趋势策略：出场信号更重要

#### 股票池进一步优化
##### 选股条件——多因子模型
+ 对因子分类，每一类有不同的权重xi
+ 每一类中有不同的因子
+ 加权平均，计算综合得分

##### 择时信号的优化
+ 周期、级别、顺势
+ N分钟K线、日线、周线、月线、年线
+ MA5、MA30、MA60
+ 小周期大均线
&emsp;及时抓住趋势，避免错误进入（假信号），用短时间的均线穿过更为长期的均线

#### 均值回复型策略
##### 短期市场反转逻辑
+ 选股：过去3（或1）个月表现最差的N只股票构成的组合
+ 再平衡周期：1个月
+ 头寸管理：
    + 所有入选股票均仓
    + 按照市值加权
+ 多空组合：做多表现最差组合、做空表现最好组合
##### 简单原理
+ 尺度量价
+ 缺口方式
+ 套利模式
##### 长期市场反转逻辑
+ 选择股票的时间范围为1~5年
+ 再平衡周期加长，比如1年 

##### 缺口方式的交易策略：日内的均值恢复
1.选择缺口型股票：开盘瞬间，选择所有的前一日最低价至今日开盘价之间收益率
低于一个标准差的股票。标准差为90天的日间收盘价的收益率的标准差。（按缺口大小对全部股票排序）
2.缩小范围：只保留当日开盘价高于收盘价20日移动平均线的股票。(同时趋势仍然保持（短时牛熊判断）)
3.在剩余股票中，按当日开盘价与前一日最低价相比得出的收益率由低到高排序，
买入排名前10的股票，不足10只就都买入。
4.收盘之间清算（T+1结算？？？）
#### 套利模式
+ 两只股票之间——完美替代品问题
+ 两组股票之间——测定相关性
+ 2种或多种ETF之间
+ ETF与一揽子股票之间
+ 现货与期货之间
##### 退出策略
略

#### 风险
+ 收益率的标准差 STDEV.P=1.5% STDEV=2.13%
+ 投资组合可以分散风险
+ 标准差沿时间的累计
#### 夏普比率：风险和收益的平衡


#### 计算夏普比率、年化收益、最大回撤

#### SQL
#### 关系数据模型
##### Data models & the relational data model
+ Relational model(aka tables)
+ Every relation has a schema
##### Schemas & data independence
+ Logical Data Independence
+ Physical Data Independence

##### SQL介绍
Structured Query Language
+ Data Manipulation Language
+ Data Definition Language
##### Multiset
+ An unordered list for a set with multiple duplicate instances allowed
+ Unions 
+ Cross-product
##### tables
+ A relation or table
+ An attribute or column
+ A tuple or row
+ Cardinality
##### Atomic types
+ CHAR, VARCHAR
+ INT, BIGINT, SMALLINT, FLOAT
+ MONEY, DATETIME
##### Schemas
+ Schema
+ Key
##### create tables
~~~sql
CREATE TABLE Students{
sid CHAR(20),
name VARCHAR(50),
gpa float,
PRIMARY KEY(sid),
}
~~~
##### select
~~~sql
SELECT <attributes>
FROM <one or more relations>
WHERE <conditions>
~~~
##### Multiple table queries
+ Joins
+ Inner Joins
+ Outer Joins

