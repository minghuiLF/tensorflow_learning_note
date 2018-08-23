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

- **frame.columns**  访问column index
- **frame.index**  访问row index

- frame['colunmn_name']  两种方法
- frame.colunmn_name

- frame.loc['row_name'] 访问行 
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
frame['clomun_name']= n                   all change to n
frame['clomun_name']= np.arange(6.)       length must match 
frame['clomun_name']= pd.Series           labels will be realigned exactly to
                                           the DataFrame’s index, inserting missing values in any holes

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



