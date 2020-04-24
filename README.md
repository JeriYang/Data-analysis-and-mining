# Data-analysis-and-mining
Study notes. Most notes come from the internet and book. Just do a summary.数据分析，数据挖掘相关
# 目录
- [理论学习](#理论学习)
  - [一、数据分析理论](#数据分析理论)
  - [二、统计学理论](#统计学理论)
    - [1、基础知识](#基础知识)
    - [2、数据离散性](#离散性)
    - [3、概率计算](#概率计算)
    - [4、期望笔记](#期望笔记)
    - [5、几何分布，二项分布，泊松分布](#离散概率分布)
    - [6、正态分布](#连续型概率分布)

- [方法学习](#方法学习)
  - [一、数据读取和存储](#数据读取和存储)
  - [二、数据的预览](#数据的预览)
  - [三、数据的清洗](#数据的清洗)
  - [四、数据的可视化](#数据的可视化)
  - [五、SQL笔记](#SQL笔记)
    - [1、mysql的登陆方式](#mysql的登陆方式)
    - [2、SQL必会列表](#SQL必会列表)
    - [3、SQL必会内容](#SQL必会内容)
  - [六、Python学习笔记](#Python学习笔记)
    - [1、python排序，保留索引值](#python保留索引值排序)
    - [2、list, ndarray, df, series等常用格式相互转换](#常用格式转换)
    - [3、python echarts画热力图(世界地图，省市地图，区县地图)](#地图热力图)
    - [4、Python 几种取整的方法](#取整方法)
  - [七、大数据笔记](#大数据学习笔记)
    - [1、Hadoop生态](#Hadoop生态)
    - [2、Hadoop中涉及的排序](#Hadoop排序)
    - [3、Spark(内存分布式计算)](#Spark)
    - [4、HDFS（hadoop分布式文件系统）](#HDFS)
    - [5、MapReduce（分布式计算框架）](#MapReduce)
    - [6、Hive（基于hadoop的数据仓库）](#Hive)
    - [7、Hbase（分布式列存数据库）](#Hbase)
  - [八、大数据框架简介](#大数据框架简介)
    - [1、著名框架汇总](#著名框架汇总)
    - [2、Hadoop框架](#Hadoop框架)
    - [3、Spark框架](#Spark框架)
    - [4、分布式列存储框架](#分布式列存储框架)
    - [5、PrestoDB_CLI](#PrestoDB_CLI)
    
  
- [附录1、名词解释](#名词解释)
- [附录2、参考产品和思路](#参考产品和思路)
- [附录3、推荐资料汇总(附下载链接o)](#推荐资料)
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
方差=求和(x<sup>2</sup>)/n - u<sup>2</sup> (化简公式，u为均值)<br>
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
+ 10.独立性:<br>
如果A,B两事件独立，有以下:<br>
P(A|B) = P(A); P(A n B)=P(A) * P(B);<br>

### 期望笔记
+ 1.期望E(x)=求和xP(X=x)
+ 2.期望方差Var(x)=E(x-u)<sup>2</sup>
+ 3.通用公式:<br>
E(aX+b)=aE(X) + b<br>
Var(aX+b) = a<sup>2</sup>Var(X)<br>
+ 4.排列组合:<br>
<img src="https://github.com/JeriYang/Data-analysis-and-mining/blob/master/img/arrange_comb.png" alt="img1" title="jery_img1" width="600" height="300" />

### 离散概率分布
+ 1.几何分布:<br>
  + 应用条件:
    + (1)相互独立 
    + (2)每次试验都有成功、失败的可能，且每次试验概率相等 
    + (3)关注点为取得一次成功需进行多少次试验
    + 结论:任何几何分布的众数永远为1
  + 如果符合几何分布的条件，那么用X表示为了取得第一次成功需要试验的次数，用p代表单次试验成功的概率(q为失败概率):
    + X ~ Geo(p)
  + 如果 X ~ Geo(p) ,则下列概率算式成立:
    + P(X=r)=q<sup>(r-1)</sup> * p<sup>1</sup>
    + P(X>r)=q<sup>(r)</sup>
    + P(X<r)=1 - q<sup>(r)</sup>
  + 如果 X ~ Geo(p) ,则:
    + E(X) = 1/p
    + Var(X) = q/p<sup>2</sup>

+ 2.二项分布:<br>
  + 应用条件:
    + 条件(1)(2)同几何分布 
    + (3)关注点为在n次试验中能成功多少次
  + 如果符合二项分布的条件，那么用X表示n次试验中成功的次数，用p代表单次试验成功的概率(q为失败概率):
    + X ~ B(n,p)
  + 如果 X ~ B(n,p) ,则下列概率算式成立:
    + P(X=r)=<sup>n</sup>C<sub>r</sub> * p<sup>r</sup> * q<sup>n-r</sup>
    + 其中: <sup>n</sup>C<sub>r</sub> = n!/(r!(n-r)!)
  + 如果 X ~ B(n,p) ,则:
    + E(X) = np
    + Var(X) = npq
    
+ 3.泊松分布:<br>
  + 应用条件:<br>
    + (1)单独事件在给定区域内随机，独立的发生，给定区间可以是时间或者空间，例如可以是一个星期，也可以是一英里
    + (2)已知该区间内的事件平均发生次数(发生率)，且为有限数值。通常用lambda(希腊字母λ)表示
    + (3)关注点为给定区间的事件发生次数
  + 如果符合柏松分布的条件，那么用X表示给定区间内事件发生的次数，用λ代表发生率，则:
    + X ~ Po(λ)
  + 如果 X ~ Po(λ), 则:
    + P(X=r)= (e<sup>-λ</sup> * λ<sup>r</sup>) / (r!)
    + E(X) = λ
    + Var(X) = λ
  + 如果 X ~ Po(λx), 如果 Y ~ Po(λy), 且X,Y是相互独立的，则:
    + X + Y ～ Po(λ<sub>x</sub> + λ<sub>y</sub>)
  + 如果 X ~ B(n,p) ,其中n足够大,p足够小, 则可将该分布近似看作X ~ Po(np)

### 连续型概率分布
+ 1.正态分布概念
  + X ～ N(μ, σ<sup>2</sup>)
  + μ指出曲线的中央位置，σ<sup>2</sup>指出分散性。在实践中，σ<sup>2</sup>越大，正态分布的曲线越扁平，越宽。


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
### mysql的登陆方式
```sql
1.本地登录MySQL
命令：mysql -u root -p   //root是用户名，输入这条命令按回车键后系统会提示你输入密码

2.指定端口号登录MySQL数据库
将以上命令：mysql -u root -p改为 mysql -u root -p  -P 3306  即可，注意指定端口的字母P为大写，
而标识密码的p为小写。MySQL默认端口号为3306

3.指定IP地址和端口号登录MySQL数据库
命令格式为：mysql -h ip -u root -p -P 3306例如：mysql -h 127.0.0.1 -u root -p -P 3306
```
### SQL必会列表
+ [知乎参考链接](https://zhuanlan.zhihu.com/p/61805956)
+ (1)基础：
  + select 选择
  + join/ left join/ right join/ union 表连接
+ (2)最常用:
  + distinct 去重
  + having/ where 筛选
  + max/ min/sum/ count + group by 聚合
  + order by/ sort by 排序
  + case when...  end 条件
  + substr/ concat/ split 字符串
+ (3)进阶:
  + to_date/ datediff() 日期函数
  + row_number() 分组函数
  + percentitle 取百分比

### SQL必会内容
+ 1.基础:
  + hive的join 默认为inner join(左右表均可匹配的记录)
  + left join: 左连接，以左表为准，补NULL
  + right join: 右连接，以右表为准，补NULL
  + full outer join: 全连接，左右补NULL，保留所有
  + union和union all均基于列合并多张表数据，
    + union 会去重，效率较低；
    + union all 直接追加(无特殊情况用union all)
+ 2.常用:
  + Distinct和Groub by原理比较:
    + Distinct原理：将全部内容存储在一个hash结构里，最后通过计算hash结构中key的个数得到结果（空间换时间）
    + Group by原理：排序(时间换空间)
    + 数据离散时，使用Group by，集中时使用Distinct
  + Where子句在聚合前先筛选记录（即where在group by 和 having子句前）；having在聚合后再使用
  + LIMIT限制行，DESC 降序，ASC升序
  + CASE WHEN 条件1 THEN value1 ELSE NULL END（其中else可省，end不可省）
  + CAST用法：常用于String/ int/ double型的转换
  + 了解concat(A,B);substr(str,0,len)等用法：合并字符，截取字符串从0开始长为len的字符
+ 3.进阶:
  + 排序:
    + rank()
    + dense_rank()
    + row_number()
    + eg: SELECT *, row_number() over (partition by deptid order by salary DESC) as rank from table
      <br> 按deptid分组，再按salary倒序编号
  + 百分比:
    + Hive的percentile(col,p) col为int, p取0-1之间的小数
    + 中位数: percentile_approx(hot_page_photo_play_cnt,0.5)   分位数；跑多个分位数时加arra
  + 时间:
    + to_date 时间字符串->时间类型
    + datediff() 以天为单位，计算差值
    + 常见时间提取函数year()/ month()/ day()/ hour()/ minute()/ second()
+ 4.数据库SQL调优的方式总结:
  + 1)创建索引
  + 2)避免在索引上进行计算
    + where salary > 11000/22 性能高于 salary*22 > 11000
  + 3)使用预编译查询
    + 对查询语句进行查询优化
  + 4)调整where子句中对顺序，表连接在where之前
  + 5)尽量将多条SQL语句压缩到一句SQL
  + 6)多有where，少用having
  + 7)使用表对别名
  + 8)union all 替换 union
  + 9)使用 临时表 暂存结果
  + 10)[避免全表扫描](https://blog.csdn.net/illusion_you/article/details/79097287):
    + 模糊查询 like
    + 查询条件中含有is null的select语句
    + 查询条件中使用了不等于操作符（<>、!=）的select语句
    + or语句使用不当会引起全表扫描
    + 使用组合索引，如果查询条件中没有前导列，那么索引不起作用，会引起全表扫描

## Python学习笔记
### python保留索引值排序
```py
# 比如对a = [3,4,1,7,2]用a.sort()排序得到a = [1,2,3,4,7]，请问如何得到排序后的
# 数组元素的索引系列，是说，在原来数组中的索引。
# 在这个例子里应该是[2,4,0,1,3].

# 方法1:稳定排序，效率较低
In [1]: a = [3,4,1,7,2]

In [2]: enumerate(a)
Out[2]: <enumerate object at 0x8591f0c>

In [3]: list(enumerate(a))
Out[3]: [(0, 3), (1, 4), (2, 1), (3, 7), (4, 2)]

In [4]: from operator import itemgetter

In [5]: sorted(enumerate(a), key=itemgetter(1))
Out[5]: [(2, 1), (4, 2), (0, 3), (1, 4), (3, 7)]

In [6]: [index for index, value in sorted(enumerate(a), key=itemgetter(1))]
Out[6]: [2, 4, 0, 1, 3]

# 方法2： 不稳定排序
In [7]: import numpy as np

In [8]: np.argsort([3,4,1,7,2])
Out[8]: array([2, 4, 0, 1, 3])

# 方法3:稳定排序，效率最高，仔细理解
n = len(a)
li = sorted(range(n),key=lambda i: a[i]) #排序[0,n),0对应a[0]
```
### 常用格式转换
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
### 取整方法
1、向下取整<br>
向下取整直接用内建的 int() 函数即可：<br>
```py
>>> a = 3.75
>>> int(a)
3
```

2、四舍五入<br>
对数字进行四舍五入用 round() 函数：<br>
```py
>>> round(3.25); round(4.85)
3.0
5.0
```

3、向上取整<br>
向上取整需要用到 math 模块中的 ceil() 方法:<br>
```py
>>> import math
>>> math.ceil(3.25)
4.0
>>> math.ceil(3.75)
4.0
>>> math.ceil(4.85)
5.0
```

4、分别取整数部分和小数部分
用 math 模块中的 modf() 方法，该方法返回一个包含小数部分和整数部分的元组：<br>
存在浮点精度问题<br>
```py
>>> import math
>>> math.modf(3.25)
(0.25, 3.0)
>>> math.modf(3.75)
(0.75, 3.0)
>>> math.modf(4.2)
(0.20000000000000018, 4.0)
```

### [地图热力图](https://www.xz577.com/j/40495.html)
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
## 大数据学习笔记
### Hadoop生态
+ 大数据分类
  + 批式大数据(bath):历史大数据
  + 流式大数据(streaming):实时大数据
+ 相关知识
  + 三驾马车:HDFS, MapReduce, Hbase
  + Spark Streaming: 是构建在SPark基础之上的流式大数据框架，类似的有storm, Flink
+ 组成:
  + Ambari(安装、部署、配置和管理工具)
  + Zoo keeper(分布式协作服务)
  + Hbase(实时分布式数据库)
  + Hive(数据仓库)
  + Pig(数据流处理)
  + Mahout(数据挖掘库)
  + Flume(日志收集工具)
  + MapReduce(分布式计算框架)
  + HDFS(分布式文件系统)
  + Sqoop(数据库ETL工具)
+ 重点:
  + (1)HDFS:
    + Client: 切分文件
    + NameNode
    + DataNode
    + Secondary NameNode
  + (2) MapReduce:
    + Map端: 输入数据分片之后，每一个节点会对应一个Map任务
    + Reduce端: 将不同节点的map结果进行合并
  + (3) Hbase特点:
    + 大
    + 无模式
    + 面向列
    + 稀疏
    + 数据多版本
    + 数据类型单一，均为string

### Hadoop排序(MapReduce)
+ Map Task: n快排->归并
  + 环形缓冲区--(达到阈值)-->快速排序---->放入磁盘--(处理结束，归并排序)-->结束
+ Reduce Task: n归并->归并
  + 环形缓冲区--(达到阈值)-->放入磁盘--(达到阈值)-->归并排序合成一个更大的文件--(数据拷贝完后)-->对内存磁盘所有数据进行一次归并
  
### Spark
+ 内存分布式计算，读取比磁盘IO流对Hadoop快100倍
+ Hadoop为离线计算，Spark为实时计算
+ Spark core(调度中心):
  + 包括任务调动，内存管理，容错管理及存储管理
  + 包括:
    + 有向无环图DAG对分布式并行计算框架
    + 容错分式数据RDD
+ pyspark使用:
  + (1)导包 import
  + (2)配置conf SparkConf
  + (3)会话 sc:SparkContent
  + (4)sc.stop

### HDFS
（hadoop分布式文件系统）是hadoop体系中数据存储管理的基础。他是一个高度容错的系统，能检测和应对硬件故障。
+ client：
  + 切分文件，访问HDFS，与那么弄得交互，获取文件位置信息，与DataNode交互，读取和写入数据。
+ namenode：
  + master节点，在hadoop1.x中只有一个，管理HDFS的名称空间和数据块映射信息，配置副本策略，处理客户 端请求。
+ DataNode：
  + slave节点，存储实际的数据，汇报存储信息给namenode。
+ secondary namenode：
  + 辅助namenode，分担其工作量：定期合并fsimage和fsedits，推送给namenode；紧急情况下和辅助恢复namenode，但其并非namenode的热备。
+ [学习链接](https://zhuanlan.zhihu.com/p/21249592)
+ HDFS存储文件原理: 分片冗余，本地校验，协同校验纠错。
+ HDFS和文件系统相似，用fsck指令可以显示块信息:% hadoop fsck / -files -blocks
+ 没有namenode，文件系统会崩溃。解决方案：(1).远程备份 (2).本地备份，运行一个备用的namenode
+ 常用命令：
```
本地文件复制：  %hadoop fs -copyFromLocal localFile.dir hdfs.dir
在HDFS创建目录：%hadoop fs -mkdir name.dir
在HDFS查看目录：%hadoop fs -ls name.dir
在HDFS删除目录：%hadoop fs -r mr name.dir
```

### MapReduce
（分布式计算框架）
mapreduce是一种计算模型，用于处理大数据量的计算。其中map对应数据集上的独立元素进行指定的操作，生成键-值对形式中间，reduce则对中间结果中相同的键的所有值进行规约，以得到最终结果。

+ jobtracker：
  + master节点，只有一个，管理所有作业，任务/作业的监控，错误处理等，将任务分解成一系列任务，并分派给tasktracker。
+ tacktracker：
  + slave节点，运行 map task和reducetask；并与jobtracker交互，汇报任务状态。
+ map task：
  + 解析每条数据记录，传递给用户编写的map（）并执行，将输出结果写入到本地磁盘（如果为map—only作业，则直接写入HDFS）。
+ reduce task：
  + 从map 它深刻地执行结果中，远程读取输入数据，对数据进行排序，将数据分组传递给用户编写的reduce函数执行。
+ [学习链接1](https://zhuanlan.zhihu.com/p/78542030)
+ [学习链接2](https://zhuanlan.zhihu.com/p/55884610)
+ Input Split 或 Read 数据阶段(切片)
  + 如何优化小文件切片问题：
    + 最好的办法：在数据处理系统的最前端（预处理、采集），就将小文件先进行合并了，再传到 HDFS 中去。
    + 补救措施：如果已经存在大量的小文件在HDFS中了，可以使用另一种 InputFormat 组件CombineFileInputFormat 去解决，它的切片方式跟 TextInputFormat 不同，它会将多个小文件从逻辑上规划到一个切片中，这样，多个小文件就可以交给一个 Map 任务去处理了。
+ Map阶段
+ Shuffle 阶段
+ Reduce 阶段
+ Output 阶段
### Hive
（基于hadoop的数据仓库）
由Facebook开源，最初用于解决海量结构化的日志数据统计问题。<br>
hive定于了一种类似sql的查询语言（hql）将sql转化为mapreduce任务在hadoop上执行。
+ 数据库与数据仓库的区别对比: [参考知乎链接](https://www.zhihu.com/question/20623931)
  + 数据库：MySQL, Oracle, SqlServer等
    + 传统的关系型数据库的主要应用，主要是基本的、日常的事务处理，例如银行交易。
  + 数据仓库：AWS Redshift, Greenplum, Hive等
    + 数据仓库系统的主要应用主要是OLAP（On-Line Analytical Processing），支持复杂的分析操作，侧重决策支持，并且提供直观易懂的查询结果。
+ [Hive体系架构](https://blog.csdn.net/zhoudaxia/article/details/8855937)
+ Hive特点： 
  + (0)Hive构建在Hadoop之上，
  + (1)HQL中对查询语句的解释、优化、生成查询计划是由Hive完成的
  + (2)所有的数据都是存储在Hadoop中
  + (3)查询计划被转化为MapReduce任务，在Hadoop中执行（有些查询没有MR任务，如：select * from table）
  + (4)Hadoop和Hive都是用UTF-8编码的

### Hbase
（分布式列存数据库）
hbase是一个针对结构化数据的可伸缩，高可靠，高性能，分布式和面向列的动态模式数据库。和传统关系型数据库不同，hbase采用了bigtable的数据模型：增强了稀疏排序映射表（key/value）。其中，键由行关键字，列关键字和时间戳构成，hbase提供了对大规模数据的随机，实时读写访问，同时，hbase中保存的数据可以使用mapreduce来处理，它将数据存储和并行计算完美结合在一起。

## 大数据框架简介
### 著名框架汇总
+ 分类：
  + 大数据计算框架
  + 大数据存储框架
+ 大数据计算框架：
  + 一类是执行一次就结束的、对计算时间要求不高的离线计算框架
    + 离线计算多用于模型的训练和数据的预处理，最经典的就是Hadoop的MapReduce
  + 另一种是对处理时间有严格要求的实时计算框架
    + 实时计算框架要求立即返回计算结果，快速响应请求，如Storm、Spark Streaming框架。
    + 其多用于简单的累加计数和基于训练好的模型进行分类等操作
+ 大数据存储框架：
  + 经典的Hadoop的HDFS就具备了动态扩容以及冗余化存储（存储多份数据）的能力。
  + 这保证了数据源增大时，用户仍然可以像操作本地磁盘一样操作HDFS,又可以保证计算结果的安全性，它是大数据存储中最主流的解决方法之一。
### Hadoop框架
一般把Hadoop Common、HDFS、YARN、MapReduce这四部分成为Hadoop框架。<br/>
除此之外，还有进行SQL化管理HDFS的Hive组件，支持OLTP(支持短时间内大量并发的小型操作（增删改查）能力)业务的NoSQL分布式数据库HBase组件，
进行图形界面管理的Ambari组件等。
+ Hadoop2.0 核心框架部分
  + (1) Hadoop Common
    + 这是Hadoop的核心功能，是对其他的Hadoop模块做支撑的，里面包含了大量的对底层文件、网络访问、对数据类型的支持、以及对象的序列化、反序列化操作的支持等。
  + (2) Hadoop Distributed File System(HDFS)
    + Hadoop 分布式文件系统，用于存储大量的数据。
  + (3) Hadoop YARN
    + 一个任务调度和资源管理的框架。
  + (4) Hadoop MapReduce
    + 基于YARN的并行大数据处理组件。
+ Hadoop1.0和2.0的区别：
  + 1.0环境的MapReduce是直接运行的
  + 2.0环境的MapReduce依赖于YARN框架，在YARN框架启动后，MapReduce在需要运行的时候把任务提交给YARN框架，让YARN框架来分配资源择机运行。
+ MapReduce原理<br/>
MapReduce是解决问题并行任务的一种模型，将一个可拆解的任务分散到多个计算节点进行计算，最后合并计算结果。
  + 流程：
    + 输入文件——>Map——>中间结果——>Reduce——>结果
  + Map处理过程：
    + 第一步：读取输入文件
    + 第二步：输出构造一个key-value文件(这一步很重要，大部分逻辑在Reduce中完成，所以在Map的部分实际要完成对Reduce操作内容的迎合性构造，让Reduce能够处理以Key-Value对形成的文件内容)
  + Reduce处理过程：
    + 第一步：读入中间结果的文件
    + 第二步：对一个Key的文本部分进行处理(不同的key通常会被分给不同的Reduce程序实例处理)
    + 第三步：合并输出结果，输出到结果文件

### Spark框架
Spark框架是一个快速且API丰富的内存计算框架。Spark采用Scala语言编写，Scala是基于JVM的语言，性能开销小。<br/>
在Spark中，一切计算都是基于[RDD](http://www.meicx.com/?p=8336)句柄(Resilient Distributed Dataset 弹性分布式数据集，是Spark中的基本抽象)来进行操作的。RDD就像一个数据容器，可以有输入口，可以有输出口。<br/>
在内存中，Spark使用[Tachyon](https://www.cnblogs.com/brucemengbm/p/7072531.html)——一种类似于内存中的HDFS的内存分布式存储框架，这样使得读写速度有了极大的提升。

### 分布式列存储框架
### PrestoDB_CLI

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
+ OR值: odds ratio
+ RR值: relative risk
+ PAR: Population Attributable Risk
+ PAF: Population Attributable Fraction
+ [拆分法（以及常用的方法)](https://zhuanlan.zhihu.com/p/52279855)
+ [Cvr转化率](https://baike.baidu.com/item/CVR/20215345)
+ ROI: Return On Investment, 是指通过投资而应返回的价值，即企业从一项投资活动中得到的经济回报，通俗点来说就是我们获得的收益和投入成本的比值。
  + ROI投资回报率：投资回报率）ROI=［（收入－成本）／投入］＊100% ，它表达的意思其实是ROI=收回价值 / 成本投入 *100%
  + 很多人会误认为这里的 收入-成本=利润 但其实不是 它所表达的是 收回了多少，而非利润，更准确点说就是销售收入。
+ 成本利润率:
  + 成本利润率= 利润（赚了多少） / 投入（成本），反映的是成本和利润的关系，衡量我的利润是否再生投入资本（资金回流），这个是站在资金回转时效的角度去看的。
+ 销售利润率:
  + 销售利润率= 利润（赚了多少）/ 销售（销售收入），反映销售额和利润的关系，衡量利润情况是否达到目标需求，这是站在一盘生意的情况上看的。
+ 投资回报率:
  + 投资回报率（ROI）=产出（销售收入）/ 投入（成本），反映投入和产出的关系，衡量我这个投资（花了多少钱）值不值得，能给到我多少价值的东西（非单单的利润），这个是站在投资的角度或长远生意上看的。
+ DPA: 说白了就是动态创意，根据用户的行为，分析出兴趣；然后推用户感兴趣的广告（商品）
+ OKR: Objectives and Key Results, 即目标与关键成果法，是一套明确和跟踪目标及其完成情况的管理工具和方法
+ [BI](https://www.finebi.com/2019/bifenxi): Business Intelligence 商务智能。广义上，BI是指商务智能的一套整体解决方案；狭义上，BI是指可视化BI 产品，例如FineBI。

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
  + 1.《深入浅出数据分析》-head first: [下载链接](https://github.com/JeriYang/Data-analysis-and-mining/blob/master/books/%E6%B7%B1%E5%85%A5%E6%B5%85%E5%87%BA%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%EF%BC%88%E7%BE%8E%EF%BC%89%E5%AE%8C%E6%95%B4%E4%B8%AD%E6%96%87%E7%89%88.pdf)
  + 2.《深入浅出统计学》-head first: [下载链接](https://github.com/JeriYang/Data-analysis-and-mining/blob/master/books/head%20first%20%E7%BB%9F%E8%AE%A1%E5%AD%A6.pdf)
