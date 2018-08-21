# 中文数据预处理材料
包含素材：
* Files --
	* 分词词典: 综合了百度、搜狗等词库，以及手动整理的若干人名和新近出现的热词
	* 中文停用词: 综合了"百度停用词表"，"哈工大停用词表"，"四川大学机器学习实验室停用词表"等若干停用词表，取交集并去除了不需要的标点符号和英文单词
* Outer Link --
	* [中文人名语料库](https://github.com/wainshine/Chinese-Names-Corpus)
* Tips --
	* stopwords.dat为utf-8编码，使用时
	```python
	with open('stopwords.dat','r') as fin:
		word_in_unicode = fin.readline.strip().decode('utf-8')
	```
	* Chinese extraction
	```python
	import re
	def Chinese_word_extraction(content_raw):
		chinese_pattern = u"([\u4e00-\u9fa5]+)"
		chi_pattern = re.compile(chinese_pattern)
		re_data = chi_pattern.findall(content_raw)
		content_clean  = ' '.join(re_data)
	```

	* Traditional 2 Simplified
	```python
	from hanziconv import HanziConv
	def tra2sim(content):
		content = HanziConv.toSimplified(content)
	```

	* Interesting Synonyms
	```python
	replace_dict = {
		u'吻腚':u'稳定',
		u'弓虽':u'强',
		u'女干':u'奸',
		u'示土':u'社',
		u'禾口':u'和',
		u'言皆':u'谐',
		u'释永性':u'释永信',
		u'大菊观':u'大局观',
		u'yl':u'一楼',
		u'cnm':u'草泥马',
		u'CCTV':u'中央电视台',
		u'CCAV':u'中央电视台',
		u'ccav':u'中央电视台',
		u'cctv':u'中央电视台',
		u'qq':u'腾讯聊天账号',
		u'QQ':u'腾讯聊天账号',
		u'cctv':u'中央电视台',
		u'CEO':u'首席执行官',
		u'克宫':u'克里姆林宫',
		u'PM2.5':u'细颗粒物',
		u'pm2.5':u'细颗粒物',
		u'SDR':u'特别提款权',
		u'装13':u'装逼',
		u'213':u'二逼',
		u'13亿':u'十三亿',
		u'巭':u'功夫',
		u'孬':u'不好',
		u'嫑':u'不要',
		u'夯':u'大力',
		u'芘':u'操逼',
		u'烎':u'开火',
		u'菌堆':u'军队',
		u'sb':u'傻逼',
		u'SB':u'傻逼',
		u'Sb':u'傻逼',
		u'sB':u'傻逼',
		u'is':u'伊斯兰国',
		u'isis':u'伊斯兰国',
		u'ISIS':u'伊斯兰国',
		u'ko':u'打晕',
		u'你M':u'你妹',
		u'你m':u'你妹',
		u'震精':u'震惊',
		u'返工分子':u'反共',
		u'黄皮鹅狗':u'黄皮肤俄罗斯狗腿',
		u'苏祸姨':u'苏霍伊',
		u'混球屎报':u'环球时报',
		u'屎报':u'时报',
		u'jb':u'鸡巴',
		u'j巴':u'鸡巴',
		u'j8':u'鸡巴',
		u'J8':u'鸡巴',
		u'JB':u'鸡巴',
		u'瞎BB':u'瞎说',
		u'nb':u'牛逼',
		u'牛b':u'牛逼',
		u'牛B':u'牛逼',
		u'牛bi':u'牛逼',
		u'牛掰':u'牛逼',
		u'苏24':u'苏两四',
		u'苏27':u'苏两七',
		u'痰腐集团':u'贪腐集团',
		u'痰腐':u'贪腐',
		u'反hua':u'反华',
		u'<br>':u' ',
		u'屋猫':u'五毛',
		u'5毛':u'五毛',
		u'傻大姆':u'萨达姆',
		u'霉狗':u'美狗',
		u'TMD':u'他妈的',
		u'tmd':u'他妈的',
		u'japan':u'日本',
		u'P民':u'屁民',
		u'八离开烩':u'巴黎开会',
		u'傻比':u'傻逼',
		u'潶鬼':u'黑鬼',
		u'cao':u'操',
		u'爱龟':u'爱国',
		u'天草':u'天朝',
		u'灰机':u'飞机',
		u'张将军':u'张召忠',
		u'大裤衩':u'中央电视台总部大楼',
		u'枪毕':u'枪毙',
		u'环球屎报':u'环球时报',
		u'环球屎包':u'环球时报',
		u'混球报':u'环球时报',
		u'还球时报':u'环球时报',
		u'人X日报':u'人民日报',
		u'人x日报':u'人民日报',
		u'清只县':u'清知县',
		u'PM值':u'颗粒物值',
		u'TM':u'他妈',
		u'首毒':u'首都',
		u'gdp':u'国内生产总值',
		u'GDP':u'国内生产总值',
		u'鸡的屁':u'国内生产总值',
		u'999':u'红十字会',
		u'霉里贱':u'美利坚',
		u'毛子':u'俄罗斯人',
		u'ZF':u'政府',
		u'zf':u'政府',
		u'蒸腐':u'政府',
		u'霉国':u'美国',
		u'狗熊':u'俄罗斯',
		u'恶罗斯':u'俄罗斯',
		u'我x':u'我操',
		u'x你妈':u'操你妈',
		u'p用':u'屁用',
		u'胎毒':u'台独',
		u'DT':u'蛋疼',
		u'dt':u'蛋疼',
		u'IT':u'信息技术',
		u'1楼':u'一楼',
		u'2楼':u'二楼',
		u'2逼':u'二逼',
		u'二b':u'二逼',
		u'二B':u'二逼',
		u'晚9':u'晚九',
		u'朝5':u'朝五',
		u'黄易':u'黄色网易',
		u'艹':u'操',
		u'滚下抬':u'滚下台',
		u'灵道':u'领导',
		u'煳':u'糊',
		u'跟贴被火星网友带走啦':u'',
		u'猿们':u'公务员们',
		u'棺猿':u'官员',
		u'贯猿':u'官员',
		u'每只猿':u'每个公务员',
		u'巢县':u'朝鲜',
		u'死大林':u'斯大林',
		u'无毛们':u'五毛们',
		u'天巢':u'天朝',
		u'普特勒':u'普京',
		u'依拉克':u'伊拉克',
		u'歼20':u'歼二零',
		u'歼10':u'歼十',
		u'歼8':u'歼八',
		u'f22':u'猛禽',
		u'p民':u'屁民',
		u'钟殃':u'中央'
	}
	```
