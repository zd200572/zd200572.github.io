---
layout:     post
title:      Python爬虫爬取电影图书前250
subtitle:   又一次蹩脚的爬虫应用
date:       2017-11-29
author:     zd200572
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - 爬虫
---

使用Python爬取，代码见[github](https://github.com/zd200572/craw-python):

# 一、top250电影：

1 肖申克的救赎 9.6

2 霸王别姬 9.5

3 这个杀手不太冷 9.4

4 阿甘正传 9.4

5 美丽人生 9.5

6 千与千寻 9.2

7 辛德勒的名单 9.4

8 泰坦尼克号 9.2

9 盗梦空间 9.3

10 机器人总动员 9.3

11 海上钢琴师 9.2

12 三傻大闹宝莱坞 9.1

13 忠犬八公的故事 9.2

14 放牛班的春天 9.2

15 大话西游之大圣娶亲 9.2

16 教父 9.2

17 龙猫 9.1

18 楚门的世界 9.1

19 乱世佳人 9.2

20 天堂电影院 9.1

21 熔炉 9.2

22 触不可及 9.1

23 当幸福来敲门 8.9

24 无间道 9.0

25 星际穿越 9.1

26 十二怒汉 9.4

27 搏击俱乐部 9.0

28 怦然心动 8.9

29 指环王3：王者无敌 9.1

30 少年派的奇幻漂流 9.0

31 鬼子来了 9.2

32 天空之城 9.0

33 蝙蝠侠：黑暗骑士 9.0

34 活着 9.1

35 罗马假日 8.9

36 大话西游之月光宝盒 8.9

37 两杆大烟枪 9.0

38 飞屋环游记 8.9

39 窃听风暴 9.1

40 飞越疯人院 9.0

41 海豚湾 9.3

42 闻香识女人 8.9

43 V字仇杀队 8.8

44 控方证人 9.6

45 哈尔的移动城堡 8.9

46 教父2 9.1

47 美丽心灵 8.9

48 死亡诗社 8.9

49 指环王2：双塔奇兵 8.9

50 指环王1：魔戒再现 8.9

51 情书 8.8

52 辩护人 9.1

53 美国往事 9.1

54 天使爱美丽 8.7

55 饮食男女 9.1

56 疯狂动物城 9.2

57 钢琴家 9.0

58 狮子王 8.9

59 七宗罪 8.7

60 被嫌弃的松子的一生 8.9

61 致命魔术 8.8

62 小鞋子 9.2

63 勇敢的心 8.8

64 剪刀手爱德华 8.7

65 音乐之声 8.9

66 素媛 9.1

67 低俗小说 8.8

68 本杰明·巴顿奇事 8.7

69 黑客帝国 8.8

70 沉默的羔羊 8.7

71 入殓师 8.8

72 拯救大兵瑞恩 8.9

73 西西里的美丽传说 8.7

74 蝴蝶效应 8.7

75 玛丽和马克思 8.9

76 春光乍泄 8.8

77 让子弹飞 8.7

78 心灵捕手 8.7

79 大闹天宫 9.2

80 幽灵公主 8.8

81 阳光灿烂的日子 8.7

82 第六感 8.8

83 重庆森林 8.7

84 大鱼 8.7

85 射雕英雄传之东成西就 8.7

86 禁闭岛 8.6

87 甜蜜蜜 8.8

88 阳光姐妹淘 8.8

89 一一 8.9

90 上帝之城 8.9

91 致命ID 8.6

92 狩猎 9.0

93 末代皇帝 8.9

94 告白 8.7

95 布达佩斯大饭店 8.7

96 看不见的客人 8.7

97 加勒比海盗 8.6

98 断背山 8.6

99 摩登时代 9.2

100 猫鼠游戏 8.7

101 哈利·波特与魔法石 8.7

102 爱在黎明破晓前 8.7

103 阿凡达 8.6

104 风之谷 8.8

105 爱在日落黄昏时 8.7

106 穿条纹睡衣的男孩 8.9

107 侧耳倾听 8.8

108 消失的爱人 8.7

109 萤火虫之墓 8.7

110 超脱 8.8

111 驯龙高手 8.7

112 倩女幽魂 8.6

113 菊次郎的夏天 8.7

114 恐怖直播 8.7

115 红辣椒 8.9

116 幸福终点站 8.6

117 海洋 9.0

118 七武士 9.2

119 岁月神偷 8.6

120 神偷奶爸 8.5

121 借东西的小人阿莉埃蒂 8.7

122 电锯惊魂 8.7

123 谍影重重3 8.7

124 杀人回忆 8.6

125 贫民窟的百万富翁 8.5

126 真爱至上 8.5

127 雨人 8.6

128 燃情岁月 8.7

129 东邪西毒 8.6

130 记忆碎片 8.5

131 小森林 夏秋篇 8.9

132 喜宴 8.8

133 虎口脱险 8.9

134 喜剧之王 8.5

135 疯狂原始人 8.7

136 怪兽电力公司 8.6

137 黑天鹅 8.5

138 卢旺达饭店 8.8

139 英雄本色 8.7

140 猜火车 8.5

141 穿越时空的少女 8.6

142 魂断蓝桥 8.8

143 恋恋笔记本 8.5

144 雨中曲 8.9

145 傲慢与偏见 8.4

146 教父3 8.7

147 完美的世界 9.0

148 纵横四海 8.7

149 萤火之森 8.7

150 玩具总动员3 8.8

151 哈利·波特与死亡圣器(下) 8.6

152 7号房的礼物 8.7

153 花样年华 8.5

154 海边的曼彻斯特 8.6

155 二十二 8.8

156 我是山姆 8.8

157 荒蛮故事 8.7

158 人工智能 8.6

159 浪潮 8.7

160 香水 8.4

161 冰川时代 8.4

162 小森林 冬春篇 8.9

163 朗读者 8.5

164 追随 8.9

165 撞车 8.6

166 时空恋旅人 8.6

167 唐伯虎点秋香 8.4

168 心迷宫 8.6

169 罗生门 8.7

170 一次别离 8.7

171 超能陆战队 8.6

172 蝙蝠侠：黑暗骑士崛起 8.5

173 战争之王 8.5

174 可可西里 8.7

175 梦之安魂曲 8.7

176 地球上的星星 8.8

177 未麻的部屋 8.8

178 碧海蓝天 8.7

179 爆裂鼓手 8.6

180 恐怖游轮 8.3

181 秒速5厘米 8.3

182 阿飞正传 8.5

183 谍影重重2 8.5

184 达拉斯买家俱乐部 8.6

185 牯岭街少年杀人事件 8.7

186 谍影重重 8.5

187 海盗电台 8.6

188 惊魂记 8.9

189 魔女宅急便 8.4

190 被解救的姜戈 8.5

191 再次出发之纽约遇见你 8.5

192 东京物语 9.2

193 绿里奇迹 8.7

194 青蛇 8.4

195 末路狂花 8.7

196 勇闯夺命岛 8.5

197 迁徙的鸟 9.1

198 哪吒闹海 8.8

199 荒野生存 8.6

200 终结者2：审判日 8.5

201 忠犬八公物语 9.0

202 卡萨布兰卡 8.6

203 这个男人来自地球 8.5

204 源代码 8.3

205 变脸 8.4

206 新龙门客栈 8.4

207 燕尾蝶 8.6

208 黑客帝国3：矩阵革命 8.5

209 E.T. 外星人 8.5

210 黄金三镖客 9.1

211 英国病人 8.4

212 发条橙 8.4

213 城市之光 9.2

214 美国丽人 8.4

215 无耻混蛋 8.4

216 叫我第一名 8.6

217 穆赫兰道 8.3

218 模仿游戏 8.5

219 非常嫌疑犯 8.6

220 初恋这件小事 8.3

221 勇士 8.9

222 上帝也疯狂 8.6

223 房间 8.8

224 蓝色大门 8.3

225 爱在午夜降临前 8.8

226 无敌破坏王 8.6

227 爱·回家 9.0

228 血钻 8.5

229 头脑特工队 8.7

230 国王的演讲 8.3

231 疯狂的石头 8.2

232 大卫·戈尔的一生 8.6

233 枪火 8.6

234 麦兜故事 8.5

235 千钧一发 8.7

236 暖暖内含光 8.4

237 曾经 8.3

238 遗愿清单 8.5

239 荒岛余生 8.5

240 步履不停 8.8

241 一个叫欧维的男人决定去死 8.7

242 蝴蝶 8.6

243 彗星来的那一夜 8.4

244 我爱你 9.0

245 巴黎淘气帮 8.6

246 月球 8.5

247 与狼共舞 8.9

248 偷拐抢骗 8.5

249 无人知晓 9.0

250 寿司之神 8.8

# top250图书：

1 追风筝的人 [美] 卡勒德·胡赛尼 / 李继宏 / 上海人民出版社 / 2006-5 / 29.00元

2 小王子 [法] 圣埃克苏佩里 / 马振聘 / 人民文学出版社 / 2003-8 / 22.00元

3 围城 钱锺书 / 人民文学出版社 / 1991-2 / 19.00

4 解忧杂货店 [日] 东野圭吾 / 李盈春 / 南海出版公司 / 2014-5 / 39.50元

5 活着 余华 / 南海出版公司 / 1998-5 / 12.00元

6 白夜行 [日] 东野圭吾 / 刘姿君 / 南海出版公司 / 2008-9 / 29.80元

7 挪威的森林 [日] 村上春树 / 林少华 / 上海译文出版社 / 2001-2 / 18.80元

8 嫌疑人X的献身 [日] 东野圭吾 / 刘子倩 / 南海出版公司 / 2008-9 / 28.00

9 三体 刘慈欣 / 重庆出版社 / 2008-1 / 23.00

10 不能承受的生命之轻 [捷克] 米兰·昆德拉 / 许钧 / 上海译文出版社 / 2003-7 / 23.00元

11 红楼梦 [清] 曹雪芹 著 / 人民文学出版社 / 1996-12 / 59.70元

12 梦里花落知多少 郭敬明 / 春风文艺出版社 / 2003-11 / 20.00元

13 达·芬奇密码 [美] 丹·布朗 / 朱振武 / 上海人民出版社 / 2004-2 / 28.00元

14 看见 柴静 / 广西师范大学出版社 / 2013-1-1 / 39.80元

15 百年孤独 [哥伦比亚] 加西亚·马尔克斯 / 范晔 / 南海出版公司 / 2011-6 / 39.50元

16 1988：我想和这个世界谈谈 韩寒 / 国际文化出版公司 / 2010-9 / 25.00元

17 何以笙箫默 顾漫 / 朝华出版社 / 2007-4 / 15.00元

18 平凡的世界（全三部） 路遥 / 人民文学出版社 / 2005-1 / 64.00元

19 简爱 [英] 夏洛蒂·勃朗特 / 世界图书出版公司 / 2003-11 / 18.00元

20 哈利·波特与魔法石 [英] J. K. 罗琳 / 苏农 / 人民文学出版社 / 2000-9 / 19.50元

21 白夜行 东野圭吾 / 刘姿君 / 南海出版公司 / 2013-1-1 / 39.50元

22 三体Ⅱ 刘慈欣 / 重庆出版社 / 2008-5 / 32.00

23 飘 [美国] 玛格丽特·米切尔 / 李美华 / 译林出版社 / 2000-9 / 40.00元

24 送你一颗子弹 刘瑜 / 上海三联书店 / 2010-1 / 25.00元

25 三体Ⅲ 刘慈欣 / 重庆出版社 / 2010-11 / 38.00元

26 天才在左 疯子在右 高铭 / 武汉大学出版社 / 2010-2 / 29.80元

27 傲慢与偏见 [英] 奥斯丁 / 张玲 / 人民文学出版社 / 1993-7 / 13.00元

28 倾城之恋 张爱玲 / 花城出版社 / 1997-3-1 / 11.00

29 三重门 韩寒 / 作家出版社 / 2000-5 / 16.00

30 杜拉拉升职记 李可 / 陕西师范大学出版社 / 2007-9 / 26.00元

31 明朝那些事儿（壹） 当年明月 / 中国友谊出版公司 / 2006-9 / 24.80

32 哈利·波特与阿兹卡班的囚徒 [英] J. K. 罗琳 / 郑须弥 / 人民文学出版社 / 2000-9 / 26.50元

33 目送 龙应台 / 生活·读书·新知三联书店 / 2009-10 / 39.00元

34 情人 [法] 玛格丽特·杜拉斯 / 王道乾 / 上海译文出版社 / 2005-7 / 20.00元

35 哈利·波特与密室 [英] J. K. 罗琳 / 马爱新 / 人民文学出版社 / 2000-9 / 22.00元

36 万历十五年 [美] 黄仁宇 / 生活·读书·新知三联书店 / 1997-5 / 18.00元

37 我们仨 杨绛 / 生活·读书·新知三联书店 / 2003-7 / 18.80元

38 幻城 郭敬明 / 春风文艺出版社 / 2003-1 / 28.00元

39 致我们终将逝去的青春 辛夷坞 / 朝华出版社 / 2007-8 / 25.00元

40 1Q84 BOOK 1 [日] 村上春树 / 施小炜 / 南海出版公司 / 2010-5 / 36.00元

41 狼图腾 姜戎 / 长江文艺出版社 / 2004-4 / 32.00元

42 微微一笑很倾城 顾漫 / 江苏文艺出版社 / 2009-8 / 25.00

43 独唱团（第一辑） 韩寒 主编 / 书海出版社 / 2010-7-6 / 16.00元

44 莲花 安妮宝贝 / 作家出版社 / 2006-3 / 25.00元

45 哈利·波特与火焰杯 [英] J. K. 罗琳 / 马爱新 / 人民文学出版社 / 2001-5 / 39.80元

46 边城 沈从文 / 北岳文艺出版社 / 2002-4 / 12.00元

47 月亮和六便士 [英] 毛姆 / 傅惟慈 / 上海译文出版社 / 2006-8 / 15.00元

48 向左走·向右走 幾米 / 生活·读书·新知三联书店 / 2002-8 / 16.00元

49 活着 余华 / 作家出版社 / 2012-8 / 20.00元

50 穆斯林的葬礼 霍达 / 北京十月文艺出版社 / 1988-12-1 / 32.00

51 从你的全世界路过 张嘉佳 / 湖南文艺出版社 / 2013-11-1 / CNY 39.80

52 悲伤逆流成河 郭敬明 / 长江文艺出版社 / 2007-5 / 24.00元

53 恶意 [日] 东野圭吾 / 娄美莲 / 南海出版公司 / 2009-6 / 18.00

54 天龙八部 金庸 / 三联书店 / 1994-5 / 96.0

55 放学后 [日]东野圭吾 / 赵峻 / 南海出版公司 / 2010-1 / 20.00元

56 Harry Potter and the Deathly Hallows J.K.Rowling / Arthur A. Levine Books / 2007-7-21 / 34.99美元

57 长安乱 韩寒 / 中国青年出版社 / 2004-8 / 20.00元

58 哈利·波特与混血王子 [英] J. K. 罗琳 / 马爱农 / 人民文学出版社 / 2005-10 / 58.00元

59 一个人的好天气 [日] 青山七惠 / 竺家荣 / 上海译文出版社 / 2007-9 / 15.00元

60 苏菲的世界 （挪威）乔斯坦·贾德 / 萧宝森 / 作家出版社 / 1999-04 / 26.80元

61 许三观卖血记 余华 / 南海出版公司 / 1998-9 / 16.80元

62 1995-2005夏至未至 郭敬明 / 春风文艺出版社 / 2005-2 / 24.00元

63 撒哈拉的故事 三毛 / 皇冠出版社 / 1976 / 160 TWD

64 盗墓笔记 南派三叔 / 中国友谊出版公司 / 2007-1 / 26.80元

65 霍乱时期的爱情 [哥伦比亚] 加西亚·马尔克斯 / 杨玲 / 南海出版公司 / 2012-9-1 / 39.50元

66 哈利·波特与凤凰社 [英] J. K. 罗琳 / 马爱农 / 人民文学出版社 / 2003-9 / 59.00元

67 喜宝 亦舒 / 新世界出版社 / 2007-2 / 22.00元

68 岛上书店 [美] 加·泽文 / 孙仲旭 / 江苏凤凰文艺出版社 / 2015-5 / CNY 35.00

69 三生三世 十里桃花 唐七公子 / 沈阳出版社 / 2009-1 / 26.80

70 海边的卡夫卡 [日] 村上春树 / 林少华 / 上海译文出版社 / 2003-4 / 25.00元

71 文化苦旅 余秋雨 / 东方出版中心 / 2001-4 / 22.00元

72 基督山伯爵 大仲马 / 周克希 / 上海译文出版社 / 1991-12-1 / 43.90元

73 窗边的小豆豆 [日] 黑柳彻子 著 / 赵玉皎 / 南海出版公司 / 2003-1 / 20.00元

74 三国演义（全二册） [明] 罗贯中 / 人民文学出版社 / 1998-05 / 39.50元

75 黄金时代 王小波 / 花城出版社 / 1999-3 / 19.00元

76 悟空传 今何在 / 光明日报出版社 / 2001-4 / 14.80元

77 兄弟（上） 余华 / 上海文艺出版社 / 2005-8 / 16.00元

78 呼啸山庄 艾米莉·勃朗特 / 张扬 / 人民文学出版社 / 1999-1 / 27.30元

79 笑傲江湖（全四册） 金庸 / 生活·读书·新知三联书店 / 1994-5 / 76.80元

80 少有人走的路 [美] M·斯科特·派克 / 于海生 / 吉林文史出版社 / 2007-1 / 26.00元

81 民主的细节 刘瑜 / 上海三联书店 / 2009-6 / 25.00

82 亲爱的安德烈 龙应台 / 人民文学出版社 / 2008-12 / 26.00

83 灿烂千阳 [美] 卡勒德·胡赛尼 / 李继宏 / 上海人民出版社 / 2007-9 / 28.00元

84 老人与海 海明威 / 吴劳 / 上海译文出版社 / 1999-10 / 8.20元

85 遇见未知的自己 张德芬 / 华夏出版社 / 2008-1 / 29.00

86 一九八四·动物农场 [英] 乔治·奥威尔 / 董乐山 / 上海译文出版社 / 2003-4 / 23.00元

87 牧羊少年奇幻之旅 [巴西]保罗·柯艾略 / 丁文林 / 南海出版公司 / 2009-3-1 / 25.00元

88 福尔摩斯探案全集（上中下） [英] 阿·柯南道尔 / 丁钟华 等 / 群众出版社 / 1981-8 / 53.00元/68.00元

89 小时代1.0折纸时代 郭敬明 / 长江文艺出版社 / 2008-10 / 29.80元

90 洛丽塔 [美] 弗拉基米尔·纳博科夫 / 主万 / 上海译文出版社 / 2005-12 / 27.00元

91 百年孤独 [哥伦比亚] 加西亚·马尔克斯 / 黄锦炎 / 上海译文出版社 / 1989-10 / 12.70元

92 1Q84 BOOK 2 [日] 村上春树 / 施小炜 / 南海出版公司 / 2010-6 / 36.00元

93 素年锦时 安妮宝贝 / 作家出版社 / 2007-9 / 27.00元

94 情书 [日] 岩井俊二 / 穆晓芳 / 天津人民出版社 / 2004-7 / 18.00元

95 第一次的亲密接触 蔡智恒 / 知识出版社 / 1999-11-1 / 12.80

96 神雕侠侣 金庸 / 生活·读书·新知三联书店 / 1994-5 / 76.8

97 一座城池 韩寒 / 二十一世纪出版社 / 2006-1 / 19.90元

98 茶花女 小仲马 / 王振孙 / 外国文学出版社 / 1997-3 / 9.00元

99 麦田里的守望者 [美国] J. D. 塞林格 / 施咸荣 / 译林出版社 / 1997-2 / 7.80元

100 他的国 韩寒 / 万卷出版公司 / 2009-1 / 25.00元

101 彼岸花 安妮宝贝 / 南海出版公司 / 2001-9 / 20.00元

102 西决 笛安 / 长江文艺出版社 / 2009-3 / 22.80元

103 东方快车谋杀案 [英] 阿加莎·克里斯蒂 / 陈尧光 / 人民文学出版社 / 2006-5 / 18.00元

104 挪威的森林 [日] 村上春树 / 林少华 / 上海译文出版社 / 2007-7 / 23.00元

105 这些都是你给我的爱 文：安东尼 / 长江文艺出版社 / 2010-3 / 24.80元

106 这些人，那些事 吴念真 / 译林出版社 / 2011-9 / 28.00元

107 八月未央 安妮宝贝 / 作家出版社 / 2001-1 / 16.00元

108 当我谈跑步时我谈些什么 [日] 村上春树 / 施小炜 / 南海出版公司 / 2009-1 / 25.00

109 明朝那些事儿（贰） 当年明月 / 中国友谊出版公司 / 2007-1 / 24.80

110 清醒纪 安妮宝贝 / 天津人民出版社 / 2004-10 / 22.00元

111 一个陌生女人的来信 [奥] 斯台芬·茨威格 / 张玉书 / 上海译文出版社 / 2007-7 / 20.00元

112 蔡康永的说话之道 蔡康永 著 / 沈阳出版社 / 2010-10 / 25.00元

113 偷影子的人 (法)马克·李维 / 段韵灵 / 湖南文艺出版社 / 2012-6-20 / 29.80元

114 陪安东尼度过漫长岁月 安东尼 / 长江文艺出版社 / 2008-3 / 18.00

115 沉默的大多数 王小波 / 中国青年出版社 / 1997-10 / 27.00元

116 白鹿原 陈忠实 / 人民文学出版社 / 1997年 / 28.00元

117 芒果街上的小屋 [美国] 桑德拉·希斯内罗丝 / 潘帕 / 译林出版社 / 2006-6 / 24.50元

118 羊脂球 （法）莫泊桑 / 柳鸣九 / 北京燕山出版社 / 2007-6 / 13.50元

119 鲁滨逊漂流记 [英] 笛福 / 马静 / 广西民族出版社 / 2002-1 / 9.20元

120 灌篮高手31 [日] 井上雄彦 / 邹宁 / 长春出版社 / 2005-1 / 7.50元

121 撒哈拉的故事 三毛 / 哈尔滨出版社 / 2003-8 / 15.80元

122 巴黎圣母院 [法]雨果 / 陈敬容 / 人民文学出版社 / 1982-6 / 22.50元

123 肖申克的救赎 [美] 斯蒂芬·金 / 施寄青 / 人民文学出版社 / 2006-7 / 29.90元

124 麦田里的守望者 [美国] J. D. 塞林格 / 孙仲旭 / 译林出版社 / 2007-3 / 28.00元

125 无声告白 [美] 伍绮诗 / 孙璐 / 江苏凤凰文艺出版社 / 2015-7 / 35.00元

126 嫌疑人X的献身 （日）东野圭吾 / 刘子倩 / 南海出版公司 / 2009年11月 / 19.80元

127 山楂树之恋 艾米 / 江苏文艺出版社 / 2007-9 / 25.00元

128 华胥引（全二册） 唐七公子 / 现代出版社 / 2011-1 / 39.80元

129 地下铁 幾米 / 辽宁教育出版社 / 2002-2 / 32.00元

130 且听风吟 [日] 村上春树 / 林少华 / 上海译文出版社 / 2001-8 / 11.80元

131 钢铁是怎样炼成的 [苏] 尼·奥斯特洛夫斯基 / 曹缦西 / 译林出版社 / 1996-10 / 20.00元

132 红玫瑰与白玫瑰 张爱玲 / 花城出版社 / 1996-06 / 12.80元

133 人生若只如初见 安意如 / 天津教育出版社 / 2006-8 / 23.80元

134 人间失格 太宰治 / 许时嘉 / 吉林出版集团有限责任公司 / 2009年9月 / 16.00元

135 鬼吹灯之精绝古城 天下霸唱 / 安徽文艺出版社 / 2006 / 25.0

136 安徒生童话故事集 （丹麦）安徒生 / 叶君健 / 人民文学出版社 / 1997-08 / 25.00

137 呐喊 鲁迅 / 人民文学出版社 / 1973年3月 / 0.36元

138 小团圆 张爱玲 / 北京十月文艺出版社 / 2009-4 / 28.00

139 泡沫之夏 明晓溪 / 新世界出版社 / 2006-3 / 20.00元

140 会有天使替我爱你 明晓溪 / 新世界出版社 / 2005-5 / 20.00元

141 1984 [英] 乔治·奥威尔 / 刘绍铭 / 北京十月文艺出版社 / 2010-4-1 / 28.00

142 年华是无效信 落落 / 春风文艺出版社 / 2005-2 / 20.00元

143 幻夜 〔日〕东野圭吾 / 李炜 / 南海出版公司 / 2009年9月 / 28.00元

144 在路上 [美] 杰克·凯鲁亚克 / 王永年 / 上海译文出版社 / 2006-10 / 28.00元

145 射雕英雄传（全四册） 金庸 / 生活·读书·新知三联书店 / 1999-04 / 47.00元

146 明朝那些事儿（1-9） 当年明月 / 中国海关出版社 / 2009-4 / 358.20元

147 月亮忘記了 幾米 / 格林 / 2000-2-1 / NT$ 299

148 明朝那些事儿（叁） 当年明月 / 中国友谊出版公司 / 2007-4 / 24.80

149 哭泣的骆驼 三毛 / 哈尔滨出版社 / 2003-6 / 15.80元

150 原来你还在这里 辛夷坞 / 朝华出版社 / 2007-10 / 25.00元

151 半生缘 张爱玲 / 北京十月文艺出版社 / 2006-12 / 28.00元

152 此间的少年 江南 / 华文出版社 / 2004-1 / 25.00元

153 货币战争 宋鸿兵 编著 / 中信出版社 / 2007-6 / 38.00元

154 佳期如梦 匪我思存 / 新世界出版社 / 2007-2 / 20.00元

155 人类简史 [以色列]尤瓦尔·赫拉利 / 林俊宏 / 中信出版社 / 2014-11-1 / CNY 68.00

156 无人生还 [英] 阿加莎・克里斯蒂 / 祁阿红 / 人民文学出版社 / 2008-3 / 19.00

157 一個人住第5年 高木直子 / 洪俞君 / 大田 / 2004-12-1 / NT$220

158 了不起的盖茨比 菲茨杰拉德 / 姚乃强 / 人民文学出版社 / 2004-06 / 12.00元

159 时间旅行者的妻子 [美] 奥德丽·尼芬格 / 夏金 / 人民文学出版社 / 2007-4 / 29.90元

160 告别薇安 安妮宝贝 / 中国社会科学出版社 / 2000-1 / 19.00

161 常识 梁文道 / 广西师范大学出版社 / 2009-1 / 38.00

162 爱你就像爱生命 王小波 / 上海锦绣文章出版社 / 2008-5 / 18.00元

163 撒哈拉的故事 三毛 / 北京十月文艺出版社 / 2011-1-7 / 24.00元

164 步步惊心 桐华 / 民族出版社 / 2006-6 / 25.00元

165 皮囊 蔡崇达 / 天津人民出版社 / 2014-12-1 / 39.80元

166 二三事 安妮宝贝 / 南海出版公司 / 2004-1 / 20.00元

167 兄弟（下） 余华 / 上海文艺出版社 / 2006-3 / 27.00元

168 孤独六讲 蒋勋 / 广西师范大学出版社 / 2009-10-1 / 36.00元

169 乌合之众 (法)古斯塔夫.勒庞 / 冯克利 / 中央编译出版社 / 1998-01 / 16.00元

170 盗墓笔记2 南派三叔 / 中国友谊出版公司 / 2007-4 / 26.80元

171 明朝那些事儿（肆） 当年明月 / 中国友谊出版公司 / 2007-9 / 24.80

172 失恋33天 鲍鲸鲸 / 中信出版社 / 2010-1 / 25.00元

173 动物农场 [英] 乔治·奥威尔 / 荣如德 / 上海译文出版社 / 2007-3 / 10.00元

174 左耳 饶雪漫 / 当代世界出版社 / 2006-2 / 22.00元

175 鹿鼎记（全五册） 金庸 / 广州出版社 花城出版社 / 2008-3 / 108.00元

176 荆棘鸟 [澳] 考琳·麦卡洛 / 曾胡 / 译林出版社 / 1998-7 / 28.00元

177 左手倒影，右手年华。 郭敬明 / 上海译文出版社 / 2003-5 / 16.00元

178 零下一度 韩寒 / 上海人民出版社 / 2000-08 / 12.00

179 像少年啦飞驰 韩寒 / 作家出版社 / 2002-1 / 16.00元

180 寻路中国 [美] 彼得·海斯勒 / 李雪顺 / 上海译文出版社 / 2011-1 / 33.00元

181 被窝是青春的坟墓 七堇年 / 长江文艺出版社 / 2007-11 / 22.00元

182 我们台湾这些年 廖信忠 / 重庆出版集团 / 2009-11 / 29.80元

183 1Q84 BOOK 3 [日] 村上春树 / 施小炜 / 南海出版公司 / 2011-1 / 39.50元

184 关于莉莉周的一切 [日] 岩井俊二 / 张苓 / 天津人民出版社 / 2006-12 / 28.00元

185 机器猫哆啦A梦23 藤子・F・不二雄 / 碧日 / 吉林美术出版社 / 1999-12 / 8.00

186 阿Q正传 鲁迅 / 上海书店出版社 / 2003-7 / 14.50元

187 乖，摸摸头 大冰 / 湖南文艺出版社 / 2014-9-1 / 36.00元

188 大地之灯 七堇年 / 长江文艺出版社 / 2007-1 / 22.00元

189 摆渡人 [英]克莱儿·麦克福尔 / 付强 / 百花洲文艺出版社 / 2015-6-1 / 36.00

190 黄金时代 王小波 / 陕西师范大学出版社 / 2009-07-01 / 23.00元

191 明朝那些事儿（伍） 当年明月 / 中国友谊出版公司 / 2008-3 / 28.80

192 骆驼祥子 老舍 / 人民文学出版社 / 2000-3-1 / 12.00

193 盗墓笔记3 南派三叔 / 中国友谊出版公司 / 2007-11 / 26.80元

194 麦琪的礼物 [美] 欧·亨利 / 张经浩 / 上海社会科学院出版社 / 2003-7 / 25.00元

195 格林童话全集 格林兄弟 / 魏以新 / 人民文学出版社 / 1994-11 / 21.45元

196 如何阅读一本书 [美] 莫提默·J. 艾德勒 / 郝明义 / 商务印书馆 / 2004-1 / 38.00元

197 当我们谈论爱情时我们在谈论什么 [美] 雷蒙德·卡佛 / 小二 / 译林出版社 / 2010-1 / 22.00元

198 尘埃落定 阿来 / 人民文学出版社 / 1998-3-1 / 22.0

199 水仙已乘鲤鱼去 张悦然 / 作家出版社 / 2005-1 / 19.00元

200 历史深处的忧虑 林达 / 生活·读书·新知三联书店 / 1997-5 / 19.00元

201 嫌疑人X的献身 东野圭吾 / 刘子倩 / 南海出版公司 / 2014-6 / 35.00元

202 小时代2.0虚铜时代 郭敬明 / 长江文艺出版社 / 2010-1 / 26.80元

203 金锁记 张爱玲 / 哈尔滨出版社 / 2005-6 / 13.5元

204 你好，旧时光（上 下） 八月长安 / 新世界出版社 / 2009-12 / 39.80元

205 东霓 笛安 / 长江文艺出版社 / 2010-7-1 / 26.80元

206 海贼王 尾田荣一郎 / 董科 / 浙江人民美术出版社 / 2007-11 / 7.50元

207 那些回不去的年少时光 桐华 / 江苏文艺出版社 / 2010-01 / 23.80元

208 孩子你慢慢来 龙应台 / 生活·读书·新知三联书店 / 2009-12-1 / 28.00元

209 橙 安东尼 / 长江文艺出版社 / 2010-10 / 28.80元

210 悲惨世界（上中下） [法] 雨果 / 李丹 / 人民文学出版社 / 1992-6 / 66.00元

211 盗墓笔记4 南派三叔 / 中国友谊出版公司 / 2008-11 / 32.80元

212 巴别塔之犬 [美] 卡罗琳·帕克丝特 / 何致和 / 南海出版公司 / 2007-7 / 22.00元

213 香水 [德] 帕·聚斯金德 / 李清华 / 上海译文出版社 / 2005-5 / 20.00元

214 梦里花落知多少 三毛 / 北京十月文艺出版社 / 2007-6 / 28.00元

215 一只特立独行的猪 王小波 / 北方文艺出版社 / 2006-4 / 18.80元

216 局外人 [法] 阿尔贝·加缪 / 柳鸣九 / 上海译文出版社 / 2010-9 / 22.00元

217 一个人的朝圣 【英】蕾秋·乔伊斯 / 黄妙瑜 / 北京联合出版公司 / 2013-9-1 / 32.80

218 史蒂夫·乔布斯传 [美] 沃尔特·艾萨克森 / 管延圻 / 中信出版社 / 2011-10-24 / 68.00元

219 看不见的城市 [意大利]伊塔洛·卡尔维诺 / 张宓 / 译林出版社 / 2006-8 / 16.00元

220 长恨歌 王安忆 / 南海出版公司 / 2003-8 / 22.00元

221 匆匆那年（上下） 九夜茴 / 东方出版社 / 2008-1 / 29.00

222 草样年华 孙睿 / 远方出版社 / 2004-1 / 19.50元

223 往事并不如烟 章诒和 / 人民文学出版社 / 2004-1 / 35.00元

224 蔷薇岛屿 安妮宝贝 / 作家出版社 / 2002-8 / 18.00元

225 我的路 寂地 / 北方妇女儿童出版社 / 2004-10 / 20.00元

226 菊与刀 （美）鲁思・本尼迪克特 / 吕万和 / 商务印书馆 / 1990-6 / 16.00

227 倾城之恋 张爱玲 / 北京十月文艺出版社 / 2006-12 / 29.80元

228 刀锋 [英]毛姆 / 周煦良 / 上海译文出版社 / 2007-3 / 18.00元

229 球状闪电 刘慈欣 / 四川科学技术出版社 / 2005-6 / 22.00元

230 谁动了我的奶酪？ [美] 斯宾塞·约翰逊 / 吴立俊 / 中信出版社 / 2001-9 / 16.80元

231 飞鸟集 [印] 罗宾德拉纳德·泰戈尔 / 徐翰林 / 哈尔滨出版社 / 2004-6 / 16.80元

232 七夜雪 沧月 / 北京十月文艺出版社 / 2006-10 / 25.00元

233 曾有一个人，爱我如生命 舒仪 / 中国画报出版社 / 2009-3 / 23.80

234 那些年，我们一起追的女孩 九把刀 / 花山文艺出版社 / 2007-1 / 20.00元

235 伊豆的舞女 [日] 川端康成 / 叶渭渠 / 广西师范大学出版社 / 2002-2 / 23.80元

236 世界尽头与冷酷仙境 [日] 村上春树 / 林少华 / 上海译文出版社 / 2002-12 / 23.00元

237 傲慢与偏见 [英] 奥斯丁 / 王科一 / 上海译文出版社 / 1996-12 / 11.00元

238 最初的爱情 最后的仪式 [英] 伊恩·麦克尤恩 / 潘帕 / 南京大学出版社 / 2010-2 / 22.00元

239 鬼吹灯之云南虫谷 天下霸唱 / 安徽文艺出版社 / 2006-11 / 26.80元

240 明朝那些事儿（柒）：大结局 当年明月 / 中国海关出版社 / 2009-4 / 29.80元

241 把时间当作朋友 李笑来 / 电子工业出版社 / 2009-6 / 32.00元

242 秘密 [澳] 朗达·拜恩 / 谢明宪 / 中国城市出版社 / 2008-11 / 32.00

243 天使与魔鬼 [美] 丹.布朗 / 朱振武 / 人民文学出版社 / 2005-2 / 29.80元

244 拆掉思维里的墙 古典 / 中国书店 / 2010-9 / 29.80元

245 明朝那些事儿（陆） 当年明月 / 中国海关出版社 / 2008-11 / 28.80

246 佛祖在一号线 李海鹏 / 文化艺术出版社 / 2010-6 / 25.00元

247 倚天屠龙记(共四册) 金庸 / 三联书店 / 1999-04 / 0

248 阿狸·梦之城堡 hans / 上海锦绣文章出版社 / 2009-1 / 36.80元

249 杜拉拉2华年似水 李可 / 陕西师范大学出版社 / 2009-1 / 28.00

250 不朽 落落 / 长江文艺出版社 / 2007-12 / 22.00

我的个人博客：[http://blog.zd200572.com](http://blog.zd200572.com/)和[www.zd200572.com](http://www.zd200572.com/)