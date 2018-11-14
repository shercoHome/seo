# seo
## 搜索引擎工作原理
1. 爬行和抓取
    1. 蜘蛛
    2. 跟踪链接
        * 深度优先
        * 广度优先
    3. 吸引蜘蛛
        * 网站和页面权重（质量高、资格老的网站）
        * 页面更新度
        * 导入链接（从哪里可以知道网站链接并进入这个网站）
        * 与首页点击距离
    4. 地址库(记录发现的地页面,与是否收录无关)
        * 人工录入的种子网站
        * 蜘蛛抓取(分析出的新URL,存入待访问地址库)
        * 站长提交
    5. 文件存储
    6. 爬行时的复制内容检测
2. 预处理
    1. 提取文字
    2. 中文分词(有歧义的记事要做处理，如标为黑体)
    3. 去停止词（的、地、得之类）
    4. 消除噪声
        基本方法：对HTML分块（页头、导航、正文、页脚、广告等区域），在网站上大量重复出现的区块往往属于噪声，会被消除。
    5. 去重
        * 页面特征关键词计算指纹
        * 文本指纹算法 
        不止是页面级别，可能进行到段落去重
    6. 正向索引
        在经过以上提取、分词、去停、消噪、去重之后，得取的就是独特的、能反映页面主体内容的、以词为单位的内容。
        接下来搜索引擎就可以提取关键词，把页面转为一个关键词的集合，并记录关键词的频率、格式（标题、黑体、a、h）、位置等权重信息。
        把以上的词集存储进 `以文件ID为索引，以多个关键词为内容的索引库`
    7. 倒排索引
        将索引库重新构造为 `以关键词为索引，以多个文件ID为内容的索引库`
    8. 链接关系计算（PR值、权重）
    9. 特殊文件处理（PDF、TXT、Flash 图片等）
3. 排名
    1. 搜索词处理
        * 中文分词
        * 去停止词
        * 指令处理（默认关键词之间是“与”关系，还有其它高级搜索指令）
        * 拼写错误矫正
        * 整合搜索触发
    2. 文件匹配（关键词1 + 关键词2 = 文件1.2.3.4.5....）
    3. 初始子集选择（从上万或更多的匹配文件中，主要根据页面权重选出1000个作为匹配项进行下一步排名）
    4. 相关性计算
        ` 计算相关性，这是排名过程中最重要的一步 `，影响相关性的主要因素有：
        * 关键词常用程度
            越常用的词对于搜索词的贡献就越小，极致就是停止词。如搜索“我们冥王星”，那么“冥王星”这个词的加权系数就更高
        * 词频及密度
            一般认为如此，但只是相关性因素的一部分，而且重要程度越来越低
        * 关键词位置及形式
            如标题标签、黑体、H1等重要的位置
        * 关键词距离
            如“减肥方法”，四字完成匹配的相关性更高，中间有其它字的话，相关性就更低一些
        * 链接分析及页面权重
            页面有越多以搜索词为锚文字的导入链接，说明页面的相关性越强
    5. 排名过滤及调整
        施加惩罚，如百度第11位 谷歌负6、负30等算法
    6. 排名显示
    7. 搜索缓存
        按2/8定律，20%的搜索词占到了总的搜索次数的80%。
        按长尾理论，最常见的搜索词没有占到80%那么多，但通常也有一个比较粗大的头部。
        所以，搜索引擎会把最常见的搜索词存入缓存
    8. 查询及点击日志
        搜索用户的IP、搜索词、搜索时间、点击了哪些结果页面都会形成日志，用于调整搜索算法。

## 链接原理
现在的搜索引擎都使用链接分析技术减少垃圾，提高用户体验。通过链接信息，可以处理图片、视频、不同语言的页面。
分析关键词，可以观察搜索结果的前几页看到关键词如何分布进行统计分析，但是因为我们不能获得搜索引擎的链接数据库。所以链接影响无法直接了解。
以下用几个链接相关的专利间接了解一下
1. 李彦宏超链分析专利
    要判断哪个页面最具权威性，不能光看页面自己怎么说，还要看其他页面怎么评价
2. HITS算法（超链诱导主题搜索）
    * 枢纽值：所有导出链接页面的权威值之和。典型的枢纽页面：雅虎目录、好123.
    * 权威值：所有导入链接所在页面的枢纽值之和。权威页面通常是提供真正相关内容的页面。
    绝不链接到其它网站的做法，并不是好的SEO方法
