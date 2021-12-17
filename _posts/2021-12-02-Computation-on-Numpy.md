---
layout: post
title:  "Computation in Numpy"

categories: Numpy
background: '/img/posts/numpy/cheetSheet.png'
---

![cheetSheet](\img\posts\numpy\cheetSheet.png)

# Here we will learn topics like 
1. Universal function
2. aggreagate function
3. Broadcasting

## we also need to check operatior like
1. arithmatic 
2. relational
3. boolean and, or, not.

4. aggregation function
   - they are differ because of execution in compiled mode
   - np.aggregate can do dimension wise aggregation
5. np.any(),np.all(),np.sum()

6. bit wise operator
    - &	np.bitwise_and	
    - |	np.bitwise_or
    - ^	np.bitwise_xor	
    - ~	np.bitwise_not 
 7. difference between boolean and bitwise
 > The difference is this: and and or gauge the truth or falsehood of entire object, while & and | refer to bits within each object.  
 
  

## Universal function

1. A big difference between python array and numpy array is execution speed.
2. python array iterate through each element and then process it.
3. numpy array use the concept of vectorized operation, which mean computing all elements of an array parallely

> we implement computaion in numpy array using universal function,"ufunc"

#### Why numpy function are fast
> it is beacuse here we use somthing called broadcasting, in broadcasting , first the code is compiled and then executed.This is the main difference between python and numpy , in python the code is compiled at run time, so this will take some time when we are processing a huge data, while in numpy , the huge data is already compiled during creation , so this will save time during execution

##### compare effectiveness between python array and numpy array


```python
# we want to find reciprocal of array element
import numpy as np
np.random.seed(0)



def reciprocal (arr):
    output = np.empty(len(arr))
    for x in range(len(arr)):
        output[x] = 1.0/arr[x]
    return output


array = np.random.randint(5,20, size=500)   
%timeit reciprocal(array)


# calculating same operation using numpy universal function
%timeit 1.0/array
```

    3.59 ms ± 121 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
    7.41 µs ± 398 ns per loop (mean ± std. dev. of 7 runs, 100000 loops each)
    

####  Exploring more Ufunc
1. arithmatic opeartion are of two type unary and binary
2. unary opeartion like (-), ** exponent, % modulas



```python
x = np.arange(4)
print("x     =", x)
print("x + 5 =", x + 5)
print("x - 5 =", x - 5)
print("x * 2 =", x * 2)
print("x / 2 =", x / 2)
print("x // 2 =", x // 2)  # floor division

print("-x     = ", -x)
print("x ** 2 = ", x ** 2)  #power
print("x % 2  = ", x % 2)  # reminder
```

    x     = [0 1 2 3]
    x + 5 = [5 6 7 8]
    x - 5 = [-5 -4 -3 -2]
    x * 2 = [0 2 4 6]
    x / 2 = [0.  0.5 1.  1.5]
    x // 2 = [0 0 1 1]
    -x     =  [ 0 -1 -2 -3]
    x ** 2 =  [0 1 4 9]
    x % 2  =  [0 1 0 1]
    


```python
y = np.arange(-10,-5)
print('y',y)
print("python absolute function abs",np.abs(y) )
print('numpy absolute function absolute', np.absolute(y))
```

    y [-10  -9  -8  -7  -6]
    python absolute function abs [10  9  8  7  6]
    numpy absolute function absolute [10  9  8  7  6]
    


```python
x = [1, 2, 3]
print("x     =", x)
print("e^x   =", np.exp(x))
print("2^x   =", np.exp2(x))
print("3^x   =", np.power(3, x))


x = [1, 2, 4, 10]
print("x        =", x)
print("ln(x)    =", np.log(x))
print("log2(x)  =", np.log2(x))
print("log10(x) =", np.log10(x))
```

    x     = [1, 2, 3]
    e^x   = [ 2.71828183  7.3890561  20.08553692]
    2^x   = [2. 4. 8.]
    3^x   = [ 3  9 27]
    x        = [1, 2, 4, 10]
    ln(x)    = [0.         0.69314718 1.38629436 2.30258509]
    log2(x)  = [0.         1.         2.         3.32192809]
    log10(x) = [0.         0.30103    0.60205999 1.        ]
    

