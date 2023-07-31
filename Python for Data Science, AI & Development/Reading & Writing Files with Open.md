# Introduction to Pandas Library in Python

## What is Pandas?

Pandas is an open-source library in Python that provides data manipulation and analysis capabilities. It is built on top of two core Python libraries - Matplotlib for data visualization and NumPy for mathematical operations.

## Importing Pandas

To use Pandas, we first need to import it. We use the `import` command, followed by the name of the library. To make things easier, we can give Pandas a nickname using the `as` statement:

```python
import pandas as pd
```

Now, we can access all the functions of Pandas using the abbreviation `pd`.

## Loading Data with Pandas

Pandas provides several functions to read data in different formats. Here's how we can load a CSV (Comma Separated Values) file:

```python
df = pd.read_csv("path_to_your_file.csv")
```

The `read_csv` function reads the CSV file located at the specified path and loads it into a DataFrame, a 2-dimensional labeled data structure with columns of potentially different types.

We can use the `head()` function to display the first five rows of the DataFrame:

```python
df.head()
```

Similarly, to load an Excel file, we can use the `read_excel` function:

```python
df = pd.read_excel("path_to_your_file.xlsx")
```

## Creating DataFrames

- A data frame is comprised of rows and columns.
- We can create a DataFrame from a dictionary as well. The keys of the dictionary become the column names and the values become the data in the rows.

```python
data = {
    "Name": ["John", "Anna", "Peter"],
    "Age": [23, 20, 22]
}
df = pd.DataFrame(data)
```

## Subsetting DataFrames

Pandas also allows us to create new DataFrames from an existing one:

- To create a DataFrame with a single column:

```python
new_df = df[["column_name"]]
```

- To create a DataFrame with multiple columns:

```python
new_df = df[["column1_name", "column2_name"]]
```

In both these examples, `new_df` will be a new DataFrame consisting of the specified columns from the original DataFrame `df`.

# Working with DataFrames in Pandas

## Finding Unique Values

With Pandas, it's easy to find unique values in a column of a DataFrame. For example, if we want to find all unique years in a 'released' column of our DataFrame, we can use the `unique()` method:

```python
unique_years = df['released'].unique()
```

The `unique()` method will return all unique values present in the specified column.

## Filtering Data

Pandas allows us to filter our data based on specific conditions. For instance, if we want to create a new DataFrame that only contains albums released after 1979, we can do this in one line:

```python
df1 = df[df['released'] > 1979]
```

## Saving DataFrames

After manipulating our data, we can save the results in a variety of formats using different methods. If we want to save our new DataFrame `df1` as a CSV file, we can use the `to_csv()` method:

```python
df1.to_csv('new_dataset.csv')
```

This line of code saves the DataFrame `df1` as a CSV file named 'new_dataset.csv' in the current working directory.



# Numpy in 1D

## Introduction
- Numpy is a library for scientific computing. 
- It provides many useful functions, advantages like speed, memory efficiency, and it's the basis for pandas.

## Basics and Array Creation

### Python Lists vs. Numpy Arrays
- A Python list is a container that allows you to store and access data. Each element is associated with an index.
- A numpy array (ND array) is similar to a list but usually fixed in size and each element is of the same type.

```python
import numpy as np
a = np.array([0, 1, 2, 3, 4])
```

### Numpy Array Attributes
- `dtype` - Data type of the array's elements.
- `size` - Number of elements in the array.
- `ndim` - Number of array dimensions or the rank of the array.
- `shape` - A tuple of integers indicating the size of the array in each dimension.

## Indexing and Slicing
- Like lists, Numpy arrays can be indexed and sliced to access or change elements.

```python
a[0] = 100 # Change the first element to 100
d = a[1:4] # Slice the array from index 1 to 3

# Slicing in [start:end:step]
arr = np.array([1, 2, 3, 4, 5, 6, 7])

print(arr[1:5:2])
# Output: [2 4]

```

