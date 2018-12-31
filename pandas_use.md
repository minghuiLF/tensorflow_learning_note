selection
=========

- loc 根据标签来选择   data.loc[行lable,列lable]   行和列支持slice  slice是特殊a:b 包含a 包含b

- iloc 根据 0 base的标签来选择   data.iloc[行i_lable,列i_lable]   行和列支持slice  slice是正常a:b 包含a 不 包含b


read_file
=========

- read_csv(file,sep=",")


change datatype
===============

### string to int64

- data.iloc[:,-2]=data.iloc[:,-2].astype("i8")   
- data.iloc[:,-2]=pd.to_numeric(data.iloc[:,-2])   
