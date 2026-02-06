# Chapter 24: Data Science & Analysis

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `numpy` (Arrays vs Lists, Broadcasting, Vectorization, dtypes), `pandas` (Series, DataFrame, Indexing `loc`/`iloc`, Missing Data `NaN`), Jupyter Notebooks, Virtual Environments (Conda vs Venv), CSV reading, Basic Statistics.

---

**Q24.1: Basic - [Numpy Array Benefit]**

The primary advantage of a NumPy array over a Python list is:

A) It can hold mixed types.
B) It is homogenous (same type), contiguous in memory, and allows vectorized operations (much faster for math).
C) It allows infinite size.
D) It is built-in to Python.

**Answer: B**

**Explanation:**
NumPy arrays use C-structs and eliminate the overhead of Python object pointers for every element.

---

**Q24.2: Intermediate - [Pandas DataFrame]**

A Pandas `DataFrame` is best described as:

A) A 3D array.
B) A 2D labeled data structure with columns of potentially different types (like a SQL table or Excel sheet).
C) A list of lists.
D) A dictionary.

**Answer: B**

**Explanation:**
The core structure of pandas, offering powerful indexing and alignment.

---

**Q24.3: Advanced - [Broadcasting]**

In NumPy, "broadcasting" refers to:

A) Sending data to wifi.
B) The rule that allows arithmetic operations between arrays of different shapes (e.g., adding a scalar to a matrix).
C) Printing to screen.
D) Resizing arrays manually.

**Answer: B**

**Explanation:**
Pandas/NumPy automatically "stretch" the smaller array to match the larger dimensionality if compatible, avoiding explicit loops.

---

**Q24.4: Basic - [Import Convention]**

The standard convention for importing these libraries is:

A) `import numpy; import pandas`
B) `import numpy as np; import pandas as pd`
C) `import np; import pd`
D) `from numpy import *`

**Answer: B**

**Explanation:**
Universally accepted aliases in the data science community.

---

**Q24.5: Intermediate - [Loc vs Iloc]**

In Pandas, `df.iloc[0]` selects:

A) The row with index label `0`.
B) The first row by integer position (0-based index), regardless of the index label.
C) The column named `0`.
D) The cell at (0,0).

**Answer: B**

**Explanation:**
`iloc` is Integer Location (positional). `loc` is Label Location (looks for index name).

---

**Q24.6: Advanced - [NaN Propagation]**

If you perform `np.sum()` on an array containing `np.nan`:

A) It ignores the NaNs.
B) It returns `np.nan`.
C) It throws an error.
D) It treats them as 0.

**Answer: B**

**Explanation:**
NaN ("Not a Number") poisons arithmetic operations. Use `np.nansum()` to ignore them.

---

**Q24.7: Expert - [View vs Copy]**

Slicing a NumPy array (e.g., `arr[1:5]`) returns:

A) A new copy of the data.
B) A "view" into the original array (memory is shared). Modifying it affects the original.
C) A list.
D) An iterator.

**Answer: B**

**Explanation:**
NumPy avoids copying for performance. To get a copy, explicitly call `.copy()`. (Note: Pandas slicing behavior can be more complex due to Copy-on-Write policies in newer versions).

---

**Q24.8: Basic - [Jupyter Notebook]**

A Jupyter Notebook (`.ipynb`) allows you to:

A) Only write code.
B) Combine live code, execution results (plots/tables), and markdown text in a single document.
C) Compile C++.
D) Write Word docs.

**Answer: B**

**Explanation:**
Standard tool for exploratory data analysis (EDA) and storytelling with code.

---

**Q24.9: Intermediate - [Pandas Read CSV]**

`pd.read_csv('data.csv')`:

A) Returns a string.
B) Returns a DataFrame.
C) Returns a list.
D) Prints the file.

**Answer: B**

**Explanation:**
Powerful parser that handles delimiters, headers, and type inference automatically.

---

**Q24.10: Advanced - [Vectorization]**

Why is `df['col'] + 5` faster than iterating through rows?

A) Loops are banned.
B) It pushes the loop to the C level (Vectorization), applying the operation to the entire column block at once using SIMD instructions where possible.
C) It uses more RAM.
D) It uses GPU.

**Answer: B**

**Explanation:**
Avoids Python interpreter overhead for every single element addition.

---

**Q24.11: Basic - [Shape]**

`arr.shape` returns:

A) The total number of elements.
B) A tuple representing the dimensions of the array (rows, columns, etc.).
C) The memory size.
D) The type.

**Answer: B**

**Explanation:**
e.g., `(3, 4)` for a matrix with 3 rows and 4 columns.

---

**Q24.12: Intermediate - [Series]**

A Pandas `Series` is:

