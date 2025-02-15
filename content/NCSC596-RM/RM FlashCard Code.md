
#flashcards/Pandas_Basics
QUESTION: What are the two primary data structures provided by the Pandas library?
OPTIONS:
A) Lists and Dictionaries
B) Series and DataFrames
C) Arrays and Tuples
D) Sets and Matrices
??
SOLUTION:
B) Series and DataFrames
Pandas is built around these two fundamental data structures. Series are one-dimensional labeled arrays, and DataFrames are two-dimensional labeled data structures.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Series
QUESTION: Create a Pandas Series from the following dictionary:  `data = {'a': 10, 'b': 20, 'c': 30}`.
OPTIONS:
A) `pd.Series({'a': 10, 'b': 20, 'c': 30})`
B) `pd.DataFrame(data)`
C) `pd.Series(data.values())`
D) `pd.Series(data, index=['x', 'y', 'z'])`
??
SOLUTION:
A) `pd.Series({'a': 10, 'b': 20, 'c': 30})`
When a dictionary is passed to `pd.Series()`, the keys become the index and the values become the data.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_DataFrame
QUESTION:  How can you display the top 5 rows of a Pandas DataFrame named `df`?
OPTIONS:
A) `df.top(5)`
B) `df.head(5)`
C) `df.first(5)`
D) `df.show(5)`
??
SOLUTION:
B) `df.head(5)`
The `head()` method is used to display the first n rows of a DataFrame. The default is 5 if no number is specified.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_DataFrame_Info
QUESTION: Which method provides a concise summary of a DataFrame, including data types and non-null values?
OPTIONS:
A) `df.describe()`
B) `df.info()`
C) `df.summary()`**
D) `df.inspect()`
??
SOLUTION:
B) `df.info()`
The `info()` method prints information about the DataFrame, such as the number of rows, columns, data types, and memory usage.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Selection
QUESTION:  Given a DataFrame `df` with columns 'Name' and 'Age', how do you select only the 'Age' column?
OPTIONS:
A) `df.Age`
B) `df['Age']`
*C*) `df.loc['Age']`
D) Both A and B
??
SOLUTION:
D) Both A and B
Both `df.Age` (attribute access) and `df['Age']` (bracket notation) can be used to select a single column.  Bracket notation is generally preferred as it handles column names with spaces or special characters.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Filtering
QUESTION:  How do you filter a DataFrame `df` to select rows where the 'Age' column is greater than 30?
OPTIONS:
A) `df[df.Age > 30]`
B) `df[df['Age'] > 30]`
C) `df.filter(Age > 30)`
D) Both A and B
??
SOLUTION:
D) Both A and B
Boolean indexing is used for filtering. The condition `df['Age'] > 30` creates a Boolean Series, which is then used to select rows where the condition is True.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Missing_Data
QUESTION:  How can you fill missing values (NaN) in a DataFrame `df` with the value 0?
OPTIONS:
A) `df.fill(0)`
B) `df.fillna(0)`
C) `df.replaceNaN(0)`
D) `df.missing(0)`
??
SOLUTION:
B) `df.fillna(0)`
The `fillna()` method is used to replace NaN values with a specified value or using a specified method (e.g., forward fill, backward fill).
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_IO
QUESTION:  What function is used to read data from a CSV file into a Pandas DataFrame?
OPTIONS:
A) `pd.read_csv()`
B) `pd.load_csv()`
C) `pd.import_csv()`
D) `pd.from_csv()`
??
SOLUTION:
A) `pd.read_csv()`
`pd.read_csv()` is the standard function for reading comma-separated value files.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_IO_Writing
QUESTION: What method is used to save a DataFrame to a CSV file? Use `df` as the DataFrame name and 'output.csv' as the file name.
OPTIONS:
A) `df.write_csv('output.csv')`
B) `df.to_csv('output.csv')`
C) `df.save_csv('output.csv')`
D) `pd.save(df, 'output.csv')`
??
SOLUTION:
B) `df.to_csv('output.csv')`
    `df.to_csv()` writes the DataFrame to a CSV file. The `index=False` argument can be used to prevent writing the index.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Concatenation
