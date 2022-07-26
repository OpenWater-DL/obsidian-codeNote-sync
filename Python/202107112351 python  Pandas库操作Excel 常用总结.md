# libr
[python pandas Examples清晰分类了实例情况](https://pythonexamples.org/pandas-examples/)


数据分析用pandas库，pandas库操作Excel似乎还要依赖openxyl
`import pandas as pd`

路径相关用os库
`import os`

其他用例：[[Python/202107111556 python文件整理-按格式分类文件到指定文件夹]]

正则表达式用re库
`import re`
[[202107111815 正则表达式]]
# read
` df = pd.read_excel(filePath, header=3)`
这里header=3的意思是，设置列名为第四行（索引是[3]）的行。

# 操作表格内容

### 重新设置列名
` df.columns = ['第一列内容', 'nums', 'discribe', 'zy', 'bz']`
(不是一个什么非常必要的操作，只是为了方便之后对列定位时键入key方便，改成了比较短的名字)

### 定位
` test = hgzb['nums'].at[2] ` 
hgzb是读来处理的Excel文件nums是我改的列名（看上一步设置），at表示内容索引（定位到具体的行[2]就是第三行）


```py
"""
日期:2021.07.11
描述：扫描指定文件夹下的多个Excel，并读取指定位置的数据.

"""

import os
import pandas as pd
import re

filePath = os.path.dirname('/Users/waterkon/Downloads/pandas练习/分支机构合规周表-河池西环路营业部（20210607-20200611）.xlsx')
files = os.listdir(filePath)
print(files)

count =[0 for i in range(5)]
print('现在的count包含以下内容')
print(count)
for item in files:
    hgzb = pd.read_excel( os.path.join(filePath, item), header=3)
    hgzb.columns = ['第一列内容', 'nums', 'discribe', 'zy', 'bz']

    # test = hgzb['nums'].at[2] #定位测试
    # print(item+test)

    for i in range(1, 6):  #range(1,6)细节，会输出1~5，而不到6
	
	
        ptn = r'\d'
        thisNum = hgzb['nums'].at[i].split('：')[-1]
        getNum = re.findall(ptn, thisNum)[0]  
		#因为正则返回的是一个list,所以[0]表示第一个。
		#`findall(r'',str)`查找全部，r标识代表后面是正则的语句

		
		
		getNum = int(getNum)
        count[i-1] += getNum
        #count是默认从0开始索引，而i是1~5，所以i-1才是正确的索引。即[0];i=1


print('流程数量:'+ str(count[0]))
print('咨询问题:'+ str(count[1]))
print('宣导次数:'+ str(count[2]))
print('本周培训次数:'+ str(count[3]))
print('处理次数:'+ str(count[4]))

```

