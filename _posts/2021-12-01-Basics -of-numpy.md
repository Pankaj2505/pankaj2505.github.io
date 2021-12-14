---
layout: post
title:  "Basics of Numpy"
categories: Numpy
background: '/img/posts/numpy/cheetSheet.png'
---

[Taken reference from ](https://jakevdp.github.io/PythonDataScienceHandbook/)
<br>
<a href="\img\posts\numpy\cheetSheet.pdf" download>Download CheetSheet</a>

## Data Type

1. python data type are objects
2. these objects holds below information


```python
struct _longobject {
    long ob_refcnt;
    PyTypeObject *ob_type;
    size_t ob_size;
    long ob_digit[1];
};
```

## Numpy Array Attributes
> Determining the size, shape, memory consumption, and data types of arrays



### Define array


```python


import numpy as np

np.random.seed(0)

x1 = np.random.randint(10 , size = 6) # one Dimensional array
x2 = np.random.randint(12, size=(3,4)) # two dimensional array
x3 = np.random.randint(24, size= (3,4,2)) # three dimensional array

x4 = ['a','b','c'] # this is a list
x5 = np.array(['a','b','c']) # array with other data type
print(x1)
print('-'*30, end='\n'*3)


print(x2)
print('-'*30, end='\n'*3)

print(x3)
print('-'*30, end='\n'*3)

print(x4)
```

    [5 0 3 3 7 9]
    ------------------------------
    
    
    [[ 3  5  2  4]
     [ 7  6  8  8]
     [10  1  6  7]]
    ------------------------------
    
    
    [[[23 14]
      [17  5]
      [13  8]
      [ 9 20]]
    
     [[19 16]
      [19  5]
      [15 15]
      [ 0 18]]
    
     [[ 3 17]
      [19 19]
      [19 14]
      [ 7  0]]]
    ------------------------------
    
    
    ['a', 'b', 'c']
    

__Note__
1. Each array has attributes 
   - ndim (the number of dimensions), 
   - shape (the size of each dimension),
   - size (the total size of the array),
   - dtype (datatype of the array),
   - itemsize(size of each item of an array),
   - nbytes(size of an array in bytes).


```python
print('x3 dimension', x3.ndim)
print('x3 shape', x3.shape)
print('x3 size', x3.size)
print('x3 datatype', x3.dtype)
print('size of each element of array x3 in bytes', x3.itemsize)
print('size of complete array x3 in bytes', x3.nbytes)
```

    x3 dimension 3
    x3 shape (3, 4, 2)
    x3 size 24
    x3 datatype int32
    size of each element of array x3 in bytes 4
    size of complete array x3 in bytes 96
    

### Array Indexing : Accessing element of an array

1. indexing from begin start with 0
2. indexing from last we can use negative indices
3. In a multi-dimensional array, items can be accessed using a comma-separated tuple of indices:
4. numpy array are mutable
5. list can take many data type but numpy array has fixed datatype


```python
# index from begin
print("first item of x1 : ",x1[0])

# now i dont know the length of the array and i want to access last item
print("last item of x1 : ",x1[-1])

# how to access multidimensional array
print("1st row and 2nd column of x2 : ", x2[0,1]) # row and column couting starts with 0

# updating array value
x2[0,1] = 15
print("1st row and 2nd column of x2 : ", x2[0,1])

# numpy array will truncate decimal values, to retain the initial type
x2[0,1] = 25.523
print("1st row and 2nd column of x2 : ", x2[0,1])

## or throw an error if try to insert other datatype

print("this will thrw ValueError: invalid literal for int() with base 10: 'panakj'") # x2[0,1] = 'panakj'
```

    first item of x1 :  5
    last item of x1 :  9
    1st row and 2nd column of x2 :  25
    1st row and 2nd column of x2 :  15
    1st row and 2nd column of x2 :  25
    this will thrw ValueError: invalid literal for int() with base 10: 'panakj'
    

### Array Slicing : accessing subarray

1 Access sub array using slice notation x\[start:stop:step]  

  - default to the values start=0, stop=size of dimension, step=1


```python
# Access 1-d array
print(x1)
print(x1[:])
print(x1[::])


print('-'*30, end='\n'*3)


print(x1[::2]) #print every second item
print(x1[::-1]) # reverse the array defaults for start and stop are swapped.
print(x1[::-2]) # reverse the array and skipp 1 item


print('-'*30, end='\n'*3)


print(x1[2:4])

```

    [5 0 3 3 7 9]
    [5 0 3 3 7 9]
    [5 0 3 3 7 9]
    ------------------------------
    
    
    [5 3 7]
    [9 7 3 3 0 5]
    [9 3 0]
    ------------------------------
    
    
    [3 3]
    


```python
# access 2-D array
print(x2)
print(x2[: ,:])
print(x2[::, ::])


print('-'*30, end='\n'*3)

print(x2[1,1])
print(x2[1:3 ,2:3])
print(x2[::2, ::2])


print('-'*30, end='\n'*3)

print(x2[::-1, ::1] ,end='\n'*2)
print(x2[::-1, ::-1])
```

    [[ 3  5  2  4]
     [ 7  6  8  8]
     [10  1  6  7]]
    [[ 3  5  2  4]
     [ 7  6  8  8]
     [10  1  6  7]]
    [[ 3  5  2  4]
     [ 7  6  8  8]
     [10  1  6  7]]
    ------------------------------
    
    
    6
    [[8]
     [6]]
    [[ 3  2]
     [10  6]]
    ------------------------------
    
    
    [[10  1  6  7]
     [ 7  6  8  8]
     [ 3  5  2  4]]
    
    [[ 7  6  1 10]
     [ 8  8  6  7]
     [ 4  2  5  3]]
    

### Array Copy 
1. array slices is that they return views rather than copies of the array data. 
2. This is one area in which NumPy array slicing differs from Python list slicing: in lists, slices will be copies. 
3. as numpy slice is a view any change in view cause actual array to modify.
4. To create copy of an array use np.copy()


```python
# array slice are views

print(x2, end='\n\n')

print(x2[0:2,1:3], end='\n\n')

x2_slice = x2[0:2,1:3]
print(x2_slice , end='\n\n')

x2_slice[1,1]=100

print(x2, end='\n\n')
```

    [[ 3  5  2  4]
     [ 7  6  8  8]
     [10  1  6  7]]
    
    [[5 2]
     [6 8]]
    
    [[5 2]
     [6 8]]
    
    [[  3   5   2   4]
     [  7   6 100   8]
     [ 10   1   6   7]]
    
    


```python
# array copy is created by copy() method
x2_copy = x2.copy()
x2_copy[0,0]= 500


print(x2, end='\n\n')
print(x2_copy, end='\n\n')
```

    [[  3   5   2   4]
     [  7   6 100   8]
     [ 10   1   6   7]]
    
    [[500   5   2   4]
     [  7   6 100   8]
     [ 10   1   6   7]]
    
    

### Reshaping of array
1. use reshape() method
2. reshape method will use a no-copy view of the initial array, but with non-contiguous memory buffers 
3. used in transposing , row to column and vice-versa


```python
# reshape

x5= np.arange(12)
print(x5, end='\n'*2)


x5 = x5.reshape((4,3))
print(x5, end='\n'*2)



# Change Row vector to column vector
x5 = np.arange(5)
print(x5, end='\n'*2)

x5=x5.reshape(1,5)
print('change row vector to column', x5 , end='\n'*2)


x5=x5.reshape(5,1)
print('change column vector to row', x5, end='\n'*2)

x5 = np.arange(5)

x5=x5[np.newaxis,:]
print('change row vector to column', x5, end='\n'*2)


x5=x5[np.newaxis,:]
print('change column vector to row', x5, end='\n'*2)
```

    [ 0  1  2  3  4  5  6  7  8  9 10 11]
    
    [[ 0  1  2]
     [ 3  4  5]
     [ 6  7  8]
     [ 9 10 11]]
    
    [0 1 2 3 4]
    
    change row vector to column [[0 1 2 3 4]]
    
    change column vector to row [[0]
     [1]
     [2]
     [3]
     [4]]
    
    change row vector to column [[0 1 2 3 4]]
    
    change column vector to row [[[0 1 2 3 4]]]
    
    


```python
### Array Concatanation and splitting
1. accomplished using the routines np.concatenate, np.vstack, and np.hstack.
```


```python
x = np.array([1, 2, 3])
y = np.array([3, 2, 1])
z = [99, 99, 99]
print(np.concatenate([x, y, z]))

```

    [ 1  2  3  3  2  1 99 99 99]
    


```python
grid = np.array([[1, 2, 3],
                 [4, 5, 6]])
print(grid ,end='\n'*2)
print(np.concatenate([grid, grid]),end='\n'*2)

print(np.concatenate([grid, grid], axis=1) ,end='\n'*2)
```

    [[1 2 3]
     [4 5 6]]
    
    [[1 2 3]
     [4 5 6]
     [1 2 3]
     [4 5 6]]
    
    [[1 2 3 1 2 3]
     [4 5 6 4 5 6]]
    
    


```python
x = np.array([1, 2, 3])
grid = np.array([[9, 8, 7],
                 [6, 5, 4]])

# vertically stack the arrays
np.vstack([x, grid])
```




    array([[1, 2, 3],
           [9, 8, 7],
           [6, 5, 4]])




```python
# horizontally stack the arrays
y = np.array([[99],
              [99]])
np.hstack([grid, y])
```




    array([[ 9,  8,  7, 99],
           [ 6,  5,  4, 99]])



### Splitting of array 
 1. implemented by the functions np.split, np.hsplit, and np.vsplit
 2.np.dsplit will split arrays along the third axis.


```python
x = [1, 2, 3, 99, 99, 3, 2, 1]
x1, x2, x3 = np.split(x, [3, 5])
print(x1, x2, x3)
```

    [1 2 3] [99 99] [3 2 1]
    


```python
grid = np.arange(16).reshape((4, 4))
grid
```




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11],
           [12, 13, 14, 15]])




```python
upper, lower = np.vsplit(grid, [2])
print(upper)
print(lower)
```

    [[0 1 2 3]
     [4 5 6 7]]
    [[ 8  9 10 11]
     [12 13 14 15]]
    


```python
left, right = np.hsplit(grid, [2])
print(left)
print(right)
```

    [[ 0  1]
     [ 4  5]
     [ 8  9]
     [12 13]]
    [[ 2  3]
     [ 6  7]
     [10 11]
     [14 15]]
    


```python

```