QUESTION: You have two DataFrames, `df1` and `df2`.  How do you concatenate them vertically (stack them on top of each other)?
OPTIONS:
A) `pd.concat([df1, df2], axis=1)`
B) `pd.concat([df1, df2], axis=0)`
C) `pd.merge([df1, df2])`
D) `df1.append(df2)`
??
SOLUTION:
B) `pd.concat([df1, df2], axis=0)`
`pd.concat()` with `axis=0` concatenates along the row axis (vertically).
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Merging
QUESTION: What function is used to perform database-style joins on DataFrames in Pandas?
OPTIONS:
 A) `pd.join()`
 B) `pd.merge()`
 C) `pd.combine()`
 D) `pd.concat()`
??
SOLUTION:
 B) `pd.merge()`
 `pd.merge()` is used for SQL-like joins based on common columns or indices.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_GroupBy
QUESTION:  How would you group a DataFrame `df` by the 'Category' column and calculate the sum of the 'Value' column for each category?
OPTIONS:
A) `df.groupby('Category').sum('Value')`
B) `df.group('Category').sum()['Value']`
C) `df.groupby('Category')['Value'].sum()`
D) `df.groupby('Category').aggregate('Value', 'sum')`
??
SOLUTION:
C) `df.groupby('Category')['Value'].sum()`
This groups the DataFrame by 'Category', then selects the 'Value' column, and finally calculates the sum for each group.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Apply
QUESTION:  Apply the function `lambda x: x * 2` to every element in the 'Value' column of DataFrame df.
OPTIONS:
A) df['Value'].apply(lambda x: x*2)
B) df.apply(lambda x: x*2, column='Value')
C) df['Value'].map(lambda x: x*2)
D) Both A and C
??
SOLUTION:
D) Both A and C
Both `apply()` and `map` can be used on a Series to apply a function element-wise.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Dates
QUESTION: What is the correct Pandas function and its arguments to generate a sequence of 5 daily dates starting from '2025-01-01'?
OPTIONS:
A) `pd.date_range(start='2025-01-01', end='2025-01-05', freq='D')`
B) `pd.date_range(start='2025-01-01', periods=5, freq='D')`
C) `pd.date_range('2025-01-01', '2025-01-05')`
D) `pd.dates('2025-01-01', 5)`
??
SOLUTION:
B) `pd.date_range(start='2025-01-01', periods=5, freq='D')`
`pd.date_range()` creates a fixed-frequency DatetimeIndex. `start` defines the start date, `periods` the number of periods, and `freq='D'` specifies daily frequency.
<!--SR:!2025-02-18,4,270-->

#flashcards/Pandas_Time_Series
QUESTION:  Given a DataFrame `df` with a datetime index, how do you resample the data to a monthly frequency, calculating the mean of each month?
OPTIONS:
 A) `df.resample('M').mean()`
 B) `df.monthly().mean()`
 C) `df.groupby(pd.Grouper(freq='M')).mean()`
 D) Both A and C
??
SOLUTION:
 D) Both A and C
 `resample('M')` groups the data by month.  `.mean()` then calculates the mean for each month. The Grouper option provides the same.
<!--SR:!2025-02-18,4,270-->

#flashcards/NumPy_Basics
QUESTION:  What is the primary data structure in NumPy?
OPTIONS:
A) List
B) ndarray
C) Tuple
D) Dictionary
??
SOLUTION:
B) ndarray
The ndarray (n-dimensional array) is the core of NumPy, providing efficient storage and operations on numerical data.
<!--SR:!2025-02-18,4,270-->

#flashcards/NumPy_Creation
QUESTION: Create a NumPy array of shape (2, 3) filled with zeros.
OPTIONS:
A) `np.array([2, 3])`
B) `np.zeros(2, 3)`
C) `np.zeros((2, 3))`
D) `np.empty((2, 3))`
??
SOLUTION:
C) `np.zeros((2, 3))`
`np.zeros()` creates an array filled with zeros. The shape is specified as a tuple.
<!--SR:!2025-02-18,4,270-->