3. TrustRank算法（信任指数）
    基于一个假设：好的网站很少会链接到坏的网站；反之则不成立。
    挑选出百分之百信任的网站（人工查看、或根据PR值），计算TurstRank随链接关系减少（按链接次数逐层衰减、按链接数目分配值）；
    现在搜索算法中，TrustRank值也表现在域名级别。
4. Google PR（拉里佩奇发明，斯坦福大学所有，Google永久排他使用的一个专利）
    1. PR定义
        PR是PageRank的缩写，即页面级别，页面权重（本意是，佩奇级别），反向链接越多的，PR值越高（被引用次数）。公式如下
        ```
        PR(A)=(1-d)+d(PR)(t<sub>1</sub>)/C(t<sub>1</sub>)+ ... + PR(t<sub>n</sub>)/C(t<sub>n</sub>))
        ```
        一个页面的PR值取决于导入页的PR值与导入页导出的链接数
    2. 工具条PR（0-10，11个级别）
        真正的PR值 是不间断计算更新中的，工具条RP值 只是某一个时间点上真实PR值 的快照输出，几个月才更新一次。
    3. PR值只与链接有关
        有反射链接就有PR，没有则无。PR的更新与页面排名变化在时间上没有对应关系，因为我们只能看到工具条的PR值，工具条PR的变化早在几个月前就更新和计入排名里了。
    5. PR的意义
        PR在Google中只是200多个因素之一。但还是重要因素之一，体现在：
        * 网站收录深度和总页面数（PR越高，更容易收录内页）
        * 更新频率（PR越高，更快速收录）
        * 重复内容判定
        * 排名初始子集的选择
5. Hilltop算法
    外链来源的主题应该与本站相关
## 用户浏览和点击
1. （英文搜索）页面点击为“F”形的金三角分布
2. （英文搜索）2006年AOL的三个月搜索记录分析首页点击占比：第1名42%，第2名12%，第3-10名8.5、6.1、4.9、4.1、3.4、3.0、2.8、3.0
3. 以上两点不太适用于百度等中文搜索

## 高级搜索指令
1. 双引号，完全匹配搜索——可用于定位特定关键词的竞争对手
2. 减号，排除后面的。比如搜索“苹果 -电影”
3. 星号，*通配符，`百度不支持`
4. inurl: 用于搜索查询词出现在url
5. inanchor: 导入链接锚文字中包含搜索词的页面。`百度不支持`。—- 可以找到某个关键词的竞争对手，以及竞争对手页面有哪些外部链接资源。
6. intitle: 返回title含查询词的页面。找到更准确的竞争页面。
7. allintitle: 同上，用于多组词的“与”关系查询
8. allinurl: 与allintitle类似
9. filetype:pdf SEO，返回含seo的PDF文件
10. site:返回域名下被收录的所有页面
11. link:搜索某个url的反向链接，只返回随机的一部分索引链接。`百度不支持`
12. linkdomain: `只适用于雅虎` ，返回某个域名的反向链接，比较准确，可用的重要工具。如：linkdomain:dunsh.org -site:dunsh.org，排除站内链
    2010.8.24，yahoo正式宣布将其搜索引擎后端完全转换为微软的Bing，所以此指令不可用
13. related: `只适用于Google`，返回与某个网站有关联的页面（一般认为是有共同的外链）

--------

## 竞争研究
* 确定适当的关键词是SEO的第一步
* 竞争对手研究
* 现有网站评估诊断
### 一、为什么研究关键词
1. 确保目标关键词有人搜索
2. 降低优化难度（排除最热闹、搜索次数最多的词）
3. 寻找有效流量（容易转化的词）
    比如搜索“律师”的人，可能只是找律师报考指导，而不是寻求法律援助
4. 搜索多样性
    英文搜索2009的研究表明，用户搜索的关键词4个词以上的在增长，更容易搜索到自己想要的结果
5. 发现新的机会
    通过关键词扩展工具发现有共通性或明显趋势的词，融入网站或增加新栏目，是一个很好的方向

### 二、关键词的选择
原则：
1. 内容相关，以得到有效的流量
2. 搜索次数多，竞争小
3. 主关键词不可太宽泛（比如”房地产“就太宽泛了）
4. 主关键词不可太特殊（比如”北京东街口律师“，不靠谱，没人搜索）
5. 商业价值（即搜索词表达的付费意图，如”液晶电视原理“与”液晶电视促销“）

