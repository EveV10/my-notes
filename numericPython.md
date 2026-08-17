# packages must be 1) installed in the computer; 2) invoked (imported) into the session

import numpy as np #where np is an abbreviation for easier referencing
# Create a 1D array (vector)

x = np.array ([3, 4, 5])

y = np.array ([4, 9, 7])

x + y

#new question 
# Data Types:
# function type() can be used to check the type of an object in Python


type(x)  # This will show the type of the object x
type(y)  # This will show the type of the object y
type(x + y)  # This will show the type of the result of the addition

w = [1,2,3]  # This is a Python list
z = [4,5,6]  # Another Python list

type(w + z)  # This will concatenate the two lists, not add them element-wise

# In Numpy, the type of an array can be checked using the .dtype attribute
x.dtype

#matrices 
#lists do not have a data type (.dtype) but they do have a type (type[matrix])
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
matrix.dtype
type[matrix]

matrix = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
matrix.dtype
type[matrix]

matrix.ndim
matrix.shape

array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
# Dimensions of the matrix

matrix.ndim
matrix.dtype

np.array ([[1 , 2], [3.0 , 4]]).shape

#methods
x = [1, 2, 3, 4, 5]
x

sum(x)

y= np.array(x)
type(y.sum())
print(sum(y))

#reshaping 
x = np.array ([1, 2, 3, 4, 5, 6])
x.shape

y= x.reshape(3, 2)
y.shape

#indexing 
#used to filter data
print(y[0, 0])
y

print(y[1,1])

print(y[0:2,])
y
y[1,1]=8

#transpose 
y.T

np.round(np.sqrt(y),2)
y**2
y

y^2

#sequence of values
# Create a sequence of numbers:
x= np.arange (16) # indexes in Python start at 0 
type(x)

y= x.reshape(4,4).T
y
y[1:4,:]

#boolean 
i= np.zeros(16, dtype=bool)

i= i.reshape(4,4)

i[:, [1,3]]= True
i

y[i]
