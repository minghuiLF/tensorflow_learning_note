## Series
~~~~~~~~
  
  In [11]: obj = pd.Series([4, 7, -5, 3])
  In [12]: obj
  Out[12]:
  0 4
  1 7
  2 -5
  3 3
  dtype: int64
 

  In [13]: obj.values
  Out[13]: array([ 4, 7, -5, 3])
  In [14]: obj.index # like range(4)
  Out[14]: RangeIndex(start=0, stop=4, step=1)
  
  // The string representation of a Series displayed interactively shows the index on the
left and the values on the right. Since we did not specify an index for the data, a
default one consisting of the integers 0 through N - 1 (where N is the length of the
data) is created. //

  You can get the array representation and index object of the Series via
its values and index attributes, respectively
  
  In [15]: obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  In [16]: obj2
  Out[16]:
  d 4
  b 7
  a -5
  c 3
  dtype: int64
  In [17]: obj2.index
  Out[17]: Index(['d', 'b', 'a', 'c'], dtype='object')
  
  Compared with NumPy arrays, you can use labels in the index when selecting single
values or a set of values:
 
  In [18]: obj2['a']
  Out[18]: -5
  In [19]: obj2['d'] = 6
  In [20]: obj2[['c', 'a', 'd']]
  Out[20]:
  c 3
  a -5
  d 6
  dtype: int64
  
  
  
In [21]: obj2[obj2 > 0]
Out[21]:
d 6
b 7
c 3
dtype: int64
In [22]: obj2 * 2
Out[22]:
d 12
b 14
a -10
c 6
dtype: int64
In [23]: np.exp(obj2)
Out[23]:
d 403.428793
b 1096.633158
a 0.006738
c 20.085537
dtype: float64

~~~~~~~~

--------------------------

~~~~~~~~
indexing like a dic
 
In [24]: 'b' in obj2   
Out[24]: True

In [25]: 'e' in obj2
Out[25]: False


In [26]: sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}
In [27]: obj3 = pd.Series(sdata)
In [28]: obj3
Out[28]:
Ohio 35000
Oregon 16000
Texas 71000
Utah 5000
dtype: int64


  
~~~~~~~~




~~~~~
When you are only passing a dict, the index in the resulting Series will have the dict’s
keys in sorted order. You can override this by passing the dict keys in the order you
want them to appear in the resulting Series:

In [29]: states = ['California', 'Ohio', 'Oregon', 'Texas']
In [30]: obj4 = pd.Series(sdata, index=states)
In [31]: obj4
Out[31]:
California NaN
Ohio 35000.0
Oregon 16000.0
Texas 71000.0
dtype: float64


~~~~~

-------------------------

- Both the Series object itself and its index have a name attribute, which integrates with
other key areas of pandas functionality:
~~~~~

In [38]: obj4.name = 'population'
In [39]: obj4.index.name = 'state'
In [40]: obj4
Out[40]:
state
California NaN
Ohio 35000.0
Oregon 16000.0
Texas 71000.0
Name: population, dtype: float64


~~~~~



~~~~~


In [46]: frame.head()    // For large DataFrames, the head method selects only the first 5 rows:

Out[46]:
pop state year
0 1.5 Ohio 2000
1 1.7 Ohio 2001
2 3.6 Ohio 2002
3 2.4 Nevada 2001
4 2.9 Nevada 2002


In [47]: pd.DataFrame(data, columns=['year', 'state', 'pop']) //If you specify a sequence of columns, the DataFrame’s columns will be arranged in
that order:

Out[47]:
year state pop
0 2000 Ohio 1.5
1 2001 Ohio 1.7
2 2002 Ohio 3.6
3 2001 Nevada 2.4
4 2002 Nevada 2.9
5 2003 Nevada 3.2


If you pass a column that isn’t contained in the dict, it will appear with missing values
in the result:

In [48]: frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'],
....: index=['one', 'two', 'three', 'four',
....: 'five', 'six'])