### 三、关键词竞争程度判断
关键词选择最核心的是 `搜索次数多，竞争程度小`，那么如何判断竞争程度？

关键词 | 搜索结果数 | intitle 数 | 竞价数 | 平均点击价格 | 竞争对手实力 | 前10内页数 | 竞争指数
--------- | --------    |--------   |------ | ------ |--------|--------|--------|
减肥       | 66 400 000 | 9 090 000 | 8+3+2 | ￥1.64 |   9    |    4    |   10   | 
运动减肥   | 17 800 000 |   892 000 | 6+1+2 | ￥0.54 |   6    |   5    |   7   | 

1. 搜索结果数
    10万以下，竞争很小；几十万，有一定难度，需要质量和权重都不错的网站才能竞争；一两百万，很热门的网站……
    以上只是大致的，实际情况还是要综合判断（比如某些疑难杂症的治疗广场，结果少但商业价值高，所以竞争程度也高）
2. intitle 结果数
    标题中出现关键词的页面才是真正的竞争对手
3. 竞价结果数
    页面右侧等地方的竞价广告数量
4. 竞价价格
    具体价格分行业，同行的价格才有可比性
5. 竞争对手情况
    竞争对手网站的外链数量质量、网站结构、页面关键词优化等……
6. 内页排名数量
    一般来说，排在前面的内页数越多，说明竞争越小    
    注：大型知名门户的频道页，也视同首页

### 四、核心关键词
`选择关键词的第一步是确定 网站核心关键词`
核心关键词通常就是网站首页的目标关键词。
* 难度最高、搜索次数最多的两三个是核心关键词，放在首页
* 难度次一级、数量更多的关键词，放在栏目首页或分类首页
* 难度更低的关键词，数量更为庞大，放在具体产品或文章页面  

整个网站的关键词按照搜索次数、竞争程度、优化难度逐级分布  
一量首页核心关键词确定，项下的其它页面也就相应确定了

1. 头脑风暴
    * 你的网站能为用户解决什么问题
    * 用户遇到这些问题时，会搜索什么样的关键词
    * 如果你自己是用户，在寻找这些问题的答案时会怎么搜索
    * 用户在寻找你的产品时会搜索什么关键词
2. 同事、朋友
    其它不熟悉你的产品的人，寻找服务时会搜索什么
3. 竞争对手
    查看竞争对手的网站首页源文件，查找关键词
4. 查询搜索次数
    关键词 | Google月搜索数 |  百度指数 | 竞争指数 | 潜在效能
    ----- | --------       | ------- | ------  | ------- |  
    减肥  |  687 000        |  78645  | 10      | 7   | 
    运动减肥 | 201 000  |  386  | 7  | 6 | 

5. 确定核心关键词
    从以上选出三个作为网站核心关键词

### 五、关键词扩展
研究几十个关键词并不足够，还要找出比核心关键词搜索次数少一些的更多关键词，扩展出几百甚至几千个关键词，常见方式：
1. 关键词工具（百度指数）
2. 搜索建议（在百度搜索框中输入核心关键词，就会提示一些关联搜索）
3. 相关搜索（在搜索结果的最下方）
4. 其它关键词扩展工具（如追词网）
5. 各种形式的变体
    1. 同义词
    2. 相关词（如网站建设、网页设计、网络营销与SEO，也是相关的）
    3. 简写
    4. 错字
6. 补充说明文字
    1. 地名（旅游——云南旅游）
    2. 品牌
    3. 限定和形容词（如 主机——免费主机）
7. 网站流量分析
    查看现有流量，用户都使用什么关键词来到自己的网站。
8. 单词交叉组合
    交叉组合后，会形成大量的关键词，单个搜索不多，但数量庞大，累计流量也是可观的。

### 六、关键词分布
以上扩展，应该已经得到一个至少包含几百个相关关键词的大列表，如何合理分布？
1. 金字塔形结构
    * 核心关键词位于塔尖，只有两三个，使用首页优化
    * 次一级位于塔身，可能有几十个，放在一级分类的首页。意义最相关的两三个关键词放在一起
    * 再次一级位于二级分类 的首页，同样两三个关键词。（小型网站经常不用到二级分类）
    * 更多的长尾关键词放在具体的产品（文章）页面
