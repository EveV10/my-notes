#Basic statistical functions 
import numpy as np
import matplotlib.pyplot as plt

# Sample random data for demonstration
rng = np.random.default_rng(3) # key is 3
y = rng.normal(50, 5, 1000) # 1000 samples from a N(50, 5)

# plot the histogram of y
plt.hist(y)
plt.show()

y[1:5]

#Central Tendency
# Mean
print(np.mean(y))  # Calculate the mean of y
print(y.mean())  # Another way to calculate the mean using the array method

print(np.median(y))

# Visualize the mean on the histogram
# add a line to the plot to show the mean
plt.hist(y)
plt.axvline(np.mean(y), color='red', linestyle='dashed')
plt.show()

#Measures of Location (quantiles/percentiles/quartiles)
# Compute Quartiles
print(np.quantile(y, (0, 0.25, 0.5, 0.75, 1)))  # Quartiles (Q0, Q1, Q2, Q3, Q4)
np.quantile (y, 0.99)

np.min(y)
np.max(y)

#Measures of dispersion
# Range
np.max(y) - np.min(y)

# Variance
print(np.var(y))  # Calculate the variance of y

# Standard Deviation
print(np.std(y))  # Calculate the standard deviation of y

# Interquartile Range (IQR)
np.quantile(y, 0.75) - np.quantile(y, 0.25)
np.diff(np.quantile(y, (0.25, 0.75)))  # Another way to calculate the IQR

# Coefficient of Variation
def CV(x):
    return np.std(y) / np.mean(y) * 100 # Calculate the coefficient of variation
CV(y)

np.std(y)
np.mean(y)

# Visualize the standard deviation on the histogram
plt.hist(y)
plt.axvline(np.mean(y) + np.std(y), color='blue', linestyle='dashed', label='Mean -/+ 1 Std Dev')
plt.axvline(np.mean(y) - np.std(y), color='blue', linestyle='dashed')
plt.legend()
plt.show()

#Applying statistical functions to 2 dimensional arrays 
# Sample random data for demonstration
rng = np.random.default_rng(1) # key is 1
# Sample a 10 by 3 matrix of random numbers N(50, 5)
X = rng.normal(50, 5, (10, 3))
X
np.sum(X, axis=0)
np.mean(X, axis=0)
np.std(X, axis=0)

# Calculate the mean of each column
print(np.mean(X, axis=0))  # Mean of each column

# Calculate the mean of each row
print(np.mean(X, axis=1))  # Mean of each row
