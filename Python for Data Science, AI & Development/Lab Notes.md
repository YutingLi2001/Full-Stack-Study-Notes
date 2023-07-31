# Practice Lab: Selecting data in a Dataframe

## Exercise 1: Pandas: DataFrame and Series 

### Problem 1: Create a dataframe to display the result as below:
```python
a = {'Student':['David', 'Samuel', 'Terry', 'Evan'],
     'Age':['27', '24', '22', '32'],
     'Country':['UK', 'Canada', 'China', 'USA'],
     'Course':['Python','Data Structures','Machine Learning','Web Development'],
     'Marks':['85','72','89','76']}

# casting the dictionaary to a DataFrame
df1 = pd.DataFrame(a)
# display the dataset
df1
```

### Problem 2: Retrieve the Marks column and assign it to a variable b
```python
b = df1[['Marks']]
b
```

### Problem 3: Retrieve the Country and Course columns and assign it to a variable c
```python
c = df1[['Country','Course']]
c
```

## Exercise 2: `loc()` and `iloc()` functions 

### Problem 1: Use the <code>loc()</code> function, to get the Department of Jane in the newly created dataframe df2.

```python
df2.loc['Jane','Department']
```

### Problem 2: Use the <code>iloc()</code> function to get the Salary of Mary in the newly created dataframe df2.

```python
df2.iloc[3,2]
```

# 1D Numpy in Python

## 