#flashcards/NumPy_Attributes
QUESTION:  What attribute of a NumPy array gives you the number of elements in the array?
OPTIONS:
A) shape
B) size
C) dtype
D) nbytes
??
SOLUTION:
B) size
The `size` attribute returns the total number of elements in the array.
<!--SR:!2025-02-18,4,270-->

#flashcards/NumPy_Slicing
QUESTION: Given a NumPy array `arr = np.arange(10)`, how would you select the elements from index 2 up to (but not including) index 7?
OPTIONS:
A) `arr[2:7]`
B) `arr[2, 7]`
C) `arr[2-7]`
D) `arr[2 to 7]`
??
SOLUTION:
A) `arr[2:7]`
This uses standard Python slicing notation.
<!--SR:!2025-02-18,4,270-->

#flashcards/NumPy_Broadcasting
QUESTION:  If you add a scalar value of 5 to a NumPy array, what happens due to broadcasting?
OPTIONS:
A) An error occurs.
B) The value 5 is added to only the first element.
C) The value 5 is added to every element of the array.
D) The array is multiplied by 5.
??
SOLUTION:
C) The value 5 is added to every element of the array.
Broadcasting "stretches" the scalar to match the shape of the array, allowing element-wise addition.

#flashcards/NumPy_Linear_Algebra
QUESTION: How do you calculate the dot product of two NumPy arrays, `A` and `B`?
OPTIONS:
A) `A * B`
B) `A.dot(B)`
C) `np.dot(A, B)`
D) Both B and C
??
SOLUTION:
D) Both B and C
Both `A.dot(B)` (method call) and `np.dot(A, B)` (function call) compute the dot product.  The `@` operator can also be used (`A @ B`).

#flashcards/NumPy_Statistical_Methods
QUESTION: How to calculate the standard deviation of values in a NumPy array named `arr`?
OPTIONS:
    A) `arr.std()`
    B) `np.std(arr)`
    C) `arr.standard_deviation()`
    D) Both A and B
??
SOLUTION:
    D) Both A and B
    Both `arr.std()` and `np.std(arr)` calculates the standard deviation.

#flashcards/NumPy_Random
QUESTION: Generate a 2x2 NumPy array with random numbers drawn from a standard normal distribution.
OPTIONS:
A) `np.random.rand(2, 2)`
B) `np.random.randn(2, 2)`
C) `np.random.normal(2, 2)`
D) `np.random.uniform(2, 2)`
??
SOLUTION:
B) `np.random.randn(2, 2)`
`randn` generates samples from the standard normal distribution (mean 0, variance 1).

#flashcards/NumPy_Axis
QUESTION:  In a 2D NumPy array, what does `axis=0` typically refer to?
OPTIONS:
A) Columns
B) Rows
C) Depth
D) Diagonal
??
SOLUTION:
B) Rows
`axis=0` refers to operations *down* the rows (e.g., summing each column).

#flashcards/Matplotlib_Basics
QUESTION:  What function is used to display a plot in Matplotlib?
OPTIONS:
A) `plt.display()`
B) `plt.show()`
C) `plt.render()`
D) `plt.plot()`
??
SOLUTION:
B) `plt.show()`
`plt.show()` is essential to display the created plot.

#flashcards/Matplotlib_Line_Plot
QUESTION: Create a simple line plot with x-values [1, 2, 3] and y-values [4, 5, 6].
OPTIONS:
A) `plt.line([1, 2, 3], [4, 5, 6])`
B) `plt.plot([1, 2, 3], [4, 5, 6])`
C) `plt.scatter([1, 2, 3], [4, 5, 6])`
D) `plt.draw([1, 2, 3], [4, 5, 6])`
??
SOLUTION:
B) `plt.plot([1, 2, 3], [4, 5, 6])`
`plt.plot()` is the primary function for creating line plots.

#flashcards/Matplotlib_Scatter_Plot
QUESTION:  How do you create a scatter plot in Matplotlib using `plt`?
OPTIONS:
A) `plt.line(x, y)`
B) `plt.scatter(x, y)`
C) `plt.plot(x, y, 'o')`
D) Both B and C
??
SOLUTION:
D) Both B and C
Both `plt.scatter(x, y)` and `plt.plot(x, y, 'o')` create scatter plots.  `plt.scatter` offers more control over marker properties.