A) A one-dimensional labeled array (like a column in Excel).
B) A TV show.
C) A list of DataFrames.
D) A 3D array.

**Answer: A**

**Explanation:**
The building block of a DataFrame.

---

**Q24.13: Advanced - [Boolean Indexing]**

`arr[arr > 5]` performs:

A) A syntax error.
B) Boolean Masking: returns a new array containing only the elements where the condition is True.
C) Returns True/False.
D) Sets elements to 5.

**Answer: B**

**Explanation:**
Powerful way to filter data without loops.

---

**Q24.14: Expert - [Conda]**

The main difference between `conda` and `pip` is:

A) `conda` is for Anaconda only.
B) `pip` installs Python packages. `conda` is a package AND environment manager that can install Python packages AND binary dependencies (like C libraries, HDF5, MKL) and even Python itself.
C) `conda` is slower.
D) They are the same.

**Answer: B**

**Explanation:**
Conda is preferred in Data Science because standard scientific libraries often have complex non-Python binary dependencies (BLAS, LAPACK) that pip sometimes struggles to compile.

---

**Q24.15: Intermediate - [Describe]**

`df.describe()` provides:

A) A string description of the columns.
B) Summary statistics (count, mean, std, min, max, quartiles) for numeric columns.
C) The first 5 rows.
D) Metadata.

**Answer: B**

**Explanation:**
Quick way to get a statistical overview of the dataset.

---

**Q24.16: Basic - [Head]**

`df.head()` returns:

A) The headers.
B) The first 5 rows of the DataFrame.
C) The top row only.
D) The metadata.

**Answer: B**

**Explanation:**
Useful for quickly inspecting data structure.

---

**Q24.17: Advanced - [Merge vs Concat]**

In Pandas, `merge` is like SQL JOIN (combining on keys), whereas `concat` is:

A) Like SQL UNION (stacking DataFrames on top of each other or side-by-side).
B) The same as merge.
C) Used for strings.
D) Deleting data.

**Answer: A**

**Explanation:**
`concat` glues objects together along an axis. `merge` aligns them based on values in key columns.

---

**Q24.18: Intermediate - [Dtype]**

If a NumPy array has `dtype='object'`, it usually means:

A) It is very fast.
B) It contains mixed types (strings and numbers) or Python objects, falling back to slow Python-level storage (losing vectorization benefits).
C) It is optimized.
D) It is empty.

**Answer: B**

**Explanation:**
Avoid object arrays in performance-critical code.

---

**Q24.19: Basic - [Mean]**

`df['col'].mean()` calculates:

A) The median.
B) The average (arithmetic mean).
C) The sum.
D) The mode.

**Answer: B**

**Explanation:**
Standard statistical method.

---

**Q24.20: Advanced - [Apply]**

`df.apply(func)`:

A) Applies a function along an axis of the DataFrame (default axis=0: column-wise).
B) Applies to every cell individually.
C) Is faster than vectorization.
D) Is deprecated.

**Answer: A**

**Explanation:**
While useful for custom logic, `apply` is generally slower than vectorized methods because it runs a Python loop internally.

---

**Q24.21: Expert - [Memory Layout]**

NumPy arrays are stored in "row-major" (C-style) order by default. This means:

A) Iterating along rows is fastest (cache-friendly).
B) Iterating along last dimension (columns) is fastest because adjacent elements in a row are contiguous in memory.
C) It is random.
D) It uses Fortran order.

**Answer: B**

**Explanation:**
In C-order (default), the last index changes fastest. Accessing `arr[0,0]`, `arr[0,1]` accesses adjacent memory addresses.

---

**Q24.22: Intermediate - [Value Counts]**

`df['col'].value_counts()` gives:

A) The number of values.
B) A frequency table (counts of unique values), sorted by count.
C) The sum.
D) The unique values only.

**Answer: B**

**Explanation:**
equivalent to SQL `GROUP BY col COUNT(*)`.

---

**Q24.23: Basic - [Arange]**

`np.arange(10)` creates:

A) A list `[1..10]`.
B) An array `[0, 1, 2, ..., 9]`.
C) A range object.
D) A random number.

**Answer: B**

**Explanation:**
NumPy equivalent of Python's `range()`, but returns an array.

---

**Q24.24: Advanced - [Missing Data Drop]**

`df.dropna(how='any')`:

A) Drops columns with missing data.
B) Drops any row that contains at least one missing value (NaN).
C) Drops rows where ALL values are missing.
D) Fills with 0.

**Answer: B**

**Explanation:**
Be careful, this can remove a lot of data if inputs are sparse.

---

**Q24.25: Intermediate - [Groupby]**

`df.groupby('category').mean()`:

