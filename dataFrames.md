import pandas as pd
import numpy as np

# Reading in a Data Set
# Load the dataset from a CSV file
dat = pd.read_csv('Auto.csv')

# Show the first few rows of the DataFrame
print(dat.head())

dat.shape
dat.columns

#Read data from an external reporsitory.
url = "https://raw.githubusercontent.com/fammediavilla2/datasets/refs/heads/main/Auto.csv"
dat = pd.read_csv(url)

# Show the first few rows of the DataFrame
print(dat.head())

dat.shape
dat.columns
np.mean(dat.mpg)
np.mean(dat.horsepower) #result is error becasue there is a mixture of data types

# Reveal data types
dat.dtypes

np.unique(dat.horsepower)

dat= pd.read_csv(url, na_values=["?"])
dat.shape
dat.dtypes

np.mean(dat.horsepower)

# Missing data
# Check for missing values in the DataFrame
dat.isnull()
print(dat.isnull().sum()) # how many missing values in each column (missing values or true)

dat[dat.horsepower.isnull()]

dat = dat.dropna()
dat.shape