#### some more operation
>  calling reduce on the add ufunc returns the sum of all elements in the array:  
Specifying output


```python
##### Specifying output
x = np.arange(5)
y = np.empty(5)
np.multiply(x, 10, out=y)
print(y)


x = [1,2,3,4,5]
print(np.multiply.reduce(x))
print(np.multiply.accumulate(x))
```

    [ 0. 10. 20. 30. 40.]
    120
    [  1   2   6  24 120]
    

## Aggregation in Numpy
1. sum() and np.sum() and np.nansum()
2. remember np.sum() take cares of multidimensionality also . so never use python sum() with multidimensional array 



```python
big_array = np.random.rand(1000000)
%timeit sum(big_array)
%timeit np.sum(big_array)
```

    264 ms ± 15 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
    2.52 ms ± 198 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
    


| Function Name        |     	NaN-safe Version      |        Description |
-----------------------|------------------------------|--------------------|
|np.sum |	np.nansum |	Compute sum of elements|
|np.prod	| np.nanprod	| Compute product of elements|  
|np.mean	|np.nanmean|	Compute mean of elements|
|p.std|	np.nanstd|	Compute standard deviation|
|np.var|	np.nanvar|	Compute variance|
|np.min|	np.nanmin|	Find minimum value|
|np.max|	np.nanmax|	Find maximum value|
|np.argmin|	np.nanargmin|	Find index of minimum value|
|np.argmax|	np.nanargmax|	Find index of maximum value|
|np.median|	np.nanmedian|	Compute median of elements|
|np.percentile|	np.nanpercentile|	Compute rank-based statistics of elements|
|np.any|	N/A|	Evaluate whether any elements are true|
|np.all|	N/A|	Evaluate whether all elements are true|


# BroadCasting


#### Rules of Broadcasting
Broadcasting in NumPy follows a strict set of rules to determine the interaction between the two arrays:

- Rule 1: If the two arrays differ in their number of dimensions, the shape of the one with fewer dimensions is padded with ones on its leading (left) side.
- Rule 2: If the shape of the two arrays does not match in any dimension, the array with shape equal to 1 in that dimension is stretched to match the other shape.
- Rule 3: If in any dimension the sizes disagree and neither is equal to 1, an error is raised.

M = np.ones((2, 3))  
a = np.arange(3)  
- Let's consider an operation on these two arrays. The shape of the arrays are

M.shape = (2, 3)  
a.shape = (3,)  
- We see by rule 1 that the array a has fewer dimensions, so we pad it on the left with ones:

M.shape -> (2, 3)  
a.shape -> (1, 3)  
- By rule 2, we now see that the first dimension disagrees, so we stretch this dimension to match:

M.shape -> (2, 3)  
a.shape -> (2, 3)  
- The shapes match, and we see that the final shape will be (2, 3):

M = np.ones((3, 2))  
a = np.arange(3)  
- This is just a slightly different situation than in the first example: the matrix M is transposed. How does this affect the calculation? The shape of the arrays are

M.shape = (3, 2)  
a.shape = (3,)  
- Again, rule 1 tells us that we must pad the shape of a with ones:

M.shape -> (3, 2)  
a.shape -> (1, 3)  
- By rule 2, the first dimension of a is stretched to match that of M:

M.shape -> (3, 2)  
a.shape -> (3, 3)  
- Now we hit rule 3–the final shapes do not match, so these two arrays are incompatible, as we can observe by attempting this operation:

#### Practice of broadcasting



```python
#Lets say we have 10 sample which measure three hight of three flower, so we need an array of 10 rows and 3 column

#x = np.random.randint(1,50,size=30).reshape(10,3)
x= np.random.random((10,3))
#print(x)

# to know the mean hight of each flower
y= np.empty(3)
np.mean(x,axis =0,out=y)  # axis zero mean row wise sum
print(y)

# to verify if mean is correct, we all know sum of( mean-point ) is always 0 when all point are between 0,1

xcentered= x-y
print(xcentered.mean(0))
```

    [0.4368809  0.58307355 0.53017212]
    [ 0.00000000e+00 -4.44089210e-17  2.22044605e-17]
    


```python

```