A) Sorts by category.
B) Split-Apply-Combine: Splits data into groups by 'category', calculates mean for each numeric column in each group, and combines results.
C) Errors.
D) Returns a list.

**Answer: B**

**Explanation:**
The fundamental pattern for aggregation in pandas.

---

**Q24.26: Basic - [Matplotlib usage]**

Matplotlib is primarily used for:

A) Machine Learning.
B) Data Visualization (2D plotting).
C) Web Scraping.
D) Database.

**Answer: B**

**Explanation:**
The "Grandfather" of Python plotting libraries.

---

**Q24.27: Expert - [SettingWithCopyWarning]**

Pandas `SettingWithCopyWarning` warns you that:

A) You are copying data.
B) You are attempting to assign values to a "View" of a DataFrame (chained indexing `df[mask]['col'] = 5`), which might not update the original DataFrame.
C) Your computer is slow.
D) You are using too much memory.

**Answer: B**

**Explanation:**
Ambiguity between view vs copy. Fix: Use `.loc[mask, 'col'] = 5` for explicit assignment.

---

**Q24.28: Intermediate - [Reshape]**

`arr.reshape((2, 5))` on a size-10 array:

A) Changes the shape to 2 rows, 5 columns without changing data.
B) Deletes data.
C) Transposes.
D) Copies data.

**Answer: A**

**Explanation:**
Efficient because it usually returns a view, not a copy.

---

**Q24.29: Advanced - [One Hot Encoding]**

`pd.get_dummies(df)` performs:

A) Label Encoding.
B) One-Hot Encoding (converts categorical variables into dummy/indicator variables: 0/1 columns).
C) Validation.
D) Compression.

**Answer: B**

**Explanation:**
Standard preprocessing step for Machine Learning models that require numerical input.

---

**Q24.30: Basic - [Axis]**

In a 2D array/DataFrame, `axis=0` usually refers to:

A) The index (rows) - operations run "down" the columns (e.g., `sum(axis=0)` sums each column).
B) The columns.
C) The depth.
D) Nothing.

**Answer: A**

**Explanation:**
"Move along the rows". Results in one value per column.

---

**Q24.31: Intermediate - [Pivot Table]**

`df.pivot_table(index='A', columns='B', values='C', aggfunc='sum')`:

A) Rotates the table.
B) Creates a spreadsheet-style pivot table where unique values of 'A' become rows, 'B' become columns, and the cells contain the sum of 'C'.
C) Deletes 'A'.
D) Sorts by C.

**Answer: B**

**Explanation:**
Powerful tool for reshaping and summarizing data.

---

**Q24.32: Advanced - [Numpy Dtype]**

If you try to create a NumPy array `np.array([1, 2, 3.5])` (integers and float), the resulting dtype will be:

A) `int64` (truncating 3.5 to 3).
B) `float64` (upcasting integers to floats to maintain precision and homogeneity).
C) `object`.
D) Error.

**Answer: B**

**Explanation:**
NumPy enforces a single data type per array, choosing the one that can represent all data (upcasting).

---

**Q24.33: Basic - [Plot Show]**

After creating a plot with matplotlib (e.g., `plt.plot(x, y)`), to display it you call:

A) `plt.render()`
B) `plt.show()`
C) `plt.display()`
D) `plt.open()`

**Answer: B**

**Explanation:**
Opens the figure window or renders it in the notebook output cell.

---

**Q24.34: Expert - [Strides]**

NumPy array "strides" (`arr.strides`) describe:

A) How fast the code runs.
B) The number of bytes to step in memory to reach the next element in each dimension.
C) The size of the array.
D) The number of walkers.

**Answer: B**

**Explanation:**
Allows advanced tricks like "sliding window" views (`as_strided`) without copying memory.

---

**Q24.35: Intermediate - [Isnull]**

`df.isnull().sum()` is commonly used to:

A) Count the number of missing values (NaN) in each column.
B) Check if the dataframe is empty.
C) Sum the values.
D) Delete NaNs.

**Answer: A**

**Explanation:**
`isnull()` returns a boolean mask, and `sum()` treats True as 1.

---

**Q24.36: Advanced - [Map vs Apply]**

In Pandas, `Series.map(dict)` is faster/preferred over `Series.apply(lambda x: dict[x])` because:

A) `map` is vectorized/optimized for mapping values based on a dictionary or Series lookup.
B) `apply` is faster.
C) `map` uses GPU.
D) They are the same.

**Answer: A**

**Explanation:**
Use `map` for simple element-wise transformations or lookups on a Series.

---

**Q24.37: Basic - [Pandas Save CSV]**

To save a DataFrame to a file:

A) `df.save('file.csv')`
B) `df.to_csv('file.csv', index=False)`
C) `df.write_csv('file.csv')`
D) `pd.save(df)`

