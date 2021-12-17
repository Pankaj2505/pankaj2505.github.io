---
layout: post
title:  Masking and indexing

categories: Numpy
background: '/img/posts/numpy/cheetSheet.png'
---

## Masking and indexing

__Masking__  
1. it means manipulating(extract/modify/count) values of array based on some criteria
2. you want to remove all outlier
3. count values greater than some value
  

__Ufunc__
1. fast element wise arithmetic operation
2. element wise comparision over arrays


```python
import numpy as np
np.random.seed(0)
```


```python
# Comparision operator as ufunc
# >
# <
# >=
# <=
# !=
# ==

x = np.random.randint(11,25,size=5)
print(x)
```

    [23 16 11 14 22]
    


```python
# in simple python to find all the element greater than 20 we need to loop over it , but in numoy we can use ufunc
print(x>20)
print()
# this comparision will work with any dimension of array
x = np.random.randint(20, size=(3,4))
print(x)
print()
print(x>10)
```

    [[False False False False]
     [False False False False]
     [False False False False]]
    
    [[18  3 17 19]
     [19 19 14  7]
     [ 0  1  9  0]]
    
    [[ True False  True  True]
     [ True  True  True False]
     [False False False False]]
    

### Remark
1. here first broadcasting is happening
2. then element wise array comaprision is happening  

__Rule of broadcasting__
   - Rule 1: If the two arrays differ in their number of dimensions, the shape of the one with fewer dimensions is padded with ones on its leading (left) side.
   - Rule 2: If the shape of the two arrays does not match in any dimension, the array with shape equal to 1 in that dimension is stretched to match the other shape.
   - Rule 3: If in any dimension the sizes disagree and neither is equal to 1, an error is raised.

4. [1]--->[1,1]---->[3,4]
now perform element wise comparision


```python
# we can do element wise comparision of two array
# here it is must you have same dimension
np.array([1,2,3,4,5]) == np.array([2,12,3,14,5])
```




    array([False, False,  True, False,  True])



### Working with Boolean array
1. array([False, False,  True, False,  True])

  - np.sum(), np.any(), and np.all() are differnet from sum(), any(), all() as they cant to parallel processing
2. to count use np.sum(operation, axis)
3. checking whether any or all the values are true, np.any or np.all:


```python
# Count entries
    # how many no are greater than 5
# dir(np.random)
x = np.array([1,2,3,4,5,6,12])
y= x>3
print(y)

print(np.sum(y))
print()
print(np.count_nonzero(x>3))

```

    [False False False  True  True  True  True]
    4
    
    4
    


```python
# are there any value greater than 5
print(np.any(x>6))
print(np.all(x<15))
print(np.all(x<10))
```

    True
    True
    False
    

### Working with Bitwise operator
1.  Python's bitwise logic operators, &, |, ^, and ~.


```python
x = np.array(np.arange(10))
print(x)
print((x>2) & (x<7))
print(np.sum((x>2) & (x<7)))
```

    [0 1 2 3 4 5 6 7 8 9]
    [False False False  True  True  True  True False False False]
    4
    


```python
x[x < 5]
```




    array([0, 1, 2, 3, 4])



bit wise operator  
    - &	np.bitwise_and	 
    - |	np.bitwise_or  
    - ^	np.bitwise_xor	  
    - ~	np.bitwise_not 

# Fancy Indexing
1. Access multiple arraay element at once .print(x[[3,7,2]])
2. Combined Indexing X[2, [2, 0, 1]]


```python
# Access multiple array at once

import numpy as np
rand = np.random.RandomState(42)

x = rand.randint(100, size=10)
print(x)



print([x[3], x[7], x[2]])
print('\n'*3)



print(x[[3,7,2]])
print('\n'*3)





# it works in multidimension also 
X = np.arange(12).reshape((3, 4))
print('multidimensional array \n',X)
print('\n'*3)



row = np.array([0, 1, 2])
col = np.array([2, 1, 3])
print('display multiple indexes \n',X[row, col])
print('\n'*3)



print('Combined index\n',X[2, [2, 0, 1]])
```

    [51 92 14 71 60 20 82 86 74 74]
    [71, 86, 14]
    
    
    
    
    [71 86 14]
    
    
    
    
    multidimensional array 
     [[ 0  1  2  3]
     [ 4  5  6  7]
     [ 8  9 10 11]]
    
    
    
    
    display multiple indexes 
     [ 2  5 11]
    
    
    
    
    Combined index
     [10  8  9]
    


```python

```
