# Data-analysis-and-mining
Study notes. Most notes come from the internet and book. Just do a summary.一位数据分析，数据挖掘师的成长笔记
# 目录
- [理论学习](#理论学习)
  - [一、数据分析理论](#数据分析理论)
  - [二、统计学理论](#统计学理论)
    - [1、基础知识](#基础知识)
    - [2、数据离散性](#离散性)
    - [3、概率计算](#概率计算)

- [方法学习](#方法学习)
  - [一、数据读取和存储](#数据读取和存储)
  - [二、数据的预览](#数据的预览)
  - [三、数据的清洗](#数据的清洗)
  - [四、list, ndarray, df, series等常用格式相互转换](#常用格式转换)
  - [五、python echarts画热力图(世界地图，省市地图，区县地图)](#地图热力图)
  - [六、数据的可视化](#数据的可视化)
  - [七、SQL笔记](#SQL笔记)
- [附录1、名词解释](#名词解释)
- [附录2、参考产品和思路](#参考产品和思路)
- [附录3、推荐资料汇总](#推荐资料)
# 理论学习
## 数据分析理论
### 1.分析流程
确定问题-->分解问题-->评估-->决策<br>

## 统计学理论
### 基础知识
+ 1.长方形面积代表频数<br>
+ 2.频数密度=频数/组距<br>
+ 3.均值(u,'谬')，中位数，众数<br>
### 离散性
+ 1.全距(极差)：
说明数据的离散程度；<br>
+ 2.四分位数，
四分位距= 上四分位数 - 下四分位数<br>
+ 3.异常值处理：
(1)构建迷你距，忽略异常值；(2)四分位距剔除异常值<br>
+ 4.箱线图：
显示数据的全距，四分位距和中位数<br>
+ 5.方差
方差=求和(x^2)/n - u^2 (化简公式，u为均值)<br>
+ 6.标准差('西格玛'):典型值与均值的距离，用于量度数据的分散性<br>
+ 7.标准分(z分):对不同数据集中的数值进行比较的一种方法，z=(x-u)/西格玛
### 概率计算
+ 1.P(A)=n(A)/n(S),
S为概率空间(样本空间)<br>
+ 2.韦恩图/概率树：
概率的图形表示；对立事件:P(A)+P(A')=1<br>
+ 3.概率只是对事件发生可能性的一种表达，概率并非担保<br>
 !!无论事件多么不可能发生，只要不是完全不可能发生，该事件就仍然可能发生。<br>
+ 4.概率相加的前提是:
相互独立<br>
+ 5.互斥事件，相交事件，交集n，并集U<br>
+ 6.P(AUB)=P(A)+P(B)-P(AnB)<br>
+ 7.条件概率:
P(A|B)=P(AnB)/P(B) <br>
+ 8.全概率公式(贝叶斯定理的分母):<br>
P(B)=P(A n B)+P(A' n B);P(A n B) = P(A) * P(B|A); P(A' n B)=P(A') * P(B|A')<br>
->得全概率公式:P(B)=P(A) * P(B|A) + P(A') * P(B|A')<br>
+ 9.贝叶斯定理:<br>
由P(A|B)=P(AnB)/P(B)<br>
和分子P(AnB) = P(A) * P(B|A)<br>
和全概率公式(分母):P(B)=P(A) * P(B|A) + P(A') * P(B|A')<br>
->得贝叶斯定理:P(A|B) = (P(A) * P(B|A)) / (P(A) * P(B|A) + P(A') * P(B|A'))<br>


# 方法学习
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

+ 替换
  + [正则表达式](https://docs.python.org/zh-cn/3/library/re.html)
```py
#1. df.replace(to_replace, value)
#这样会搜索整个DataFrame, 并将所有符合条件的元素全部替换。
#进行上述操作之后，其实原DataFrame是并没有改变的。改变的只是一个复制品。
df.replace('A',0.1)

#2.如果需要改变原数据，需要添加常用参数 inplace=True
df.replace('A',0.1,inplace=True)

#3.用列表/字典形式替换多个值。
data['parent_id'].replace([2,3],'2~3',inplace=True) #列表
df.replace({'C':1, 'D':2})#字典

#4.使用正则表达式替换多个(个人觉得在用于数字时不好用)
df.replace('[A-Z]',0.1,regex=True)

#5.批量替换数字
data.loc[data['parent_id'] > 200, 'parent_id'] = '>200' #筛选parent_id这一列，大于200的数替换为>200

#eg:
import pandas as pd
data = pd.read_excel(r'additem.xlsx')
#ps:在数据量大、sheet多的情况下，方式1的速度大于方式2的速度
data.loc[data['parent_id'] > 200, 'parent_id'] = '>200'
data['parent_id'].replace([2,3],'2~3',inplace=True)
data['parent_id'].replace([i for i in range(4,11)],'4~10',inplace=True)
data['parent_id'].replace([i for i in range(11,101)],'11~100',inplace=True)
data['parent_id'].replace([i for i in range(101,201)],'101~200',inplace=True)

print(data['parent_id'])

data.to_excel(r'new4.xlsx')  #存入D盘的data文件夹
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

## 常用格式转换
+ 1.list to others
```py
# list
data = [[2000, 'Ohino', 1.5],
        [2001, 'Ohino', 1.7]]  # type(data) 为 list

# (1).list to pandas.series, data对应list,index对于单列时，可以没有
import pandas as pd
ser = pd.Series(data, index = ['one', 'two'])
#单列数据拼接时：定义列名和数据
df['new_name']=ser

# (2).list to pandas.dataframe
df = pd.DataFrame(data, index = ['one', 'two'], columns = ['year', 'state', 'pop'])

# (3).list to numpy.ndarray
import numpy as np
ndarray = np.array(data)
```
+ 2.ndarray to others
```py
# (1).array to dataframe, index为索引，columns为列名
import pandas as pd
pdNum = pd.DataFrame(ndarray, index = ['one', 'two'], columns = ['year', 'state', 'pop'])

# (2).ndarray to list
import numpy as np
#定义一个numpy.ndarray
array=np.array([1,2,3,4,5,6])
#转为list
list=array.tolist()

```
+ 3.pd.DataFrame to others
```py
# dataframe
import pandas as pd
data = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['a', 'b', 'c'])

# (1).dataframe to array
arr = data.values

# (2).dataframe to dict 
dict = data.to_dict()

# (3).dataframe to list
train_data = np.array(data) #np.ndarray()
train_x_list=train_data.tolist() #list

```
+ 4.dict to others
```py
import numpy as np
import pandas as pd
from pandas import Series, DataFrame

# dict
data = { 'name': ['Li', 'Zhang', 'Wang'],
         'year': [2000, 2001, 2002]}  # type(data) 为 dict
         
# (1) dict to series
# 若不指定 index，data 的 key 充当 Series 的 index
ser = Series(data)
print('ser\n', ser)

# (2) dict to dataframe
# 若不指定 columns，data 的 key 充当 DataFrame 的 columns
df = DataFrame(data)
print('df\n', df)
```

## [地图热力图](https://www.xz577.com/j/40495.html)
+ 1.首先安装对应的python模块
```
$ pip install pyecharts==0.5.10
$ pip install echarts-countries-pypkg
$ pip install echarts-china-provinces-pypkg
$ pip install echarts-china-cities-pypkg
$ pip install echarts-china-counties-pypkg
$ pip install pyecharts-snapshot
```

+ 2.世界地图热力图
```py
from pyecharts import Map
 
value = [95.1, 23.2, 43.3, 66.4, 88.5]
attr = ["China", "Canada", "Brazil", "Russia", "United States"]
map0 = Map("世界地图示例", width=1200, height=600)
map0.add("世界地图", attr, value, maptype="world", is_visualmap=True, visual_text_color='#000')
map0.render(path="世界地图.html")
```

+ 3.中国地图热力图
```py
from pyecharts import Map
 
province_distribution = {'河南': 45.23, '北京': 37.56, '河北': 21, '辽宁': 12, '江西': 6, '上海': 20, '安徽': 10, '江苏': 16, '湖南': 9,'浙江': 13, '海南': 2, '广东': 22, '湖北': 8, '黑龙江': 11, '澳门': 1, '陕西': 11, '四川': 7, '内蒙古': 3, '重庆': 3,'云南': 6, '贵州': 2, '吉林': 3, '山西': 12, '山东': 11, '福建': 4, '青海': 1, '天津': 1,'其他': 1}
provice = list(province_distribution.keys())
values = list(province_distribution.values())
map = Map("中国地图", '中国地图', width=1200, height=600)
map.add("", provice, values, visual_range=[0, 50], maptype='china', is_visualmap=True,
  visual_text_color='#000')
map.render(path="中国地图.html")
```

+ 4.省市地图热力图
```py
from pyecharts import Map
 
map2 = Map("贵州地图", '贵州', width=1200, height=600)
city = ['贵阳市', '六盘水市', '遵义市', '安顺市', '毕节市', '铜仁市', '黔西南布依族苗族自治州', '黔东南苗族侗族自治州', '黔南布依族苗族自治州']
values2 = [1.07, 3.85, 6.38, 8.21, 2.53, 4.37, 9.38, 4.29, 6.1]
map2.add('贵州', city, values2, visual_range=[1, 10], maptype='贵州', is_visualmap=True, visual_text_color='#000')
 
map2.render(path="贵州地图.html")
```
+ 5.区县地图
```py
from pyecharts import Map
quxian = ['观山湖区', '云岩区', '南明区', '花溪区', '乌当区', '白云区', '修文县', '息烽县', '开阳县', '清镇市']
values3 = [3, 5, 7, 8, 2, 4, 7, 8, 2, 4]
 
map3 = Map("贵阳地图", "贵阳", width=1200, height=600)
map3.add("贵阳", quxian, values3, visual_range=[1, 10], maptype='贵阳', is_visualmap=True)
map3.render(path="贵阳地图.html")
```

+ 5.全国主要城市空气质量热力图
```py
from pyecharts import Geo
 
keys = ['上海', '北京', '合肥', '哈尔滨', '广州', '成都', '无锡', '杭州', '武汉', '深圳', '西安', '郑州', '重庆', '长沙', '贵阳', '乌鲁木齐']
values = [4.07, 1.85, 4.38, 2.21, 3.53, 4.37, 1.38, 4.29, 4.1, 1.31, 3.92, 4.47, 2.40, 3.60, 1.2, 3.7]
 
geo = Geo("全国主要城市空气质量热力图", "data from pm2.5", title_color="#fff",title_pos="left", width=1200, height=600,background_color='#404a59')
 
geo.add("空气质量热力图", keys, values, visual_range=[0, 5], type='effectScatter',visual_text_color="#fff", symbol_size=15,is_visualmap=True, is_roam=True) # type有scatter, effectScatter, heatmap三种模式可选，可根据自己的需求选择对应的图表模式
geo.render(path="全国主要城市空气质量热力图.html")
```
## 数据的可视化
python实现
+ 中文字体问题解决方法
```py
#1.查询matplotlib系统中文字体
from matplotlib.font_manager import fontManager
import os

fonts = [font.name for font in fontManager.ttflist if
         os.path.exists(font.fname) and os.stat(font.fname).st_size > 1e6]

for font in fonts:
    print(font)

#2.设置plot
# 中文乱码和坐标轴负号处理。
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['Heiti TC'] #用来正常显示中文标签, 这里Heiti TC为mac的黑体
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号
```

+ 直方图
```py
#eg1:横置直方图+随机展示
import matplotlib.pyplot as plt
import random

# 中文乱码和坐标轴负号处理。
plt.rcParams['font.sans-serif']=['Heiti TC'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号

city_name = [u'北京', u'上海', u'广州', u'深圳', u'成都']
city_name.reverse()

data = []
for i in range(len(city_name)):
    data.append(random.randint(100, 200))

colors = ['red', 'yellow', 'blue', 'green', 'gray']
colors.reverse()

plt.barh(range(len(data)), data, tick_label=city_name, color=colors)

# 不要X横坐标标签。
# plt.xticks(())

plt.show()
```

```py
#eg2:横置直方图+数据读取
import matplotlib.pyplot as plt
import pandas as pd
# 中文乱码和坐标轴负号处理。
plt.rcParams['font.sans-serif']=['Heiti TC'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号

data = pd.read_excel(r'data1.xlsx')
name = data['大洲'].tolist()
num = data['销量'].tolist()

plt.title(u'各州销量')
plt.xlabel(u'大洲')
plt.ylabel(u'销量')

plt.barh(range(len(num)), num, tick_label=name)

plt.show()
```
## SQL笔记
+ mysql的登陆方式
```sql
1.本地登录MySQL
命令：mysql -u root -p   //root是用户名，输入这条命令按回车键后系统会提示你输入密码

2.指定端口号登录MySQL数据库
将以上命令：mysql -u root -p改为 mysql -u root -p  -P 3306  即可，注意指定端口的字母P为大写，
而标识密码的p为小写。MySQL默认端口号为3306

3.指定IP地址和端口号登录MySQL数据库
命令格式为：mysql -h ip -u root -p -P 3306例如：mysql -h 127.0.0.1 -u root -p -P 3306
```

## 名词解释
+ [DNU](https://www.jianshu.com/p/3018da7b29cb)：Daily New User，日新增用户。
+ [DAU](https://www.zhihu.com/question/24007425):日活(Daily Active Users)，单日活跃用户量，反应产品短期用户活跃度
+ [MAU]:月活(Monthly Active Users)，单月活跃用户量，反应产品长期用户活跃度
+ [pv and uv](https://www.zhihu.com/question/20448467):
<br>UV(Unique visitor):一个人（记录身份证号） ;<br> PV(Page View):人次（只认次数，不认人）
+ [埋点](https://www.zhihu.com/question/36411025): 埋点捕获数据<br>
  埋点就是在应用中特定的流程收集一些信息，用来跟踪应用使用的状况，后续用来进一步优化产品或是提供运营的数据支撑<br>
  
+ [A/B测试](https://www.zhihu.com/question/20045543):通常会设置两个base组，多个exp组 
+ [GMV](https://en.wikipedia.org/wiki/Gross_merchandise_volume): Gross Merchandise Volume，是成交总额（一定时间段内）的意思。
+ [回流](https://www.zhihu.com/search?type=content&q=%E7%94%A8%E6%88%B7%E5%9B%9E%E6%B5%81%E8%A7%A3%E9%87%8A): 流失用户召回的一种叫法，也称“复活”、“唤醒”、“回流”等
+ [漏斗模型](https://zhuanlan.zhihu.com/p/29720621):是一个模型，更是一种可以普遍适用的方法论，或者说是一种思维方式
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
