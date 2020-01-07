# Data-analysis-and-mining
Study notes. Most notes come from the internet. Just do a summary.一位数据分析，数据挖掘师的成长笔记
# 目录

- [一、数据读取和存储](#数据读取和存储)
- [二、数据的预览](#数据的预览)
- [三、数据的清洗](#数据的清洗)
- [附录1、名词解释](#名词解释)
- [附录2、参考产品和思路](#参考产品和思路)
- [附录3、推荐资料汇总](#推荐资料)

## 数据读取和存储
### 1.数据读取
+ 方式1：
```py
import pandas as pd
io = pd.io.excel.ExcelFile(r'D:\data\python\amazon_data.xlsx')
amazon_data = pd.read_excel(io,sheet_name='data')
price = pd.read_excel(io,sheet_name='price')
io.close()
``` 
+ 方式2：
```py
import pandas as pd
amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheet_name='data')
price = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheet_name='price')
#ps:在数据量大、sheet多的情况下，方式1的速度大于方式2的速度
```

### 2.数据存储
+ 方式1:
```py
import pandas as pd
amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheet_name='data')
amazon_data.to_excel(r'D:\data\new.xlsx')  #存入D盘的data文件夹
```

+ 方式2: 如果是多个表需要输出，且输出到一个Excel的不同sheet
```py
import pandas as pd
writer=pd.ExcelWriter(r'D:\data\python\存储数据.xlsx')
amazon_data .to_excel(writer,sheet_name='data')
price.to_excel(writer,sheet_name='price')
writer.save()
```

## 数据的预览
```py
import pandas as pd
amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheet_name='data')
```
+ 查看列名：amazon_data.columns
+ 查看行数列数：amazon_data.shape
+ 查看前5行/后5行数据： amazon_data.head(5)、amazon_data.tail(5)
+ 查看每列的数据格式：amazon_data.dtypes
+ 数据的索引：
  + 列的索引：amazon_data['Id']或者amazon_data.loc[:, 'Id'] 数据ID列
  + 行的索引：amazon_data.loc[0, :] 读取第1行（Python的索引从0开始）
  + 某行某列：amazon_data.loc[2, 'Id'] ID列的第3个
  + 扩展
    + 物理位置索引 amazon_data.iloc[ ]
    + 第3行第5列，可以写 amazon_data.iloc[ 2, 4 ]，注意索引都是从0开始的
    + 多行多列，可用 amazon_data.iloc[ 2:8, 1:3]，[python切片](https://blog.csdn.net/slvher/article/details/44703185)
+ 数据描述：amazon_data.describe()
  + 包含了每一列的个数、均值、方差、最小值、最大值、分位数。如果查看某一列的，可以加上列的索引：amazon_data['Id'].describe()
+ 数据信息：amazon_data.info()   包含了每一列的个数、有无空值、数据格式、内存大小

## 数据的清洗
格式修改、去除空格、替换、分列、合并
+ 字符串格式→日期格式
```py
#导入库
import datetime
import pandas as pd
#读取数据
amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheetname='data')
price = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheetname='price')

#数据清洗
#字符串转日期
amazon_data.loc[:,'日期date'] 
= amazon_data['Time'].apply(lambda x: datetime.datetime.strptime(x,'%Y/%m/%d %H:%M')) 
```
+ 去除空格
```py
#去除空格
amazon_data.loc[:,'ProfileName无空格'] = amazon_data['ProfileName'].str.replace(' ','')

#方法2:
amazon_data['ProfileName'].str.strip(' ')
```
+ 分列
```py
#数据分列
amazon_data.loc[:,'ProfileName分列'] = amazon_data['ProfileName'].str.split(' ').str[0]
```

+ 合并
```py
#合并
amazon_data = pd.merge(left=amazon_data,right=price,on='ProductId')
#pd.merge(left=df1, right=df2, left_on=’key1’, right_on=’key2’, how=’left’)

#left左表，right右表，left_on左表的连接键，right_on右表连接键，
#how是连接方式：左连left，右连right，外连outer，内连inner（默认）。
```
  合并表格，除了用merge，还有个方法是concat。concat可以纵向合并，也可以横向合并。
  <br>
  pd.concat([df1, df2] ) 纵向合并，即把df2的数据接到df1后面。
  <br>
  pd.concat([df1, df2], axis=1, join='inner') 横向合并，按索引取交集。


## 名词解释
+ [DAU](https://www.zhihu.com/question/24007425):日活(Daily Active Users)，单日活跃用户量，反应产品短期用户活跃度
+ [MAU]:月活(Monthly Active Users)，单月活跃用户量，反应产品长期用户活跃度
+ [pv and uv](https://www.zhihu.com/question/20448467):
<br>UV(Unique visitor):一个人（记录身份证号） ;<br> PV(Page View):人次（只认次数，不认人）
+ [埋点](https://www.zhihu.com/question/36411025): 埋点捕获数据<br>
  埋点就是在应用中特定的流程收集一些信息，用来跟踪应用使用的状况，后续用来进一步优化产品或是提供运营的数据支撑<br>
  
+ [A/B测试](https://www.zhihu.com/question/20045543):通常会设置两个base组，多个exp组 
+ [GMV](https://en.wikipedia.org/wiki/Gross_merchandise_volume): Gross Merchandise Volume，是成交总额（一定时间段内）的意思。
+ 回流: 
+ 漏斗模型:
+ [异动归因](https://zhuanlan.zhihu.com/p/37530954):
  + 1. 启发式归因
    <br>顾名思义，启发式归因主要起启发作用，是一种快速分析方法。它使用简单的算法，计算各个触点、渠道对转化的贡献度。
  + 2. 算法归因
    <br>利用统计或者机器学习方法分析各个触点对最终转化的影响程度。
    <br>与启发式归因相比，它更加客观，不受到使用者偏好的影响。
    <br>常见的算法有logistics回归、生存模型、probabilistic模型、markov模型等。
+ OR值
+ RR值
+ PAR
+ PAF
+ [拆分法（以及常用的方法)](https://zhuanlan.zhihu.com/p/52279855)
+ [Cvr转化率](https://baike.baidu.com/item/CVR/20215345)
+ ROI:
+ 成本利润率:
+ 销售利润率:
+ 投资回报率:
+ DPA:
+ OKR:
+ BI:

## 参考产品和思路
+ 常见流程：<br>
  1.看数->报表->分析<br>
  
+ 分析思路:<br>
  1.判断，定位，原因<br>
  2.经营分析中注意：去节假日，去峰值，去活动日<br>

+ 数据产品2019末更新:
  + 观星台
  + 驾驶舱
  + 浑天仪
  + 业务参谋
  + 零售通运营罗盘
  + 鹰眼
  + 黄金策
  + 嵌入业务中台
  + BI分析师 
  + 部门OKR

+ 数据产品岗位分类:
  + 工具类:通用性强，自助报表，流量分析，天花板比较低
  + 业务类:深度结合业务，生意参谋，商家诊断，营销活动分析，
  + 产品架构类：非常熟悉业务

## 推荐资料
+ 书籍：
  + 1.《深入浅出数据分析》-head first
  + 2.《深入浅出统计学》-head first
