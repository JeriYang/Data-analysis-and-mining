# Data-analysis-and-mining
Study notes. Most notes come from the internet. Just do a summary.
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
+ DAU:
+ UV: ; PV:
+ 埋点: 埋点捕获数据
+ AB测试: 
+ GMV: 
+ 回流: 
+ 漏斗模型:
+ 异动归因:
+ [拆分法（以及常用的方法)](https://zhuanlan.zhihu.com/p/52279855)
+ [Cvr转化率](https://baike.baidu.com/item/CVR/20215345)
+ ROI:
+ 成本利润率:
+ 销售利润率:
+ 投资回报率:
+ dpa:

## 参考产品和思路
+ 常见流程：
  1.看数->报表->分析
  
+ 分析思路:
  1.判断，定位，原因
  2.经营分析中注意：去节假日，去峰值，去活动日

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