## Basic Operations
- Numpy allows easy and efficient mathematical operations on arrays including vector addition, subtraction, scalar multiplication, Hadamard product, and dot product.

```python
u = np.array([1, 0])
v = np.array([0, 1])
z = u + v # vector addition
z = u - v # vector subtraction
y = np.array([1, 2])
y = 2 * y # scalar multiplication
z = u * v # Hadamard product
result = np.dot(u, v) # dot product
```

```python
import numpy as np

# Create two vectors
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Compute the dot product
dot_product = np.dot(a, b)
print(dot_product)  # Output: 32 (1*4 + 2*5 + 3*6)
```


## Broadcasting
- Broadcasting is a feature that allows numpy to work with arrays of different shapes. It extends smaller arrays to match the shape of larger ones.

```python
u = np.array([1, 2, 3, 4, 5])
u = u + 1 # add 1 to each element in the array
```

## Universal Functions
- Universal functions in numpy are simple mathematical functions that are applied elementwise on array(s).

```python
a = np.array([0, 1, 0, 1, 0])
mean_a = a.mean() # calculate the mean of a
```

## Creating Functions for Numpy Arrays
- You can create functions that map numpy arrays to new numpy arrays.

```python
x = np.array([0, np.pi/2 , np.pi])
y = np.sin(x) # apply sin function to each element in x
```

## Line Space Function
- `np.linspace` returns evenly spaced numbers over a specified interval.

```python
np.linspace(-2, 2, num=5)
# result: -2,-1,0,1,2,
```

## Plotting Mathematical Functions
- Numpy can be used with Matplotlib to plot mathematical functions.

```python
import matplotlib.pyplot as plt
x = np.linspace(0, 2*np.pi, 100)
y = np.sin(x)

# The first input corresponds to the values for the horizontal or x-axis
# The second input coresponds to the values for the vertical or y-axis
plt.plot(x, y)
```



# 2D Numpy Arrays Notes

## Basics and Array Creation

- Numpy can handle multi-dimensional arrays. This section focuses on 2D arrays.
- Consider a nested list `a`. It can be converted into a numpy array.
- Each nested list corresponds to a different row of the array (or matrix).
- Numpy arrays can be visualized as rectangular arrays.
  
## Array Attributes

- `ndim`: Returns the number of dimensions (or axes) of the array. Also known as the rank. This does not refer to the number of linearly independent columns like a matrix.
- `shape`: Returns a tuple representing the dimensionality of the array. The first element is the number of rows and the second is the number of columns.
- `size`: Returns the total number of elements in the array.

```python
import numpy as np

# a is a nested list
a = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Convert list to numpy array
arr = np.array(a)

# Get array attributes
print(arr.ndim) # Output: 2
print(arr.shape) # Output: (3, 3)
print(arr.size) # Output: 9
```

## Indexing and Slicing

- The first bracket accesses the different rows in the array.
- The second bracket accesses the elements within a particular row.
- A single bracket can be used to access elements as well.
- Slicing works similarly to 1D arrays but now you have to account for rows and columns.

```python
# Accessing element at second row and third column
print(arr[1, 2]) # Output: 6

# Accessing first row and first two columns
print(arr[0, :2]) # Output: array([1, 2])

# Accessing first two rows and last column
print(arr[:2, -1]) # Output: array([3, 6])
```

## Basic Operations

- Arrays can be added and the process is identical to matrix addition.
- Multiplication by a scalar is identical to multiplying a matrix by a scalar.
- Multiplication of two arrays corresponds to an element-wise product, also known as Hadamard product.
- Matrix multiplication is also possible with numpy arrays.

```python
# Define another array
b = np.array([[10, 11, 12], [13, 14, 15], [16, 17, 18]])

# Addition of arrays
print(arr + b)

# Multiplication by scalar
print(2 * arr)

# Hadamard product
print(arr * b)

# Matrix multiplication
print(np.dot(arr, b))
```

