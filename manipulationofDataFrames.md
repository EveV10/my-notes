import pandas as pd
import numpy as np

# Read data from an external reporsitory.
url = "https://raw.githubusercontent.com/fammediavilla2/datasets/refs/heads/main/Auto.csv"
dat = pd.read_csv(url)

# Show the first few rows of the DataFrame
print(dat.head())

# We can use dat.columns to check the variable names.
print(dat.columns)

dat[:3]  # first three rows

idx_80 = dat['year'] > 80

dat[idx_80].head()  # rows where the year is greater than 80

dat.index  # check the index of the DataFrame
RangeIndex(start=0, stop=397, step=1)

# Default index
dat[['mpg', 'horsepower']].head()  # first few rows of 'mpg' and 'horsepower' columns

dat_re = dat. set_index ('name')
dat_re.head()

dat_re.columns  # check the columns of the DataFrame

rows = ['amc rebel sst', 'ford torino'] # select specific rows
dat_re.loc[rows]  # access rows by name

dat_re.loc['ford galaxie 500', :]  # access all rows with the name 'ford galaxie 500'

dat_re.iloc[3:4]  # access rows by index position

dat_re.iloc[:, [0, 3]]  # select the first and fourth columns 

dat_re.iloc[3:5, [0, 2, 3]]  # select specific rows and columns

# For example, to select rows where 'mpg' is greater than 20:
filtered_rows = dat_re[dat_re['mpg'] > 20]
print(filtered_rows.head())  # display the first few rows of the filtered DataFrame

# we can use indexing to select specific rows and columns:
idx_80 = dat_re['year'] > 80
dat_re.loc[idx_80 , ['weight', 'origin']].head()  # select 'weight' and 'origin' for rows where 'year' > 80

filtered_data = dat_re.loc[dat_re['year'] > 80, ['weight', 'origin']]
print(filtered_data.head())  # display the first few rows of the filtered data

# we can use an anonymous function called a lambda:
dat_re.loc[lambda df: df['year'] > 80, ['weight', 'origin']].head()  # select 'weight' and 'origin' for rows where 'year' > 80 using a lambda function

#  suppose that we want all cars built after 1980 that achieve greater than 30 miles per gallon
dat_re.loc[(dat_re['year'] > 80) & (dat_re['mpg'] > 30)].head()  # select rows where 'year' > 80 and 'mpg' > 30

# We can also use the query() method for more complex filtering:
filtered_query = dat_re.query('year > 80 and mpg > 30')
print(filtered_query.head())  # display the first few rows of the filtered DataFrame using query'

dat_re.loc[(dat_re['displacement'] < 300) & 
           (dat_re.index.str.contains('ford') |
            dat_re.index.str.contains('datsun'))].head()  # select rows with 'displacement' < 300 and index containing 'ford' or 'datsun'

# We can also use the query() method for more complex filtering:
filtered_query = dat_re.query('displacement < 300 & (index.str.contains("ford") | index.str.contains("datsun"))')
print(filtered_query.head())  # display the first few rows of the filtered DataFrame using query