#flashcards/Matplotlib_Subplots
QUESTION: How would you create a figure with two subplots arranged vertically (one above the other)?
OPTIONS:
A)  `plt.subplots(2, 1)`
B)  `plt.subplot(2, 1)`
C)  `plt.figure(2)`
D)  `plt.plot(2, 1)`
??
SOLUTION:
A) `plt.subplots(2, 1)`
`plt.subplots(nrows, ncols)` creates a figure and a grid of subplots.

#flashcards/Matplotlib_Customization
QUESTION: How do you set the title of a plot in Matplotlib, using the `plt` interface?
OPTIONS:
 A) `plt.title = "My Title"`
 B) `plt.set_title("My Title")`
 C) `plt.title("My Title")`
 D) `plt.plot(title="My Title")`
??
SOLUTION:
 C) `plt.title("My Title")`
 `plt.title()` sets the title of the current axes.

 #flashcards/Matplotlib_Saving
QUESTION: How can you save the current Matplotlib plot to a file named "my_plot.png"?
OPTIONS:
A) plt.save("my_plot.png")
B) plt.save_figure("my_plot.png")
C) plt.savefig("my_plot.png")
D) plt.export("my_plot.png")
??
SOLUTION:
C) plt.savefig("my_plot.png")
    `plt.savefig()` saves the current figure to a file. The file format is inferred from the extension.


#flashcards/Pandas_Series_Creation
QUESTION:  How can you create a Pandas Series with the values [1, 4, 9, 16] and the index ['a', 'b', 'c', 'd']?
OPTIONS:
A) `pd.Series([1, 4, 9, 16], index=['a', 'b', 'c', 'd'])`
B) `pd.Series(['a', 'b', 'c', 'd'], [1, 4, 9, 16])`
C) `pd.DataFrame({'values': [1, 4, 9, 16], 'index': ['a', 'b', 'c', 'd']})`
D) `pd.Series([1, 4, 9, 16], labels=['a', 'b', 'c', 'd'])`
??
SOLUTION:
A) `pd.Series([1, 4, 9, 16], index=['a', 'b', 'c', 'd'])`
This correctly passes the data and the index to the `pd.Series()` constructor.

#flashcards/Pandas_DataFrame_Creation
QUESTION: Create a Pandas DataFrame from the following dictionary: `data = {'col1': [1, 2], 'col2': [3, 4]}`.
OPTIONS:
A) `pd.Series(data)`
B) `pd.DataFrame(data)`
C) `pd.DataFrame([1, 2], [3, 4])`
D) `pd.DataFrame({'col1': [1, 2]}, {'col2': [3, 4]})`
??
SOLUTION:
B) `pd.DataFrame(data)`
Passing a dictionary to `pd.DataFrame()` creates a DataFrame where keys are column names and values are column data.

#flashcards/Pandas_DataFrame_Tail
QUESTION: How do you view the last 3 rows of a DataFrame named `my_dataframe`?
OPTIONS:
A) `my_dataframe.last(3)`
B) `my_dataframe.tail(3)`
C) `my_dataframe.bottom(3)`
D) `my_dataframe.end(3)`
??
SOLUTION:
B) `my_dataframe.tail(3)`
The `tail()` method displays the last n rows of a DataFrame.

#flashcards/Pandas_Selection_Multiple
QUESTION: Given a DataFrame `df` with columns 'A', 'B', and 'C', select columns 'A' and 'C'.
OPTIONS:
A) `df['A', 'C']`
B) `df[['A', 'C']]`
C) `df.loc['A', 'C']`
D) `df.iloc['A', 'C']`
??
SOLUTION:
B) `df[['A', 'C']]`
Using a list of column names within brackets selects multiple columns.

#flashcards/Pandas_iloc
QUESTION: How would you select the element in the second row and third column of a DataFrame `df` using integer-based indexing?
OPTIONS:
A) `df.loc[1, 2]`
B) `df.iloc[1, 2]`
C) `df[1, 2]`
D) `df.at[1, 2]`
??
SOLUTION:
B) `df.iloc[1, 2]`
`iloc` is used for integer-based indexing. Remember that indexing starts at 0.  So row 2 is index 1, and column 3 is index 2.

