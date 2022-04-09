# Pandas 
pandas is a Python package providing fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive.

to import pandas we use `import pandas as pd` 

### Object creation
to create a series s in pandas we use `s = pd.Series([1,7,pd.nan,13])`, the output of this s series is the numbers 1,7,NaN,13.

we can creat a dataframe by passing a NumPy array , `dates= pd.date_range("20130101", periods=6)`, this will return a list of the dates between 2013-01-01 and 2013-01-06 

you can use dates in as index as following `df=pd.DateFrame(np.random.randn(6,4), index=dates, columns = list("abcd"))`, this will create a table with  6 rows and 4 columns , filled will random numbers, and dates is its index

### Viewing data

DataFrame.to_numpy() gives a NumPy representation of the underlying data. Note that this can be an expensive operation when your DataFrame has columns with different data types, which comes down to a fundamental difference between pandas and NumPy: NumPy arrays have one dtype for the entire array, while pandas DataFrames have one dtype per column. When you call DataFrame.to_numpy(), pandas will find the NumPy dtype that can hold all of the dtypes in the DataFrame. This may end up being object, which requires casting every value to a Python object.

use `.discribe()` to get a summery of the data, use `.T` to transpos the data. with `.sort_index(axis=1, ascending= False)` you can sort the data by index, or use `df.sort_values(by="col_name")` to sort the data by the values in col_name

### Getting
Selecting a single column, which yields a Series, `df[col_name]`, or you can use d`df[:3]` to select the first three rows, or `df["value1":"value2"]` to select rows by values of index.

to select by lable use `df.loc[dates[0]]`, and to select multi axis use `df.loc[:,["col1","col2"]]` this will select data in columns 1 and 2.

to slice data we can use `df.loc[index_value1: index_value2, ["col1","col2"]]` , this will show data in col 1 and two ranging between index values 1 and 2.

### selection by position 
you can select by posistion using `df.iloc[index]` , this will show the row of index in the dataframe

you can slice the data in the form of `df.iloc[index1:index2, col1:col2]`, this will show the data ranging between row of index 1 and and 2 , and between columns 1 and 2. inseted of range you can select the index by inseerting a list `.iloc[[indx1,indx2,indx3],[col_indx1,col_indx2,col_indx3]]`, to slice rows or columns explicitly use [indx1:indx2, :] and [:,col_indx1:col_indx2]

### boolean indexing
you can use conditions to index `df[df[col]>value]`, we can use `df[df[col].isin([value1,value2])] to show the data where the values in col euqal value1 and value2 only .

