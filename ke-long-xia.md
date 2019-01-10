## 操作步骤

## 域名
### 选老域名
1. https://tool.22.cn/
选择简短的域名（如：4个字母.cn)查询，会显示可注册的域名，导出结果。
2. 在link114.cn批量查询在百度、搜狗、360、神马上的收录情况，有收录的不要
3. 批量过滤在（http://web.archive.org/）没有历史记录的域名
4. 在（http://web.archive.org/）上一个个手到查询具体的网站历史记录，删除有色情、菠菜等历史的域名
### 注册域名
批量注册域名，在西部数码可以离线批量注册，价格可与客服咨询。
### 批量解析
下载好解析模板，可以多个（二级）域名解析到同一个ip。

## 模板
###  选模板
1. 搜索行业关键词，比如，扫地机器人，托福考试。排名靠前的网站。
2. 搜索到的网站，查询一下收录情况，收录不能太多。权重也不能太高，知名的网站不要，最好有几十条几百条收录就行。
3. 尽量选择代码不变的自适应模板，可适应手机端展示，提高百度移动排名
### 下载模板（克隆网站）
使用wget下载，软件下载地址是：https://eternallybored.org/misc/wget/releases/wget-1.20-win64.zip 

```shell
cd wget
wget -r -p -k -np -nc -e robots=off https://www.domain.com/m/

wget -p -A "*.jpg,*.png,*.gif,*.css,*.js" 

wget -k -p -P download www.zhuoyuesc.com
wget -e robots=off -k -p -P download 
```
### 模板处理
```html
<!DOCTYPE HTML>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <title><转码主词></title>
    <link href="http://<当前域名>/" rel="canonical" />
    <meta name="keywords" content="<转码主词>">
    <meta name="description" content="<首页描述>" />
    <meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=no" />


</head>
<body>
    <div style="position:fixed;left:-9000px;top:-9000px;"><干扰段></div>
```
> 注意：首页描述可加入统一的一个特殊符号，以便在百度查排名展示时，更容易识别。
* 替换 href
* 替换 域名
* href="http://m.<顶级域名>/" 
* href="http://wap.<顶级域名>/" 
* href="http://www.<顶级域名>/" 
* href="http://<顶级域名>/" 
* <转码主词>
* <首页主词>
* <顶级域名>

## 关键词
### 筛选关键词
* 查找百度相关搜索、下拉框索的词
    > https://www.5118.com/seo/search/word 
* 人工删除一下不合适的词
### 二次筛选
用百度搜索预选词，看一下搜索结果，判断词的价值和可排名性
### 关键词分组
两个相关的词分布在一个title，用_,-|等分开   