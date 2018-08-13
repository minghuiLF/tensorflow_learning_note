



# Ipython 

<img src="frequency_magic_command.png"/>

%run
%run -i

# Numpy as np
## ndarrays

<img src="ndarray.png"/>

~~~~~
  Data=[1,2,3]                                              
  np.array(Data)
  array([ 1, 2, 3]
  
  np.zeros(10)
  array([ 0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])
  
  np.empty(10)
  array([arbitrary*10])
  
  np.ones(10)
  array([ 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.])
  
  np.arange(15)                                                           
  array([ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
  
  np.full(10,5)
  array([ 5*10])
  
  #一些常见矩阵创建方法
  
  arr = np.arange(32).reshape((8, 4))                         
  
  arr = np.empty((8, 4))
  for i in range(8):
      arr[i] = i
  
  np.full((10,5),True)
  
  D.dtype
  D.ndim
  D.shape
  
  
~~~~~~~
<img src="dtype.png"/>

## np.astype()

    - Calling astype always creates a new array (a copy of the data), even
      if the new dtype is the same as the old dtype.
~~~~~~~~

  arr=np.ones(10,dtype='?')
  a=arr.astype('i4')
  a=arr.astype(np.int32)
  
  
  numeric_strings = np.array(['1.25', '-9.6', '42'], dtype=np.string_)
  numeric_strings.astype(float)
  array([ 1.25, -9.6 , 42. ])
  
  boo_array=npp.array([True,False])
  int_array.astype(bool_array.dtype)
  
  

~~~~~~~~


## strids
  每个dim上该arry存储的byte
  以此来访问每一个数据
~~~~~~~

  In [11]: np.ones((3, 4, 5), dtype=np.float64).strides
  Out[11]: (160, 40, 8)

  5*8 40 *4 160
  
~~~~~~~

## Arithmetic

~~~~~~
  
  arr * 10
  arr ** 0.5
  -------------------
  math.sin(1)
  0.8414....
  np.sin(1)
  0.8414....
  
  math.sin(arr)
  Error  
  np.sin(arr)
  [.841,.841]
  --------------------
 
  arr > arr2 
  array([[False, True, False],
        [ True, False, True]], dtype=bool)
  
~~~~~~

## slice [a:b]

~~~~~~~
 !!!index in slice a,b  it's index, from 0 
 a 包含
 b：不包含
 
 arr [0:1] =arr[0]
 arr [3:6] =(3,4,5) arr[3].append(arr[4]).append(arr[5])
 
  "one end" & "bare" slice: 
 [a:],[:b],[:]
 arr_slice[a:]  a to end  
 arr_slice[:b]  begin to b-1  
 arr_slice[:]  all  
 
 [::-1] reverse
 
 arr = np.ones(10)
 arr[5,8] = 12 普通的array 不可以
 : array([1,1,1,1,1,12,12,12,1,1])
 
 arr_slice = arr[5:8]
 arr_slice
 : array([12, 12, 12])
 
 !!! note the slice edition will change the original array
 all above typeof slice include[::-1]
 
 arr_slice[1]=12345
 arr
 array([ 1... ,12, 12345, 12,1,1])
 
 using arr[5:8].copy()  !!!
 ~~~~~~~
 
 
 <img  src="2dindex.png" />
 
 ~~~~~~~
 
 hight dimension 
 
 arr_hightd[a][b][c]
 arr_hightd[a,b,c]
 
 notice !!
 arr3d.shape=(2,2,3)
 arr3d[0]= 42 will change all the [0]th 2*3 2d-array's value to 42
 
 

~~~~~~~
  __all this kind of selections are views__
  __whcih means if you change it you will change the original as well__

~~~~~~~

arr2d
  array([[1, 2, 3],
         [4, 5, 6],
         [7, 8, 9]])
       
arr2d[:2]
  array([[1, 2, 3],
         [4, 5, 6]])

multiple slices:

arr2d[:2, 1:]
  array([[2, 3],
         [5, 6]])
         
arr2d[1, :2]
  array([4, 5])
  
arr2d[:2, 2]      #noice this is a little different ,it will take the 'column' to a single array
  array([3, 6])   # see below  if you use [:2,2:] will give you 'column'


arr2d[:, :1]     #if you want the 'column' version use slice 
  array([[1],
         [4],
         [7]])
  
~~~~~~~
__Note that a colon by itself means to take the entire__
__axis, so you can slice only higher dimensional axes by colon [:]__

<img src="2dslice.png"/>


## Boolean Indexing

- Suppose each name corresponds to a row in the data array and we wanted to select
all the rows with corresponding name 'Bob'.

__Boolean selection will not fail if the boolean array is not the correct
length, so I recommend care when using this feature__
~~~~~~
names = np.array(['Bob', 'Joe', 'Will', 'Bob', 'Will', 'Joe', 'Joe'])
data = np.random.randn(7, 4)

names == 'Bob'
Out: array([ True, False, False, True, False, False, False], dtype=bool)


data[names == 'Bob']
Out:
array([[ 0.0929, 0.2817, 0.769 , 1.2464],
       [ 1.669 , -0.4386, -0.5397, 0.477 ]])
~~~~~~

__You can even mix and match boolean arrays with slices or integers (or sequences of integers__

~~~~~~~
In [104]: data[names == 'Bob', 2:]
Out[104]:
array([[ 0.769 , 1.2464],
       [-0.5397, 0.477 ]])

In [105]: data[names == 'Bob', 3]
Out[105]: array([ 1.2464, 0.477 ])


~~~~~~~

__To select everything but 'Bob', you can either use != or negate the condition using ~:__

__combine multiple boolean conditions,use
boolean arithmetic operators like & (and) and | (or):__

**python ___'and' 'or'___ not work**


~~~~~~~
names != 'Bob'

data[~(names == 'Bob')]

mask = (names == 'Bob') | (names == 'Will')

data[mask]

~~~~~~~

__Selecting data from an array by boolean indexing always creates a copy of the data,
even if the returned array is unchanged.__



__Setting values with boolean arrays works in a common-sense way__


__this is setting value so not about copy:)__ 


~~~~~~~

In [113]: data[data < 0] = 0
In [114]: data
Out[114]:
array
([[ 0.0929, 0.2817, 0.769 , 1.2464],
  [ 1.0072, 0. , 0.275 , 0.2289],
  [ 1.3529, 0.8864, 0. , 0. ],
  [ 1.669 , 0. , 0. , 0.477 ],
  [ 3.2489, 0. , 0. , 0.1241],
  [ 0.3026, 0.5238, 0.0009, 1.3438],
  [ 0. , 0. , 0. , 0. ]])


In [115]: data[names != 'Joe'] = 7
In [116]: data
Out[116]:
array
([[ 7. , 7. , 7. , 7. ],
  [ 1.0072, 0. , 0.275 , 0.2289],
  [ 7. , 7. , 7. , 7. ],
  [ 7. , 7. , 7. , 7. ],
  [ 7. , 7. , 7. , 7. ],
  [ 0.3026, 0.5238, 0.0009, 1.3438],
  [ 0. , 0. , 0. , 0. ]])

~~~~~~~

## Fancy Indexing

~~~~~~~~~




array([[ 0., 0., 0., 0.],
       [ 1., 1., 1., 1.],
       [ 2., 2., 2., 2.],
       [ 3., 3., 3., 3.],
       [ 4., 4., 4., 4.],
       [ 5., 5., 5., 5.],
       [ 6., 6., 6., 6.],
       [ 7., 7., 7., 7.]])
       
       
In [120]: arr[[4, 3, 0, 6]]
Out[120]:
array([[ 4., 4., 4., 4.],
       [ 3., 3., 3., 3.],
       [ 0., 0., 0., 0.],
       [ 6., 6., 6., 6.]])      
       
       
In [121]: arr[[-3, -5, -7]]
Out[121]:
array([[ 5., 5., 5., 5.],
       [ 3., 3., 3., 3.],
       [ 1., 1., 1., 1.]])

~~~~~~~~~

__The behavior of fancy indexing in this case is a bit different from what some users
might have expected (myself included), which is the rectangular region formed by
selecting a subset of the matrix’s rows and columns. Here is one way to get that:__

~~~~

array([[ 0, 1, 2, 3],
[ 4, 5, 6, 7],
[ 8, 9, 10, 11],
[12, 13, 14, 15],
[16, 17, 18, 19],
[20, 21, 22, 23],
[24, 25, 26, 27],
[28, 29, 30, 31]])


In [124]: arr[[1, 5, 7, 2], [0, 3, 1, 2]]               #(1,0)(5,3)(7,1)(2,2)
Out[124]: array([ 4, 23, 29, 10])

In [125]: arr[[1, 5, 7, 2]][:, [0, 3, 1, 2]]
Out[125]:
array([[ 4, 7, 5, 6],
       [20, 23, 21, 22],
       [28, 31, 29, 30],
       [ 8, 11, 9, 10]])

~~~~

__Keep in mind that fancy indexing, unlike slicing, always copies the data into a new
array.__