In [49]: frame2
Out[49]:
year state pop debt
one 2000 Ohio 1.5 NaN
two 2001 Ohio 1.7 NaN
three 2002 Ohio 3.6 NaN
four 2001 Nevada 2.4 NaN
five 2002 Nevada 2.9 NaN
six 2003 Nevada 3.2 NaN


~~~~~
## Frame
- 总结
- **frame.columns**  访问column index
- **frame.index**  访问row index

- frame['colunmn_name']  访问列 两种方法

  frame.colunmn_name

- frame.loc['row_name'] 访问行

~~~~~~
In [99]: frame
Out[99]:
Ohio Texas California
a 0 1 2
c 3 4 5
d 6 7 8

states = ['Texas', 'Utah', 'California']

In [104]: frame.loc[['a', 'b', 'c', 'd'], states]
Out[104]:
Texas Utah California
a 1.0 NaN 2.0
b NaN NaN NaN
c 4.0 NaN 5.0
d 7.0 NaN 8.0


~~~~~~

- **frame.values**  数据表格  value**s**



frame.index.name = 'year'; frame.columns.name = 'state'  行和列的名字


**Many functions, like drop, which modify the size or shape of a Series or DataFrame,
can manipulate an object in-place without returning a new object:**

**Be careful with the _inplace_, as it destroys any data that is dropped.**

-------------------------------------------
~~~~~
In [50]: frame2.columns
Out[50]: Index(['year', 'state', 'pop', 'debt'], dtype='object')

In [51]: frame2['state']
Out[51]:
one Ohio
two Ohio
three Ohio
four Nevada
five Nevada
six Nevada
Name: state, dtype: object

In [52]: frame2.year
Out[52]:
one 2000
two 2001
three 2002
four 2001
five 2002
six 2003
Name: year, dtype: int64

----------------------------------------------------------

In [53]: frame2.loc['three']
Out[53]:
year 2002
state Ohio
pop 3.6
debt NaN
Name: three, dtype: object

~~~~~


整列操作
- frame['clomun_name']= n                   all change to n

- frame['clomun_name']= np.arange(6.)       length must match 

- frame['clomun_name']= pd.Series           labels will be realigned exactly to the DataFrame’s index, inserting missing values in any holes
                                           

Assigning a column that doesn’t exist will create a new column.

*frame.clomun_name*(上面都是['clomun_name']) syntax can not use to create new column

del frame['clomun_name']           **del**      keyword will delete columns as with a dict.
~~~~~~~

frame2['debt'] = 16.5
In [55]: frame2
Out[55]:
year state pop debt
one 2000 Ohio 1.5 16.5
two 2001 Ohio 1.7 16.5
three 2002 Ohio 3.6 16.5
four 2001 Nevada 2.4 16.5
five 2002 Nevada 2.9 16.5
six 2003 Nevada 3.2 16.5

In [56]: frame2['debt'] = np.arange(6.)
In [57]: frame2
Out[57]:
year state pop debt
one 2000 Ohio 1.5 0.0
two 2001 Ohio 1.7 1.0
three 2002 Ohio 3.6 2.0
four 2001 Nevada 2.4 3.0
five 2002 Nevada 2.9 4.0
six 2003 Nevada 3.2 5.0


In [58]: val = pd.Series([-1.2, -1.5, -1.7], index=['two', 'four', 'five'])
In [59]: frame2['debt'] = val
In [60]: frame2
Out[60]:
year state pop debt
one 2000 Ohio 1.5 NaN
two 2001 Ohio 1.7 -1.2
three 2002 Ohio 3.6 NaN
four 2001 Nevada 2.4 -1.5
five 2002 Nevada 2.9 -1.7
six 2003 Nevada 3.2 NaN

~~~~~~~

---------------------------------------

~~~~~~~
In [65]: pop = {'Nevada': {2001: 2.4, 2002: 2.9},
....: 'Ohio': {2000: 1.5, 2001: 1.7, 2002: 3.6}}


