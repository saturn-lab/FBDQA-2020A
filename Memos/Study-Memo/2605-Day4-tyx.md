	• Part1
	• 金融大数据部分
		○ 四大理论支柱，都获得经济学奖
			§ 有效市场假说
	• 交易制度
		○ 交易成本：最低五元
		○ 竞价原则：
		○ 股票
			§ 上证主板：600、601、602开头
			§ 上证中小68
			§ 深证主板000
			§ 深证中小002
			§ 创业板300
		○ 新三板不属于a股
	• r：无风险利率/资金成本
	• 债券：信用和久期 久期越长，收益理论上越高，十年期国债
	• 投资组合理论：选sharp ratio最高的，而不是收益最高的
	• 资产选择：用国债来代表无风险利率
	• 小盘股：收益高风险也高
	• CAPM
		○ 与市场相关：系统性风险
		○ 残差项的标准差：公司风险
	• 易混淆
		○ Risk premium
		○ 一个是alpha，一个是收益-无风险利率
	• fisher：金融工程之父

	• Part2
		○ roadmap适用于复习
		○ 
	• 股票池和择时最重要
	• 如果选了每天，pl_trade 会每天调用一次
	• ROE净资产收益率
		○ 杜邦分析
			§ ROE = ROA * 权益乘数
			§ ROA = 净利润/营业收入 * 营业收入/总资产 = 净利率 * 总资产周转次数
	• 沪深300: 000300
	• #Set_option 不用改
	• #Order value下单
	• 在巨宽帮助文档中搜索get_fundamental
	• 练习二
		○ 市值：market_cap
	• 经典指标：MA
	• 金叉死叉
		○ 计算均线：
		○ # 计算需要的数量个数，因为判断上穿最多需要用到3个数据，所以需要多加载两个收盘价	
			pl_count = max(PL_BUY_SHORT_MA,PL_BUY_LONG_MA) + 2
			#加2：回溯两天
			pl_close_data = attribute_history(security=pl_code, count=pl_count, unit='1d',fields=['close'],skip_paused=True, df=True, fq='pre')['close']
			if (list(np.isnan(pl_close_data)).count(True) > 0) or (len(list(pl_close_data)) < pl_count):
			continue
		
				
	• 金叉：哪怕昨天相等，但前天在下面，也认为是金叉