**Answer: B**

**Explanation:**
`index=False` is commonly used to avoid writing the row numbers as a separate column.

---

**Q24.38: Intermediate - [Numpy Linspace]**

`np.linspace(0, 10, 5)` generates:

A) `[0, 1, 2, 3, 4]`
B) 5 equally spaced numbers between 0 and 10 (inclusive), e.g., `[0. , 2.5, 5. , 7.5, 10. ]`.
C) Random numbers.
D) Integers only.

**Answer: B**

**Explanation:**
Useful for generating coordinate vectors for plotting.

---

**Q24.39: Advanced - [Explode]**

`df.explode('list_col')`:

A) Deletes the column.
B) Transforms each element of a list-like to a row, replicating index values (unnesting).
C) Blows up memory.
D) Splits strings.

**Answer: B**

**Explanation:**
Essential when working with "tidy data" principles if a cell contains a list of items.

---

**Q24.40: Expert - [Rolling Window]**

`df['col'].rolling(window=3).mean()` calculates:

A) The mean of the entire column.
B) A Simple Moving Average (SMA) where each point is the average of the previous 3 points.
C) A random walk.
D) A weighted mean.

**Answer: B**

**Explanation:**
Common in time series analysis for smoothing data.

---

**Q24.41: Basic - [Tail]**

`df.tail()` returns:

A) The last 5 rows.
B) The first 5 rows.
C) The bottom row only.
D) The summary.

**Answer: A**

**Explanation:**
Counterpart to `head()`.

---

**Q24.42: Intermediate - [Numpy Random]**

`np.random.seed(42)` ensures:

A) Randomness is cryptographically secure.
B) Reproducibility (subsequent random calls will produce the exact same sequence of numbers).
C) Randomness is truly random.
D) Speed.

**Answer: B**

**Explanation:**
Essential for debugging and sharing scientific results.

---

**Q24.43: Advanced - [Categorical Dtype]**

Converting a string column to `category` dtype (`df['C'].astype('category')`) is beneficial when:

A) The column has many unique values.
B) The column has a low cardinality (few unique values repeated many times), saving huge amounts of memory and speeding up operations.
C) You want to sort alphabetically.
D) Never.

**Answer: B**

**Explanation:**
Pandas stores the strings once in a lookup table and uses integer codes in the column.

---

**Q24.44: Expert - [Pandas Index alignment]**

When adding two Series `s1 + s2`, Pandas aligns them by:

A) Integer position (0th element + 0th element).
B) Index Label (values with same index match up). If a label is missing in one, result is NaN.
C) It appends them.
D) It crashes.

**Answer: B**

**Explanation:**
This implicit alignment by label is a superpower (and potential pitfall) of Pandas compared to NumPy.

---

**Q24.45: Intermediate - [Correlation]**

`df.corr()` calculates:

A) The sum of columns.
B) The pairwise correlation coefficients (e.g., Pearson) between all numeric columns.
C) The covariance.
D) The R-squared.

**Answer: B**

**Explanation:**
Range is -1 to 1. Visualized often with a heatmap.

---

**Q24.46: Basic - [Scatter Plot]**

`plt.scatter(x, y)` creates:

A) A line chart.
B) A scatter plot (points).
C) A bar chart.
D) A pie chart.

**Answer: B**

**Explanation:**
Standard for visualizing relationship between two continuous variables.

---

**Q24.47: Advanced - [Concat Axis]**

`pd.concat([df1, df2], axis=1)`:

A) Stacks them vertically (more rows).
B) Stacks them horizontally (side-by-side, adding columns), matching on index.
C) Merges them.
D) Deletes them.

**Answer: B**

**Explanation:**
Default is axis=0 (vertical).

---

**Q24.48: Expert - [Memory Usage Deep]**

`df.info(memory_usage='deep')`:

A) Shows estimated memory usage.
B) Inspects object columns (strings) precisely by reading string lengths, giving the true RAM footprint.
C) Is fast.
D) Shows disk usage.

**Answer: B**

**Explanation:**
Standard `df.info()` underestimates memory for object columns (it only counts pointer size).

---

**Q24.49: Intermediate - [Unique]**

`df['col'].unique()` returns:

A) A list of unique values.
B) The count of unique values.
C) A set.
D) A boolean mask.

**Answer: A**

**Explanation:**
Returns a NumPy array of the unique values. `nunique()` gives the count.

---

**Q24.50: Basic - [Pip Install]**

To install pandas, the command is:

A) `python install pandas`
B) `pip install pandas`
C) `npm install pandas`
D) `install pandas`

**Answer: B**

**Explanation:**
Standard Python package installer.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