If the nested dict is passed to the DataFrame, pandas will interpret the outer dict keys
as the columns and the inner keys as the row indices:

In [66]: frame3 = pd.DataFrame(pop)
In [67]: frame3
Out[67]:
Nevada Ohio
2000 NaN 1.5
2001 2.4 1.7
2002 2.9 3.6

The keys in the inner dicts are combined and sorted to form the index in the result.
This isn’t true if an explicit index is specified:

In [69]: pd.DataFrame(pop, index=[2001, 2002, 2003])  <--区别2003
Out[69]:
Nevada Ohio
2001 2.4 1.7
2002 2.9 3.6
2003 NaN NaN


~~~~~~~
__frame3.T__
~~~~~~~~~~

In [68]: frame3.T
Out[68]:
2000 2001 2002
Nevada NaN 2.4 2.9
Ohio 1.5 1.7 3.6

~~~~~~~~~~


- frame.index.name = 'year'; frame.columns.name = 'state'
~~~~~~~~

In [72]: frame3.index.name = 'year'; frame3.columns.name = 'state'
In [73]: frame3
Out[73]:
state Nevada Ohio
year
2000 NaN 1.5
2001 2.4 1.7
2002 2.9 3.6

~~~~~~~~

- frame.values

~~~~~~~
In [75]: frame2.values
Out[75]:
array([[2000, 'Ohio', 1.5, nan],
[2001, 'Ohio', 1.7, -1.2],
[2002, 'Ohio', 3.6, nan],
[2001, 'Nevada', 2.4, -1.5],
[2002, 'Nevada', 2.9, -1.7],
[2003, 'Nevada', 3.2, nan]], dtype=object)

~~~~~~~

complete list of things you can pass the DataFrame constructor

<img src="dataframe_constructor.png"/>


## Index Objects

pandas’s Index objects are responsible for holding the axis labels and other metadata
(like the axis name or names). Any array or other sequence of labels you use when
constructing a Series or DataFrame is internally converted to an Index:

~~~~~~
In [76]: obj = pd.Series(range(3), index=['a', 'b', 'c'])
In [77]: index = obj.index
In [78]: index
Out[78]: Index(['a', 'b', 'c'], dtype='object')
In [79]: index[1:]
Out[79]: Index(['b', 'c'], dtype='object')


Index objects are immutable and thus can’t be modified by the user:

index[1] = 'd' # TypeError

Immutability makes it safer to share Index objects among data structures:

In [80]: labels = pd.Index(np.arange(3))
In [81]: labels
Out[81]: Int64Index([0, 1, 2], dtype='int64')
In [82]: obj2 = pd.Series([1.5, -2.5, 0], index=labels)
In [83]: obj2
Out[83]:
0 1.5
1 -2.5
2 0.0
dtype: float64
In [84]: obj2.index is labels
Out[84]: True

~~~~~~

-----------------------

In addition to being array-like, an Index also behaves like a fixed-size set:

however

Unlike Python sets, a pandas Index can contain duplicate labels:
~~~~~~
In [86]: frame3.columns
Out[86]: Index(['Nevada', 'Ohio'], dtype='object', name='state')
In [87]: 'Ohio' in frame3.columns
Out[87]: True
In [88]: 2003 in frame3.index
Out[88]: False

Unlike Python sets, a pandas Index can contain duplicate labels:

In [89]: dup_labels = pd.Index(['foo', 'foo', 'bar', 'bar'])
In [90]: dup_labels
Out[90]: Index(['foo', 'foo', 'bar', 'bar'], dtype='object')

~~~~~~

Each Index has a number of methods and properties for set logic, which answer other
common questions about the data it contains. Some useful ones are summarized here

<img src="pd_index_methods.png"/>

## Reindexing