2. 关键词分组
    将关键词分组，分组就可作为一级分类的依据
3. 关键词布局
    * 每页只针对两三个关键词，使页面主题突出
    * 避免内部竞争（多页面优化同一词，是错误的）
    * 关键词研究决定内容策划（每一版块，分类，都是明确的）
4. 关键词-URL 对应表
    将关键词分配至确定的URL  
    关键词 | 百度指数 | 竞争指数 | 目标URL | 是否收录 | 目前排名 | 目前月搜索流量  | 
    ------ | ------- | -------- | ------ | ------- | -------- | -------------- | 
    减肥瘦身 | 2057 |    10       | www.doani.com | 是 | 78  | 35 | 
    饮食减肥 | 121 | 8 |   www.doani.com/yinshi/ | 是 | 21 | 29 | 
    腹部减肥 | 247 | 7 | www.doani.com/jubu/fubu/ | 否 | 无 | 无 |   

    确定好每一个关键词的优化页面，这样在做内部链接时，凡是提到这个页面的关键词就链接到事先确定的URL

### 七、长尾关键词
1. 长尾理论
    在销售成本忽略不计的情况下，种类巨多但单品销量少的产品带来的效益与热门产品带来的效益相当，类似C形的图
2. 搜索长尾
    在SEO领域，较长的、比较具体的、搜索次数比较低的词，就是长尾关键词。  
    `要形成长尾效应，就需要大量的页面做基础！`
3. 怎么样做长尾关键词
    由于数量庞大，只能通过大量有效内容及网站结构方面的优化确保页面收录。  
    长尾词的排名，也同样与域名权重相关。
    * 关键：页面的基本优化和收录
    * 易：只要页面基本优化做好，长尾关键词排名就能全面提高。页面优化尤其在于内部链接的结构。
    * 难：大量的长尾就要有大量的内容
### 八、三类关键词
1. 导航类关键词（搜索占比10%）
    比如搜索竞争对手的品牌时，你的网站排在前面；
    一般通过增强外部链接和锚文字
2. 交易类关键词（搜索占比10%）
    比如”电视机网上购买“
3. 信息类关键词（搜索占比80%）
    比如”减肥方法“，针对信息类关键词进行优化，是网站长尾页面的任务。
### 九、预估流量及价值





------
------
------

## 购买相关
* QQ28751976 国内/香港/韩国/美国服务器批发
* 有个叫楚狂人的软件做了近十年，有狂人系列营销软件
* 365建站网

## 忠告
一劳永逸是不行的。做站群的人大部分都喜欢偷懒，偷懒的人不会也不懂怎么做原创内容。缺乏原创内容的支撑，站群只能有一时的作用。更重要的是大量购买站群转软件的人都在用同一种方法不停的复制粘贴，并没有给互联网贡献新内容。那么无论如何躲避，百度K掉，也是合情合理的。
原创是关键，做站群还是得找好下手的目标站很重要，然后在这样的原创团队下持续盈利

## 博彩类网站SEO
有些接触，简单说几句。由于行业特殊性，只能点到即止，不能说得再具体了，能明白多少就明白多少，更深入的自己去研究吧。

菠菜类网站SEO目前常见方法包括：

新闻或企业网站CMS为主体，采集+关键词替换或插入，再加上JS跳转。这个是目前比较成功的方式。
镜像站点+关键词替换，加JS跳转。
正常页面，不跳转，JS+iFrame嵌入让用户看的内容。
泛解析高权重域名，或租用高权重域名的子域名，采集内容加JS跳转。
静态和动态寄生虫程序，生成大量页面。
需要收录大量页面时，如寄生虫程序，经常配合使用蜘蛛池。
需要提高域名权重时，如企业站形式，经常黑政府网站加黑链。
赌博行业SEO还有几个特点：

管用的方法在不停变动中，这个行业的SEO是比较努力又激进的。
能获得排名的网站也不停变动，被惩罚一批，再上一批，很少有能稳定排名的网站。
网站数量都是几百个为起点。
只能说这么多了。

