# Data-analysis-and-mining
Study notes.

### 1.数据读取
+ 方式1：

<html>  
    <title>import pandas as pd</title>
    <title>io = pd.io.excel.ExcelFile(r'D:\data\python\amazon_data.xlsx')</title>
    <title>amazon_data = pd.read_excel(io,sheetname='data')</title>
    <title>price = pd.read_excel(io,sheetname='price')</title>
    <title>io.close()</title>
</html>

+ 方式2：
    import pandas as pd
    amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheetname='data')
    price = pd.read_excel(r'amazon_data.xlsx',sheetname='price')
    #ps:在数据量大、sheet多的情况下，方式1的速度大于方式2的速度

### 2.数据存储
+ 方式1:
    import pandas as pd
    amazon_data = pd.read_excel(r'D:\data\python\amazon_data.xlsx',sheetname='data')
    amazon_data.to_excel(r'D:\data\new.xlsx')  #存入D盘的data文件夹

+ 方式2: 如果是多个表需要输出，且输出到一个Excel的不同sheet
    import pandas as pd
    writer=pd.ExcelWriter(r'D:\data\python\存储数据.xlsx')
    amazon_data .to_excel(writer,sheet_name='data')
    price.to_excel(writer,sheet_name='price')
    writer.save()