~~~~~~~
In [91]: obj = pd.Series([4.5, 7.2, -5.3, 3.6], index=['d', 'b', 'a', 'c'])
In [92]: obj
Out[92]:
d 4.5
b 7.2
a -5.3
c 3.6
dtype: float64

Calling reindex on this Series rearranges the data according to the new index, introducing
missing values if any index values were not already present:

In [93]: obj2 = obj.reindex(['a', 'b', 'c', 'd', 'e'])
In [94]: obj2
Out[94]:
a -5.3
b 7.2
c 3.6
d 4.5
e NaN
dtype: float64

~~~~~~~

For ordered data like time series, it may be desirable to do some interpolation or filling
of values when reindexing. The method option allows us to do this, using a
method such as ffill, which forward-fills the values:

~~~~~~~
In [95]: obj3 = pd.Series(['blue', 'purple', 'yellow'], index=[0, 2, 4])
In [96]: obj3
Out[96]:
0 blue
2 purple
4 yellow
dtype: object

In [97]: obj3.reindex(range(6), method='ffill')
Out[97]:
0 blue
1 blue
2 purple
3 purple
4 yellow
5 yellow
dtype: object
~~~~~~~

- With DataFrame, reindex can alter either the (row) index, columns, or both. 
  -  When passed only a sequence, it reindexes the rows in the result:
     frame.reindex(indexobj)
  -  The columns can be reindexed with the columns keyword 
     frame.reindex(columns=indexobj)
~~~~~
In [98]: frame = pd.DataFrame(np.arange(9).reshape((3, 3)),
....: index=['a', 'c', 'd'],
....: columns=['Ohio', 'Texas', 'California'])
In [99]: frame
Out[99]:
Ohio Texas California
a 0 1 2
c 3 4 5
d 6 7 8
----------------------------------------------------------------------index
In [100]: frame2 = frame.reindex(['a', 'b', 'c', 'd'])
In [101]: frame2
Out[101]:
Ohio Texas California
a 0.0 1.0 2.0
b NaN NaN NaN
c 3.0 4.0 5.0
d 6.0 7.0 8.0

----------------------------------------------------------------------column
In [102]: states = ['Texas', 'Utah', 'California']
In [103]: frame.reindex(columns=states)
Out[103]:
Texas Utah California
a 1 NaN 2
c 4 NaN 5
d 7 NaN 8

~~~~~

you can reindex more succinctly by label-indexing with loc, and many users prefer to use it exclusively

~~~~~~~~~
frame.loc[['a', 'b', 'c', 'd'], states]   #总结地方有
~~~~~~~~~

reindex function arguments

<img src="pd_reindex_arg.png" />

## Dropping Entries from an Axis

~~~~~
Calling drop with a sequence of labels will drop values from the row labels (axis 0):
- data.drop(['Colorado', 'Ohio'])

You can drop values from the columns by passing axis=1 or axis='columns':
- data.drop('two', axis=1)


In [105]: obj = pd.Series(np.arange(5.), index=['a', 'b', 'c', 'd', 'e'])
In [106]: obj
Out[106]:
a 0.0
b 1.0
c 2.0
d 3.0
e 4.0
dtype: float64

In [107]: new_obj = obj.drop('c')
In [108]: new_obj
Out[108]:
a 0.0
b 1.0
d 3.0
e 4.0
dtype: float64

In [109]: obj.drop(['d', 'c'])
Out[109]:
a 0.0
b 1.0
e 4.0
dtype: float64

data.drop('two', axis=1)  # drop columns 
~~~~~


## Indexing, Selection, and Filtering

**Series** indexing (obj[...]) works analogously to NumPy array indexing, except you
can use the Series’s index values instead of only integers. Here are some examples of
this:

**类似NumPy array indexing   ([:] slice , obj[obj < 2] boolean 等等) **

~~~~~~~~~~
In [117]: obj = pd.Series(np.arange(4.), index=['a', 'b', 'c', 'd'])
In [118]: obj
Out[118]:
a 0.0
b 1.0
c 2.0
d 3.0
dtype: float64