#flashcards/Pandas_loc
QUESTION: If a DataFrame `df` has row labels 'row1', 'row2', 'row3', and you want to select 'row2', how would you do it using label-based indexing?
OPTIONS:
A) `df.iloc['row2']`
B) `df.loc['row2']`
C) `df['row2']`
D) `df.ix['row2']`
??
SOLUTION:
B) `df.loc['row2']`
`loc` is used for label-based indexing.

#flashcards/Pandas_Filtering_Multiple
QUESTION:  Select rows from DataFrame `df` where 'Age' is greater than 25 AND 'City' is 'New York'.
OPTIONS:
A) `df[(df['Age'] > 25) & (df['City'] == 'New York')]`
B) `df[df['Age'] > 25 & df['City'] == 'New York']`
C) `df.filter(Age > 25 and City == 'New York')`
D) `df.query("Age > 25 and City == 'New York'")`
??
SOLUTION:
A) `df[(df['Age'] > 25) & (df['City'] == 'New York')]`
This uses boolean indexing with the `&` operator for combining conditions.  Parentheses are crucial for correct operator precedence.  Option D using `.query()` is also valid, but not mentioned in the provided PDF content.

#flashcards/Pandas_dropna
QUESTION: How to remove all rows with any missing values (NaN) from DataFrame named df_nan?
OPTIONS:
A) `df_nan.remove_na()`
B) `df_nan.dropna()`
C) `df_nan.fillna()`
D) `df_nan.delete(NaN)`
??
SOLUTION:
B) `df_nan.dropna()`
The `dropna()` method, by default, removes all rows containing at least one NaN value.

#flashcards/Pandas_to_excel
QUESTION:  You have a DataFrame `df`.  Save it to an Excel file named "data.xlsx" without including the index.
OPTIONS:
A) df.to_excel("data.xlsx", include_index=False)
B) df.to_excel("data.xlsx", index=False)
C) pd.save_excel(df, "data.xlsx")
D) df.write_excel("data.xlsx", index=False)
??
SOLUTION:
B) df.to_excel("data.xlsx", index=False)
`to_excel()` writes to an Excel file, and `index=False` prevents writing the index.

#flashcards/Pandas_read_excel
QUESTION: How to read sheet name 'Sheet2' from excel file 'data.xlsx' into DataFrame `df_excel`?
OPTIONS:
A) df_excel = pd.read_excel('data.xlsx', sheetname='Sheet2')
B) df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet2')
C) df_excel = pd.read_excel('data.xlsx', sheet='Sheet2')
D) df_excel = pd.read_excel('data.xlsx')[Sheet2]
??
SOLUTION:
B) df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet2')
The argument `sheet_name` takes a string for sheet name, an integer for sheet index, a list of sheet names, or None (default reads the first sheet).

#flashcards/Pandas_concat_axis1
QUESTION: What is the result of `pd.concat([df1, df2], axis=1)` if `df1` and `df2` are DataFrames?
OPTIONS:
A) `df1` and `df2` are stacked vertically.
B) `df1` and `df2` are joined side-by-side (column-wise).
C) An error occurs.
D) The DataFrames are merged based on a common column.
??
SOLUTION:
B) `df1` and `df2` are joined side-by-side (column-wise).
`axis=1` in `pd.concat()` performs concatenation along columns.

#flashcards/Pandas_merge_how
QUESTION: In `pd.merge(df1, df2, on='key', how='left')`, what does `how='left'` specify?
OPTIONS:
A) An inner join
B) A right join
C) A left join
D) An outer join
??
SOLUTION:
C) A left join
`how='left'` uses only the keys from the left DataFrame (`df1` in this case), similar to a SQL left outer join.

#flashcards/Pandas_groupby_multiple
QUESTION:  Group DataFrame `df` by 'Col1' and 'Col2', then calculate the mean of 'Col3' for each group.
OPTIONS:
A) `df.groupby(['Col1', 'Col2']).mean()['Col3']`
B) `df.groupby('Col1', 'Col2').mean('Col3')`
C) `df.groupby(['Col1', 'Col2'])['Col3'].mean()`
D) Both A and C are incorrect
??
SOLUTION:
C) `df.groupby(['Col1', 'Col2'])['Col3'].mean()`
This groups by the specified columns, selects 'Col3', and then computes the mean.

