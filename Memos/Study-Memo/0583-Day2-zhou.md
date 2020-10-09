### 课程小结2 周航宇 2017010583
#### markdown语法使用
##### 列表
1.项目1
2.项目2
3.项目3
##### 表格
|  表格  | 表头  |
|  ----  | ----  |
| 单元格1 | 单元格3 |
| 单元格2 | 单元格4 |
| test |  |
##### 公式
这是一个行间公式
$$ r_p=\beta_P\cdot r_B+\alpha_p+\epsilon_P$$
内联公式$a^2+b^2=c^2$ 

#### git 使用
##### git添加/删除文件
~~~bash
git add .
git commit -m "mycommit"
git rm 
~~~
##### git克隆/上传/更新
~~~bash
git clone 
git push
git pull
~~~
##### 其他用法
~~~bash
git status
git reset --hard  版本回滚
git branch -a 查看远程分支
git branch test 创建test分支
git checkout test 切换到test分支
~~~

#### python使用
##### 安装
~~~bash
sudo apt-get install python3
~~~
##### 虚拟环境配置
~~~bash
virtualenv test
source test/bin/activate
pip3 install package_name
~~~
##### python基本使用
~~~python
list=[1,2,3]
list
set=(1,2,3,4)
set
a={'1':'one'}
a
tdlist=[[i for i in range(9)] for _ in range(9)]
tdlist
lists=[i for i in range(5)]
for list in lists:
    print(list)
for i in range(5):
    print(f'Hello{i}')
~~~

#### 稳定绩效

 	长期视角、风险与收益的平衡、盈亏同源、系统性的方法和执行手段
#### 交易系统的关键要素
 	胜率、赔率、成本、频率、头寸、本金
 	打雪仗模型

#### 行为金融学
 	有效市场假说：理性交易者、市场无摩擦->价格正确
 	质疑：纠正定价错误也需承担风险和成本，错误定价仍然存在
 	启示：避免非理性、抓住他人非理性机会、世界主力陷阱、顺逆
 	禀赋效应、跨期选择、心理账户

### 套利限制与投资者行为
 	有效市场假说漏洞->交易者非绝对理性->行为金融学解释非理性原因->寻找非理性现象->策略捕获
 	噪音交易者、套利者
 	严格套利的风险和成本：基本面风险、噪音交易者风险、实施成本
	