In [119]: obj['b']
Out[119]: 1.0

In [120]: obj[1]
Out[120]: 1.0
In [121]: obj[2:4]
Out[121]:
c 2.0
d 3.0
dtype: float64
In [122]: obj[['b', 'a', 'd']]
Out[122]:
b 1.0
a 0.0
d 3.0
dtype: float64
In [123]: obj[[1, 3]]
Out[123]:
b 1.0
d 3.0
dtype: float64
In [124]: obj[obj < 2]
Out[124]:
a 0.0
b 1.0
dtype: float64

~~~~~~~~~~

---------------------------

Indexing into a **DataFrame** is for retrieving one or more **columns** either with a single
value or sequence:

~~~~~~~~
In [128]: data = pd.DataFrame(np.arange(16).reshape((4, 4)),
.....: index=['Ohio', 'Colorado', 'Utah', 'New York'],
.....: columns=['one', 'two', 'three', 'four'])
In [129]: data
Out[129]:
one two three four
Ohio 0 1 2 3
Colorado 4 5 6 7
Utah 8 9 10 11
New York 12 13 14 15
In [130]: data['two']
Out[130]:
Ohio 1
Colorado 5
Utah 9
New York 13
Name: two, dtype: int64
In [131]: data[['three', 'one']]
Out[131]:
three one
Ohio 2 0
Colorado 6 4
Utah 10 8
New York 14 12

~~~~~~~~

Indexing like this has a few special cases. First, slicing or selecting data with a boolean
array:

~~~~~~~~

The row selection syntax data[:2] is provided as a convenience. Passing a single element
or a list to the [] operator selects columns.

In [132]: data[:2]             
Out[132]:
one two three four
Ohio 0 1 2 3
Colorado 4 5 6 7



Another use case is in indexing with a boolean DataFrame, such as one produced by a
scalar comparison:

In [133]: data[data['three'] > 5]
Out[133]:
one two three four
Colorado 4 5 6 7
Utah 8 9 10 11
New York 12 13 14 15

--------------------------

In [134]: data < 5
Out[134]:
one two three four
Ohio True True True True
Colorado True False False False
Utah False False False False
New York False False False False

In [135]: data[data < 5] = 0
In [136]: data
Out[136]:
one two three four
Ohio 0 0 0 0
Colorado 0 5 6 7
Utah 8 9 10 11
New York 12 13 14 15

This makes DataFrame syntactically more like a two-dimensional NumPy array in
this particular case.
~~~~~~~~


### Selection with loc and iloc

loc and iloc. They enable you to select a subset of the rows and columns from a
DataFrame with NumPy-like notation using either axis labels (loc) or integers
(iloc).


~~~~~~~~~~~~~

In [136]: data
Out[136]:
one two three four
Ohio 0 0 0 0
Colorado 0 5 6 7
Utah 8 9 10 11
New York 12 13 14 15


In [137]: data.loc['Colorado', ['two', 'three']]
Out[137]:
two 5
three 6
Name: Colorado, dtype: int64

In [138]: data.iloc[2, [3, 0, 1]]
Out[138]:
four 11
one 8
two 9
Name: Utah, dtype: int64

In [139]: data.iloc[2]
Out[139]:
one 8
two 9
three 10
four 11
Name: Utah, dtype: int64

In [140]: data.iloc[[1, 2], [3, 0, 1]]
Out[140]:
four one two
Colorado 7 0 5
Utah 11 8 9

Both indexing functions work with slices in addition to single labels or lists of labels:


In [141]: data.loc[:'Utah', 'two']
Out[141]:
Ohio 0
Colorado 5
Utah 9
Name: two, dtype: int64

In [142]: data.iloc[:, :3][data.three > 5]
Out[142]:
one two three
Colorado 0 5 6
Utah 8 9 10
New York 12 13 14

~~~~~~~~~~~~~