#flashcards/Pandas_Date_range_frequency
QUESTION: Which frequency string should be used with `pd.date_range` to generate a range of dates representing the *last* day of each month?
OPTIONS:
A) 'MS'
B) 'M'
C) 'D'
D) 'W'
??
SOLUTION:
B) 'M'
'M' represents month end frequency.

#flashcards/Pandas_Date_range_timezone
QUESTION: How to create a date range with timezone set to 'UTC' using pd.date_range?
OPTIONS:
A) Set timezone parameter
B) Set tz parameter to 'UTC'
C) Set time_zone parameter
D) It is not possible
??
SOLUTION:
B) Set tz parameter to 'UTC'
pd.date_range(start='2024-01-01', periods=5, freq='D', tz='UTC')

#flashcards/NumPy_Array_Creation_arange
QUESTION:  Create a NumPy array containing the sequence of numbers from 5 to 15 (exclusive) with a step of 2.
OPTIONS:
A) `np.arange(5, 15, 2)`
B) `np.linspace(5, 15, 2)`
C) `np.array(5, 15, 2)`
D) `np.range(5, 15, 2)`
??
SOLUTION:
A) `np.arange(5, 15, 2)`
`np.arange(start, stop, step)` generates a sequence.

#flashcards/NumPy_reshape
QUESTION:  You have a 1D NumPy array `arr` with 12 elements. Reshape it into a 3x4 2D array.
OPTIONS:
A) `arr.reshape(4, 3)`
B) `arr.resize(3, 4)`
C) `arr.reshape(3, 4)`
D) `np.reshape(arr, 3, 4)`
??
SOLUTION:
C) `arr.reshape(3, 4)`
The `reshape()` method returns a new array with the specified shape.

#flashcards/NumPy_Boolean_Indexing
QUESTION: Given `arr = np.array([1, 2, 3, 4, 5])`, how would you select elements greater than 2?
OPTIONS:
A) `arr[arr > 2]`
B) `arr.select(arr > 2)`
C) `arr[arr.greater_than(2)]`
D) `arr(arr > 2)`
??
SOLUTION:
A) `arr[arr > 2]`
This uses a boolean array (`arr > 2`) as an index to select elements where the condition is True.

#flashcards/NumPy_Linear_Algebra_Inverse
QUESTION: How do you find the inverse of a square matrix `A` in NumPy?
OPTIONS:
A) `A.inverse()`
B) `np.linalg.inv(A)`
C) `A.invert()`
D) `np.inverse(A)`
??
SOLUTION:
B) `np.linalg.inv(A)`
The `np.linalg.inv()` function computes the matrix inverse.

#flashcards/NumPy_ufunc
QUESTION: What is a NumPy "universal function" (ufunc)?
OPTIONS:
A) A function that operates on ndarrays element-by-element.
B) A function that can only handle 1D arrays.
C) A function that converts lists to arrays.
D) A function for generating random numbers.
??
SOLUTION:
A) A function that operates on ndarrays element-by-element.
Ufuncs (e.g., `np.sin`, `np.exp`, `np.add`) are vectorized functions that apply operations efficiently to each element of an array.

#flashcards/NumPy_mean_axis
QUESTION: Calculate the mean of each *column* in a 2D NumPy array `my_array`.
OPTIONS:
A) `np.mean(my_array, axis=0)`
B) `np.mean(my_array, axis=1)`
C) `my_array.mean(columns=True)`
D) `my_array.mean(axis=columns)`
??
SOLUTION:
A) `np.mean(my_array, axis=0)`
`axis=0` specifies that the mean should be computed along the rows (resulting in a mean for each column).

#flashcards/NumPy_random_seed
QUESTION: What is the purpose of `np.random.seed(42)`?
OPTIONS:
A) Generates a random number between 0 and 42.
B) Sets the size of random arrays to 42.
C) Ensures reproducibility of random number generation.
D) Creates an array with 42 random elements.
??
SOLUTION:
C) Ensures reproducibility of random number generation.
Setting the seed allows you to get the same sequence of "random" numbers each time the code is run.

