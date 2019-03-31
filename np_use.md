Dimension
=========

### array转换为vector 

expand_dims(np.ones(10),-1)    -1是 插入新 axis 的axis 标识    如shape(2,3,4) 插入-1 表示在最后一个axis之前插入 同理取 0 ，1 表示插入在第0第1个axis之前

np.ones(shape=(DATAN,1))    

np.stack(array,axis=)
=====================

~~~~~~~~~~

Examples
--------
>>> arrays = [np.random.randn(3, 4) for _ in range(10)]
>>> np.stack(arrays, axis=0).shape
(10, 3, 4)

>>> np.stack(arrays, axis=1).shape
(3, 10, 4)

>>> np.stack(arrays, axis=2).shape
(3, 4, 10)

>>> a = np.array([1, 2, 3])
>>> b = np.array([2, 3, 4])
>>> np.stack((a, b))
array([[1, 2, 3],
       [2, 3, 4]])

>>> np.stack((a, b), axis=-1)
array([[1, 2],
       [2, 3],
       [3, 4]])
       
~~~~~~~~~~
