import numpy as np
import pandas as pd
from kmedoids import KMedoids
import matplotlib.pyplot as plt
from sklearn.metrics import pairwise_distances
from sklearn.preprocessing import StandardScaler
from scipy.spatial.distance import euclidean, cityblock, minkowski
from sklearn.cluster import DBSCAN
from sklearn.neighbors import NearestNeighbors

# Load the sportcars dataset
dat = pd.read_csv('Sportcars.csv')

dat.columns 

dat.head()

# Rename variables 
dat.rename(columns= {'Car Make': "CarMake", 'Car Model': 'CarModel', 'Engine Size (L)': 'EngineSize', 
                    'Torque (lb-ft)': 'Torque', 'Top Speed (mph)': 'TopSpeed', 
                    '0-60 MPH Time (seconds)': 'Time', 'Price (in USD)': 'Price'}, inplace=True)

dat.head()

# Categorize the variable Price into five categories using quintiles
dat['price.cat'] = pd.qcut(dat['Price'], q=5, labels=['Very Low', 'Low', 'Medium', 'High', 'Very High'])
dat.head()


# Select the first six variables for clustering
X = dat[['EngineSize', 'Horsepower', 'Torque', 'Time']]

# Scale the features to prevent numerical instability and give each feature equal weight.
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Get means for each column
np.mean(X_scaled, axis=0)
np.std(X_scaled, axis=0)



# Precomputed distance matrix example 
# Use 'manhattan' distance matrix example
distance_matrix = pairwise_distances(X_scaled, metric='manhattan')


# Initialize list to store total within-cluster sum of squares
costs = []
I = range(1, 11) # Range of cluster numbers to try

for i in I:
    # For raw data, set metric to 'euclidean'
    model=KMedoids(n_clusters=i, metric='precomputed', random_state=123)
    model.fit(distance_matrix)

    # Total intra-cluster sum of distances (cost)
    cost = model.inertia_
    costs.append(cost)

plt.plot(I, costs, marker='o')
plt.xlabel('Number of Clusters (k)')
plt.ylabel('Cost (Sum of Distances to Medoids)')
plt.title('Elbow Method for K-Medoids')
plt.show()

## =======================================================



model_k5 = KMedoids(n_clusters=5, random_state=123,metric='precomputed')
model_k5.fit(distance_matrix)


dat['cluster_k5'] = model_k5.labels_ # Assigns cluster indices (0, 1, or 2) to each sample

# Show cluster composition
print(dat['cluster_k5'].value_counts().sort_index())


# Get cluser means (centroids in original scale), round numbers 2 decimals

# Only select numeric columns plus the cluster label
profile = dat[['Year', 'EngineSize', 'Horsepower', 'Torque', 'Time', 'Price', 'cluster_k5']].groupby('cluster_k5').mean()
print(profile.round(0))

# Cross tabulation by CarMake and cluster_k4
crosstab_result = pd.crosstab(dat['CarMake'], dat['cluster_k5'])
print(crosstab_result)

# Cross tabulation by Price.cat and cluster_k4
crosstab_price = pd.crosstab(dat['price.cat'], dat['cluster_k5'])
print(crosstab_price)

## Repeat the analysis using DBSCAN

# DBSCAN Clustering
# Determine eps using k-distance plot

neighbors = NearestNeighbors(n_neighbors=10)
neighbors_fit = neighbors.fit(X_scaled)
distances, indices = neighbors_fit.kneighbors(X_scaled)

distances = np.sort(distances[:, 9])
plt.plot(distances)
plt.title('k-distance plot')
plt.show()

# DBSCAN model 
dbscan = DBSCAN(eps=0.5, min_samples=10)
clusters = dbscan.fit_predict(X_scaled)

# Add cluster labels to the dataframe
dat['cluster_dbscan'] = clusters

dat.head()

print("DBSCAN Cluster Labels:\n", dat['cluster_dbscan'].value_counts())

# Only select numeric columns plus the cluster label
profile = dat[['Year', 'EngineSize', 'Horsepower', 'Torque', 'Time', 'Price', 'cluster_dbscan']].groupby('cluster_dbscan').mean()
print(profile.round(0))


# Cross tabulation by CarMake and cluster_k4
crosstab_result = pd.crosstab(dat['CarMake'], dat['cluster_dbscan'])
print(crosstab_result)

# Cross tabulation by Price.cat and cluster_k4
crosstab_price = pd.crosstab(dat['price.cat'], dat['cluster_dbscan'])
print(crosstab_price)
