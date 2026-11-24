### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 20.11.2026
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```
import pandas as pd
import matplotlib.pyplot as plt

# Read CSV file
df = pd.read_csv("clustervisitor.csv")

# Select Age feature
X = df["Age"].tolist()

# Number of clusters
k = 3

# ==========================
# PART – 1 : Choose initial centroids (first k values)
# ==========================
centroids = X[:k]

while True:
    # ==========================
    # PART – 2 : Assign each data point to the nearest centroid
    # ==========================
    clusters = [[] for _ in range(k)]

    for value in X:
        distances = [abs(value - centroid) for centroid in centroids]
        cluster_index = distances.index(min(distances))
        clusters[cluster_index].append(value)

    # ==========================
    # PART – 3 : Calculate new centroids
    # ==========================
    new_centroids = []

    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    # Stop if centroids do not change
    if new_centroids == centroids:
        break

    centroids = new_centroids

# ==========================
# PART – 4 : Display cluster-wise output
# ==========================
print("Final Centroids:")
for i, centroid in enumerate(centroids):
    print(f"Cluster {i+1}: Centroid = {centroid:.2f}")
    print("Data Points:", clusters[i])
    print()


```
### Output:
<img width="692" height="242" alt="image" src="https://github.com/user-attachments/assets/8a1712f9-9fb4-4918-b80c-7472e8887221" />

### Visualization:
```
colors = ["red", "blue", "green"]

for i in range(k):
    # Plot cluster points
    plt.scatter(clusters[i],
                [i + 1] * len(clusters[i]),
                color=colors[i],
                s=80,
                label=f"Cluster {i+1}")

    # Display Age value above each point
    for age in clusters[i]:
        plt.text(age,
                 i + 1 + 0.05,
                 str(age),
                 fontsize=9,
                 ha='center',
                 color='black')

# Plot centroids
for i, centroid in enumerate(centroids):
    plt.scatter(centroid,
                i + 1,
                color='black',
                marker='X',
                s=200,
                label='Centroid' if i == 0 else "")

    # Display centroid value
    plt.text(centroid,
             i + 1 - 0.12,
             f"C={centroid:.1f}",
             fontsize=10,
             color='blue',
             ha='center')

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()
```
### Output:
<img width="705" height="555" alt="image" src="https://github.com/user-attachments/assets/12a78f49-763f-4e3b-abd8-800e8c999bf1" />
## Result:
Thus Cluster and Visitor Segmentation for Navigation patterns in Python is implemented.

