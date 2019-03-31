selection
=========

- loc 根据标签来选择   data.loc[行lable,列lable]   行和列支持slice  slice是特殊a:b 包含a 包含b

- iloc 根据 0 base的标签来选择   data.iloc[行i_lable,列i_lable]   行和列支持slice  slice是正常a:b 包含a 不 包含b

- boolean select 根据某一列的值来选择 data[pd.isnull(data['Sun_hours'])] 

null value handle
=================

- data.isnull()

- data.column_name.notnull()

read_file
=========

- read_csv(file,sep=",")


change datatype
===============

### string to int64

- data.iloc[:,-2]=data.iloc[:,-2].astype("i8")   
- data.iloc[:,-2]=pd.to_numeric(data.iloc[:,-2])   


adding other column
==================

### bin 分级
- We firstly category Sun_hours into three levels: High(>10), Med(>5 and <=10), and Low(<=5)

- labels = ['Low','Med','High']

- data['Sun_level'] = pd.cut(data.Sun_hours, [-1,5,10,25], labels=labels)


暂时不知道的分类
===============
boolean_data.shift(1)   往后shift 1位