## 简单地说，SEO日常工作至少包括：
* 你所说的建设外链。不是所谓的发外链，是靠内容吸引高质量外链。所以又会导致下一个工作。
* 创作高质量原创内容。这个要花的时间、精力是没有上限的。
* 大网站，调整网站结构，提高收录率。不要觉得网站已经建好了就意味着收录没问题。
* 发现新机会。可能来自检查流量统计，可能来自关键词研究，可能来自社会热点话题，可能来自竞争对手。
* 提高用户体验。检查流量后台，发现、分析问题，当然还要解决问题。
* 移动SEO做了没有？
* 社交媒体上的推广，包括各种自媒体号。
* 检查流量分析后台和百度资源平台或Google Search Console
## 站群的目的
站群的目的是建立强大的链接资源库，推动网站关键词排名上升，实现站群的最终目的从搜索引擎端获取到最大规模的流量，通过良好的商业模式，实现盈利。
## 站群的历史
* 2010年，淘宝客，淘宝广告联盟兴起，出现各种站群。
* 2011年，各种针对广告联盟的站群程序如雨后春笋涌现！
* 2012年，大概六月份，垃圾站群被重点打击。
* 2013年，新的操作方法出现，为原创内容组合+程序的方式
## 站群的分类
1. 端口站群，2013年4月份兴起，5月份被封杀，至今未翻身
2. 泛站群，如果网站权重高，流量就来的很快
3. 目录站群，可以自动采集内容，生成符合SEO规则的内容
4. 正规站群，流量稳定，不过操作的难度高
## 文章要求：  
1. 文章必须是有意义的。
2. 必须和网站的主题一致。
3. 是否能为用户提供到帮助。

## 站群互联
六边顺联 并指向主站.
站群现在最好是每个站ip不同，站的程序也要不同，站内文章的质量要高，现在百度对文章的原创度要求较高，而且百度识别技术也越来越强，站群也要向正规化开始发展！
靠团队管理和长尾流量来做战群是比较靠谱多，软件最好别用
很多公司都是用长尾词带来大多数流量，以内容为主攻方向，再加上渠道合作的方式

## 站群
1. 分科目做关键词，网站充分细分；
2. 可以借助与百度竞价提取优质的关键词
3. 原创（可以把最新的书籍提取，然后安排关键词+分段发布，每天3篇左右就够了）    +伪原创加关键词（黑帽）做法
4. 购买权重较高的行业二级域名做关键词覆盖
5. 可以做竞价推广页面经行精准长尾关键词覆盖
6. 发发外链，具体的优质外链地址可以参考(发外推网) 目前效果一般关键是持续去做，关键是内容一定要有质量，图长久，做优质站群！。

## 什么是站群
所谓站群，一般是指同一个用户组建多个的网站，而网站之间进行链接或者是广告调用的方式，提高网站的搜索引擎排名，来利于网站SEO优化，从而达到流量聚集，提升网站对搜索引擎的权重，通过产品或其他方式实现盈利的一中途径。

### 一、域名的选择
站群在域名上的关键在于选择老域名，而不是去注册全新的域名。可以到一些专门买卖域名的网站选择那些有一定权重，废弃没有多久的域名购买。

### 二、服务器的选择
于站群，因为都是垃圾站，对服务器的要求并不是很高。不过为了隐蔽站群，则要将站群IP尽可能的分散。对于我们做企业站为了养站而做的站群来说，因为站群的规模不会很大，建议直接只用虚拟空间即可。

### 三、站群的布局
网站数量问题没有具体的答案，要维护一个网站，五个站的小站群可以，一百个站的站群则更好，总归是多多益善。这里，以做一个100个网站的站群来说明一下。  
100个网站，可以以十个站为一组来建一个比较大型的站群。  
链接方式是：站群1组—>站群2组—>站群3组—>站群4组—5组—>6组—>7组—>8组—>9组—>10组—>1组.  
请注意这里是“组”，而不是简单的在组内互联，然后一起链接到主站。目前百度虽然说可以在一定程度上对站群做一个判断，但是还绝对没有办法判断十层链接的站群。另外，每一组网站里面， ` 要有七个站跟我们要推的主站高度相关，三个网站随便选择主题来做，将网站内再混淆一下 ` 。这是站群的一个基本的布局，具体的链接策略在下面详解。  

