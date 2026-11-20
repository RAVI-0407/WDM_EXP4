### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns

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
```python
import pandas as pd
import matplotlib.pyplot as plt

# Read CSV file
df = pd.read_csv("clustervisitor.csv")

# Select Age feature
X = df["Age"].tolist()

# Number of clusters
k = 3

# Step 1: Choose initial centroids (first k values)
centroids = X[:k]

while True:
    clusters = [[] for _ in range(k)]
    labels = []

    # Step 2: Assign each data point to the nearest centroid
    for value in X:
        distances = [abs(value - c) for c in centroids]
        cluster = distances.index(min(distances))
        clusters[cluster].append(value)
        labels.append(cluster)

    # Step 3: Calculate new centroids
    new_centroids = []
    for cluster in clusters:
        if len(cluster) > 0:
            new_centroids.append(sum(cluster) / len(cluster))
        else:
            new_centroids.append(0)

    # Step 4: Stop if centroids do not change
    if new_centroids == centroids:
        break

    centroids = new_centroids

# Add cluster labels to DataFrame
df["Cluster"] = labels

# Display complete dataset
print("Complete Dataset")
print(df)

print("\nVisitor Segmentation (Cluster-wise)\n")

# Display cluster-wise output
for i in range(k):
    print(f"Cluster {i}")
    print(df[df["Cluster"] == i])
    print("-" * 50)

# Visualize clusters
plt.figure(figsize=(8,6))	

colors = ["red", "blue", "green"]

for i in range(k):
    cluster_data = df[df["Cluster"] == i]
    plt.scatter(cluster_data["Age"],
                cluster_data["Cluster"],
                color=colors[i],
                s=80,
                label=f"Cluster {i}")

plt.xlabel("Age")
plt.ylabel("Cluster")
plt.title("Visitor Segmentation using K-Means")
plt.legend()
plt.grid(True)
plt.show()

```
### Output:

<img width="537" height="597" alt="image" src="https://github.com/user-attachments/assets/f086148b-67dd-493a-b001-fe09971ee124" />

<img width="521" height="235" alt="image" src="https://github.com/user-attachments/assets/3482b8df-8de1-4ad3-9f19-5441d764957d" />

<img width="490" height="245" alt="image" src="https://github.com/user-attachments/assets/b85fa530-0d1a-4c4b-8fb4-5e886ca225c7" />

<img width="520" height="211" alt="image" src="https://github.com/user-attachments/assets/eac54988-34e5-45f2-9fc0-a9ce2b912e48" />

### Visualization:
```python
# Create a list to store counts of visitors in each age group
/*WRITE YOUR CODE HERE

# Count visitors in each age group
/*WRITE YOUR CODE HERE
    
# Define age group labels and plot a bar chart
/*WRITE YOUR CODE HERE

plt.figure(figsize=(8, 6))
plt.bar(age_group_labels, visitor_counts, color='skyblue')
plt.xlabel('Age Groups')
plt.ylabel('Number of Visitors')
plt.title('Visitor Distribution Across Age Groups')
plt.show()
```
### Output:

<img width="711" height="557" alt="image" src="https://github.com/user-attachments/assets/9e0c4d4e-8152-4db2-b9e0-4886c395dff8" />



### Result:
