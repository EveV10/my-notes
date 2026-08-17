#!/usr/bin/env python3
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
# We begin by importing the subplots() function from matplotlib.
from matplotlib.pyplot import subplots

# set seed for reproducibility
rng = np.random.default_rng(123)
fig , ax = subplots (figsize =(8, 8)) # we have unpacked the tuple of length two returned by subplots() into the two distinct variables fig and ax. 
x = rng. standard_normal (100)
y = rng. standard_normal (100)

ax.plot(x, y);
plt.show()

#to create a scatterplot 
fig , ax = subplots (figsize =(8, 8))
ax.plot(x, y, 'o');
plt.show()
#or
fig , ax = subplots (figsize =(8, 8))
ax.scatter(x, y);
plt.show()

# Adding labels and titles to the plot is straightforward.
# We can use the set_xlabel(), set_ylabel(), and set_title() methods of the axes
# to add labels and titles to the plot.
fig , ax = subplots (figsize =(8, 8))
ax.scatter(x, y);
ax. set_xlabel ("this is the x-axis")
ax. set_ylabel ("this is the y-axis")
ax. set_title ("Plot of X vs Y");
plt.show()

# Occasionally we will want to create several plots within a figure.
# We can do this by passing the nrows and ncols arguments to subplots().
fig, axs = subplots(nrows=2, ncols=2, figsize=(10, 10))
axs[0, 0].scatter(x, y)
axs[0, 0].set_title("Scatter Plot 1")
axs[0, 1].scatter(x, y, color='red')
axs[0, 1].set_title("Scatter Plot 2")
plt.show()

fig, axs = subplots(nrows=2, ncols=2, 
                    sharex=True, sharey=True, 
                    figsize=(10, 10))
axs[0, 0].scatter(x, y)
axs[0, 0].set_title("Scatter Plot 1")
axs[0, 1].scatter(x, y, color='red')
axs[0, 1].set_title("Scatter Plot 2")
plt.show()

#to save the outpur of fig 
fig.savefig("Figure1.png", dpi =400)
fig.savefig("Figure1.pdf", dpi =200);

####### visualizing data
# Read data from an external reporsitory.
url = "https://raw.githubusercontent.com/fammediavilla2/datasets/refs/heads/main/whiteside.csv"
dat = pd.read_csv(url,  na_values=['?'])

# Show the first few rows of the DataFrame
print(dat.head())

# Plot a histogram illustrating the distributions of Temp and Gas.
fig, axs = subplots(nrows=1, ncols=2, figsize=(10, 8))
axs[0].hist(dat['Temp'], bins=10, color='lightblue', edgecolor='black')
axs[0].set_title('Histogram of Temperature')
axs[0].set_xlabel('Temperature Degrees Celsius')
axs[0].set_ylabel('Frequency')
axs[1].hist(dat['Gas'], bins=10, color='lightgreen', edgecolor='black')
axs[1].set_title('Histogram of Gas')
axs[1].set_xlabel('Gas ft^3')
axs[1].set_ylabel('Frequency')
plt.tight_layout()
plt.show()

#scatterplots
fig, ax = subplots(figsize=(8, 6))
ax.scatter(dat['Temp'], dat['Gas'], color='purple', alpha=0.5)
ax.set_title('Scatter Plot of Gas vs Temperature')
ax.set_xlabel('Temperature Degrees Celsius')
ax.set_ylabel('Gas ft^3')
plt.show()

# Create a basic boxplot to visualize the distribution of Gas.
fig, ax = subplots(figsize=(8, 6))
ax.boxplot(dat['Gas']) 
ax.set_title('Boxplot of Gas')
ax.set_xlabel('Gas ft^3')
plt.show()

fig, ax = subplots(figsize=(8, 6))
ax.boxplot(dat['Gas'], vert=False, 
           patch_artist=True, # This allows the boxes to be filled with color.
           boxprops=dict(facecolor='lightblue', color='black'), # Customizes the appearance of the box.
           medianprops=dict(color='red')) # Customizes the appearance of the median line inside the box.
ax.set_title('Boxplot of Gas')
ax.set_xlabel('Gas ft^3')
plt.show()  

# Conditional boxplot to visualize the distribution of Gas by Insul.
fig, ax = subplots(figsize=(8, 6))
dat.boxplot(column='Gas', by='Insul', # Groups the data by the 'Insul' column
            vert=False, # Makes the boxplots horizontal.
            ax=ax, # Draws the plot on the previously created ax subplot.
            patch_artist=True, # This allows the boxes to be filled with color.
            boxprops=dict(facecolor='lightblue', color='black'), # Customizes the appearance of the box.
            medianprops=dict(color='red')) # Customizes the appearance of the median line inside the box.
ax.set_title('Boxplot of Gas by Insul')
ax.set_xlabel('Insulation Type')
ax.set_ylabel('Gas ft^3')
plt.suptitle('')  # Suppress the default title to avoid redundancy
plt.show()

# Create a density plot to visualize the distribution of Gas.
fig, ax = subplots(figsize=(8, 6))
dat['Gas'].plot(kind='kde', ax=ax, color='orange')
ax.set_title('Density Plot of Gas') 
ax.set_xlabel('Gas ft^3')
plt.show()

# Create a conditional density plot to visualize the distribution of Gas by Insul.
fig, ax = subplots(figsize=(8, 6))
for insul_type in dat['Insul'].unique():
    subset = dat[dat['Insul'] == insul_type]
    subset['Gas'].plot(kind='kde', ax=ax, label=insul_type)
ax.set_title('Density Plot of Gas by Insul')
ax.set_xlabel('Gas ft^3')
ax.legend(title='Insulation Type')
plt.show()