#flashcards/NumPy_linspace
QUESTION: Generate 5 evenly spaced numbers between 0 and 1 (inclusive) using NumPy.
OPTIONS:
 A) `np.arange(0, 1, 5)`
 B) `np.linspace(0, 1, 5)`
 C) `np.random(0, 1, 5)`
 D) `np.array([0, 0.25, 0.5, 0.75, 1])`
??
SOLUTION:
 B) `np.linspace(0, 1, 5)`
 `np.linspace(start, stop, num)` generates `num` evenly spaced samples.

#flashcards/Matplotlib_Figure_Axes
QUESTION: Explain the relationship between "figure" and "axes" in Matplotlib.
OPTIONS:
A) They are the same thing.
B) A figure can contain multiple axes, and axes are where the plots are drawn.
C) An axes can contain multiple figures.
D) Axes are used for 3D plots, while figures are for 2D plots.
??
SOLUTION:
B) A figure can contain multiple axes, and axes are where the plots are drawn.
The figure is the top-level container; axes are individual plots within the figure.

#flashcards/Matplotlib_Labels
QUESTION: Add x and y axis labels to a plot using the object-oriented interface with an `axes` object named `ax`.
OPTIONS:
A) `ax.xlabel("X Label"); ax.ylabel("Y Label")`
B) `ax.set_xlabels("X Label"); ax.set_ylabels("Y Label")`
C) `ax.set_xlabel("X Label"); ax.set_ylabel("Y Label")`
D) `plt.xlabel("X Label", ax); plt.ylabel("Y Label", ax)`
??
SOLUTION:
C) `ax.set_xlabel("X Label"); ax.set_ylabel("Y Label")`
The `set_xlabel` and `set_ylabel` methods are used with the axes object.

#flashcards/Matplotlib_Legends
QUESTION: Add a legend to a plot using the object-oriented interface with an axes object called `ax`.
OPTIONS:
A) ax.add_legend()
B) ax.legend()
C) plt.legend(ax)
D) ax.show_legend()
??
SOLUTION:
B) ax.legend()
The legend() method displays the legend on the specified axes. The labels are usually defined within the plot() call.

#flashcards/Matplotlib_grid
QUESTION: How to add grid lines to your plot using the `plt` interface?
OPTIONS:
A) `plt.gridlines()`
B) `plt.grid(True)`
C) `plt.show_grid()`
D) `plt.axes().grid()`
??
SOLUTION:
B) `plt.grid(True)`
`plt.grid(True)` enables grid lines; `plt.grid(False)` disables them.

#flashcards/Matplotlib_styles
QUESTION: Change the plot style to the 'ggplot' style.
OPTIONS:
 A)  `plt.style('ggplot')`
 B)  `plt.set_style('ggplot')`
 C) `plt.style.use('ggplot')`
 D)  `plt.rc('style', 'ggplot')`
??
SOLUTION:
 C) `plt.style.use('ggplot')`
 `plt.style.use()` sets the plotting style.

#flashcards/Matplotlib_twinx
QUESTION: What is the purpose of the `twinx()` method in Matplotlib?
OPTIONS:
 A) To create a copy of the current plot.
 B) To create a second axes that shares the x-axis, allowing plots with different y-scales.
 C) To create a second axes that shares the y-axis.
 D) To zoom in on a section of the plot.
??
SOLUTION:
 B) To create a second axes that shares the x-axis, allowing plots with different y-scales.
 `twinx()` is useful for plotting two datasets with the same x-values but different y-ranges.

#flashcards/Matplotlib_tight_layout
QUESTION: What does `plt.tight_layout()` do?
OPTIONS:
A) Compresses the plot image file size.
B) Automatically adjusts subplot parameters to provide reasonable spacing.
C) Makes the plot lines thicker.
D) Removes whitespace around the figure.
??
SOLUTION:
B) Automatically adjusts subplot parameters to provide reasonable spacing.
`plt.tight_layout()` helps prevent labels and titles from overlapping.
