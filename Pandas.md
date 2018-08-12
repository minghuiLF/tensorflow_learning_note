



#Ipython 

<img src="frequency_magic_commands.png"/>

%run
%run -i

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
  
  
  D.dtype
  D.ndim
  D.shape
  
  
~~~~~~~
<img src="dtype.png"/>

### np.astype()

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


### strids
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

page94