### 四、程序的选择与单站的建立修改
站群在程序的选择上以站群软件支持较好的程序为主，如dedecms、wordpress、zblog等，推荐使用365站群程序，dedecms二次开发，比dedecms本身功能更强大，方便。单站建立要分这么几步：
1. 、关键词的选择。
    站群普遍来说权重相对于正经做的网站来说权重要低一些，这也决定了站群网站不能选难度大的关键词。因此在关键词的选择上建议直接用`长尾关键词`。
    在数量上，每个网站选择三个左右关键词，布局方法：首页两个，栏目页一个（每一个网站设置四个栏目，这个关键词放在第一个栏目上）。
2. 、建立网站
    因为是站群，网站程序在修改上也没有必要像平时做网站优化一样处处到位，而且这些开源的程序在对搜索引擎的友好性上都不差，也没有必要针对seo修改太多，只要将关键的几个地方修改一下就ok了。
    * （1）logo的alt标签。将alt标签设置成为网站的关键词
    * （2）首页的title，keyword，description标签要认真填写一下。
    * （3）分类栏目的设置每个网站设置四个分类，其中A分类将关键词确定为选择的目标关键词，要认真写一下title，keyword，description
    * （4）网站静态化
    * （5）选择网站模版。在这一块上尽可能的做到所有的模版都不相同
    * （6）站内文章的调用。尽可能的让网站所有页面都要有一个最新文章板块和随机文章板块
    * （7）次导航：用选择的三个关键词作为连接词，链接到首页和相应的栏目页。另外，在每个程序在footer文件里面基本都有个版权之类的链接，顺便将这个链接一起去掉
    * （8）添加统计代码。为了衡量站群的效果，建议添加一个统一的统计代码。
    * （9）友情链接。各种程序都自己带着一部分友情链接，将这部分链接去掉。同时做自己网站的友情链接，具体链接方法在下面详解
3. 、添加网站到站群程序
    将做好的网站添加到站群程序里面，并设置好采集发布关键词等规则。以后就自动运行了。

### 五、站群链接策略做站群
如何在站与站之间相互链接，如何做主站的链接是最关键的一部分，我的链接策略如下：  
1. 、首页链接
    站群之间做链接，基本都是单向链接，具体单向链接是不是搜索引擎会当作购买的链接而惩罚尚不可知，不过根据搜索引擎的一些表现，似乎对单向链接有一定的措施。很明显的一个例子是：检索“斗破苍穹”等这些非常火爆的小说，排在首页的通常都不是首页，而是内容页面。做小说站的买链接都非常疯狂，百度这么处理的原因很可能就是：百度会对单向链接到首页太多的网站做一定程度的处理，而搜索引擎对于购买链接到内容页面的没有任何办法。现在，搜索斗破苍穹排前面的买的链接都是链到了内容页面。  
    所以我们做站群的首页链接的使用方法也是：用首页链接栏目页。  
    也就是：`站群1的友情链接是站群2的A栏目，站群2的友情链接是站群3的A栏目，依次类推，知道链接成为一个环路。`这样，每一个网站都是十个友情链接，而且都是栏目页。这样可以有效提高A栏目的权重，而不会导致搜索引擎的惩罚。
2. 、站内链接
    站内以“相关阅读”板块来做相互链接，都用标题来进行互联。每一篇文章都要有一个相关阅读板块，添加站内A栏目的文章。这个用软件可以实现。
3. 、站群链接
    站群之间的链接则用除A栏目以外的三个栏目来做。这部分链接添加到内容当中，以关键词为连接词，链接到相应的内容页面。链接方法即是站群的链接方法：站群1组—>站群2组—>站群3组—>站群4组—5组—>6组—>7组—>8组—>9组—>10组—>1组.但是，只做A栏目的链接（即：在软件提取链接的时候只提取A栏目的即可）。也就是说：站群1组十个网站的三个栏目发布的内容添加站群2组A栏目文章的关键词链接。总之，通过以上的链接策略来实现一个目的：将A栏目的权重做到最仅次于首页权重，甚至更高。
###* 六、养站链接策略站群
    不管做什么样的处理，在权重上总是相对低一些，因此，在养站上，不建议靠站群来做出高难度的关键词的排名，而是以养长尾关键词为主。  
    养站时，可以在这100个网站里面同时添加网站的关键词。也就是说，用这100个网站的站群同时养七个站，而不再做详细的细分。这就要求在做网站的时候详细的做好关键词记录单，来将链接添加到站群软件里面。同时，注意文章的发布数量，建议：每天一个网站的A栏目发布两三篇文章就可以了。

