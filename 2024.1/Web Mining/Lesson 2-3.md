###### 1. Basic Concepts: Introduction to clustering

- This section defines clustering as the process of grouping data with similar properties and provides real-world applications of clustering in marketing, production, and news synthesis.

###### 2. K-means Algorithm: Understanding the algorithm and its limitations

- This section delves into the K-means algorithm, detailing its steps, convergence criteria, and computational complexity. It also highlights its limitations, such as sensitivity to outliers and initialization, and its ineffectiveness with non-spherical clusters.

###### 3. Cluster Representation: Different ways to represent clusters

- This section explores various methods for representing clusters, including centroid-based, classification model-based, and common value-based approaches, providing examples for each.

###### 4. Hierarchical Clustering: Exploring hierarchical relationships between clusters

- This section introduces hierarchical clustering, explaining its bottom-up and top-down approaches and visualizing the cluster relationships through dendrograms. It discusses different linkage methods (single, complete, average), their advantages, disadvantages, and computational complexities.

###### 5. Distance Function: Defining similarity between data points

- This section explains how to measure distances between data points for continuous and binary/discrete attributes using various distance metrics like Minkowski, Euclidean, Manhattan, Jaccard, and more.

###### 6. Normalize Data: Ensuring consistent influence across attributes

- This section emphasizes the importance of normalizing data to prevent bias from attributes with different scales, illustrating the process with examples and covering various attribute types.

###### 7. Handling Multiple Attribute Types: Dealing with diverse data

- This section addresses the challenges of handling data with multiple attribute types and suggests converting them to a common type or calculating weighted distances across attributes.

###### 8. Evaluation Method: Assessing the effectiveness of clustering

- This section covers various methods for evaluating clustering techniques, including user-based, classification-based, compression metrics, isolation metrics, and indirect evaluation through end-task performance.

###### 9. Exploring Holes and Data Areas: Identifying data sparsity

- This section highlights the importance of identifying data holes (areas with little or no data) and explains how classification techniques can be used for this purpose.

###### 10. Learning LU (Labeled and Unlabeled Examples): Leveraging unlabeled data for improved classification

- This section introduces the concept of leveraging unlabeled data alongside labeled data to improve classifier performance, especially when labeled data is scarce. It discusses various LU learning algorithms:
- **EM Algorithm:** Iterative method for estimating probabilities with missing data.
- **Co-training:** Building multiple classifiers on different attribute sets and leveraging their predictions.
- **Self-training:** Iteratively adding confidently classified unlabeled examples to the training set.
- **Inference on SVM:** Utilizing unlabeled data to optimize hyperplane selection in Support Vector Machines.
- **Graph-based methods:** Constructing graphs from data and using graph partitioning techniques for classification.

###### 11. Learning PU (Positive and Unlabeled Examples): Identifying positive instances from unlabeled data

- This section explores scenarios where only positive and unlabeled data is available and outlines techniques for building classifiers to identify positive instances.
- **Applications:** This subsection provides real-world examples of using PU learning, such as building scientific work databases.
- **Theoretical Background:** This subsection lays the mathematical foundation for understanding and evaluating PU learning algorithms.
- **Classifier Construction (2 steps):** This subsection outlines a two-step approach:
- **Step 1: Identifying reliable negative examples from unlabeled data.**
- **Step 2: Building a classifier using positive, reliable negative, and remaining unlabeled data.**
- **Step 1 Techniques:** This subsection details several techniques for identifying reliable negative examples:
- **Spying Techniques:** Using a subset of positive examples to identify positive instances within unlabeled data.
- **Cosine-Rocchio Technique:** Leveraging cosine similarity with positive example centroids to distinguish positive and negative instances.
- **1DNF technique:** Identifying frequent features in positive examples and using them to filter negative instances from unlabeled data.
- **NB and Rocchio techniques:** Adapting Naive Bayes and Rocchio classifiers for identifying negative instances.
- **Step 2 Techniques:** This subsection describes different approaches for building the final classifier:
- **EM + NB:** Combining Expectation Maximization with Naive Bayes for iterative classifier refinement.
- **SVM:** Adapting Support Vector Machines for PU learning scenarios.
- **Classifier Construction: SVM:** This subsection dives deeper into utilizing SVM for PU learning, addressing different scenarios and constraints.
- **Classifier Construction: Probability Estimation:** This subsection focuses on estimating probabilities for positive classification using both labeled and unlabeled data.

## Study Guide

### K-Means Algorithm:

- **Definition:** An iterative clustering algorithm that partitions data into k clusters, where each data point belongs to the cluster with the nearest mean (centroid).

1. **Steps:**Initialization: Randomly select k data points as initial centroids.
2. Cluster Assignment: Assign each data point to the cluster whose centroid is closest (based on distance).
3. Centroid Update: Recalculate the centroids of each cluster based on the mean of all data points assigned to that cluster.
4. Repeat steps 2 and 3 until convergence criteria are met (e.g., no more reassignments, centroids don't change significantly).

- **Convergence Conditions:**Number of reassigned data points falls below a threshold.
- Number of centroids changed is less than a threshold.
- The sum of squared errors (distance between data points and their cluster centroids) is minimized.
- **Computational Complexity:** O(tkn) - where 't' is the number of iterations, 'k' is the number of clusters, and 'n' is the number of data points.
- **Limitations:**Requires specifying 'k' (number of clusters) in advance.
- Sensitive to the initial placement of centroids (can get stuck in local optima).
- Sensitive to outliers (extreme data points).
- Assumes clusters are spherical and equally sized.

### Hierarchical Clustering:

- **Definition:** A clustering method that builds a hierarchy of clusters, represented as a tree (dendrogram).
- **Types:Agglomerative (Bottom-Up):** Starts with each data point as its own cluster and iteratively merges the closest clusters until one cluster remains.
- **Divisive (Top-Down):** Starts with all data points in one cluster and recursively divides it into smaller clusters.
- **Linkage Methods (for Agglomerative Clustering):** Determine how the distance between clusters is calculated.
- **Single Link:** Distance between two clusters is the shortest distance between any two points in the clusters. Prone to chaining effects.
- **Complete Link:** Distance is the maximum distance between any two points in the clusters.
- **Average Link:** Distance is the average distance between all pairs of points in the clusters.
- **Advantages:**Provides a hierarchy of clusters.
- Does not require specifying 'k' in advance.
- **Disadvantages:**Can be computationally expensive for large datasets.
- Sensitive to noise and outliers.

### Distance Functions:

- **Purpose:** Measure the similarity or dissimilarity between data points.
- **Common Distance Metrics:Euclidean Distance:** Straight-line distance between two points in Euclidean space.
- **Manhattan Distance:** Distance between two points measured along axes at right angles.
- **Minkowski Distance:** A generalization of Euclidean and Manhattan distances.
- **Jaccard Distance (for Binary Attributes):** Measures dissimilarity between sample sets.

### Normalizing Data:

- **Purpose:** Scales data attributes to a common range (usually [0, 1]) to prevent attributes with larger ranges from dominating distance calculations.
- **Normalization Techniques:Min-Max Scaling:** Scales data to a specific range (e.g., 0 to 1).
- **Z-Score Standardization:** Transforms data to have a mean of 0 and a standard deviation of 1.

### Handling Multiple Attribute Types:

- **Challenge:** Datasets often contain mixed attribute types (continuous, discrete, binary), making distance calculation complex.
- **Strategies:Convert to Common Type:** Transform all attributes to a common type (e.g., convert categorical to numerical).
- **Calculate Distance Separately:** Compute distance for each attribute type separately and combine them.

### Cluster Evaluation:

- **Purpose:** Assess the quality of clustering results.
- **Evaluation Methods:User-Based:** Rely on expert judgment to evaluate cluster coherence.
- **Classification-Based:** Use labeled data (if available) to compare cluster assignments to known class labels.
- **Compression Metrics:** Measure how tightly clustered the data points are within each cluster (e.g., Sum of Squared Errors - SSE).
- **Isolation Metrics:** Quantify how well-separated clusters are from each other (e.g., distance between cluster centroids).

### Exploring Holes and Data Areas:

- **Data Holes:** Regions in the data space with few or no data points.
- **Importance:** Identifying data holes can reveal areas where more data is needed, improve model generalization, or identify outliers.

### Learning with Labeled and Unlabeled Data (LU Learning):

- **Motivation:** Labeled data is often scarce and expensive to obtain, while unlabeled data is abundant.
- **Goal:** Leverage unlabeled data to improve the performance of classifiers trained on limited labeled data.
- **Techniques:EM Algorithm (Expectation-Maximization):** An iterative algorithm that estimates missing values (e.g., class labels) and updates model parameters.
- **Co-Training:** Trains multiple classifiers on different views (subsets of features) of the data and uses their predictions to label unlabeled data.
- **Self-Training:** Trains a classifier on labeled data, uses it to predict labels for unlabeled data, and incorporates high-confidence predictions into the training set.
- **Graph-Based Methods:** Construct graphs where nodes represent data points, and edges represent similarity. Use labeled data to propagate labels to unlabeled nodes.

### Learning from Positive and Unlabeled Data (PU Learning):

- **Scenario:** You have access to positive examples and unlabeled data, but no explicitly labeled negative examples.
- **Goal:** Build a classifier to distinguish positive examples from the rest.
- **Applications:** Text classification, anomaly detection, web page categorization.
- **Techniques:Spy Technique:** Identify reliable negative examples from unlabeled data.
- **Cosine-Rocchio:** Use cosine similarity to find negative examples.
- **1DNF:** Use frequent itemsets to define negative examples.

1. **Two-Step Approaches:**Identify reliable negatives.
2. Train a classifier (e.g., EM+NB, SVM) on positive and identified negative data.

## Quiz

**Instructions:** Answer the following questions in 2-3 sentences each.

1. **What is the main difference between hierarchical clustering and k-means clustering?**
2. **Explain why normalizing data is important before applying a distance-based clustering algorithm.**
3. **What is the purpose of a linkage method in hierarchical clustering?**
4. **List and briefly describe three common distance metrics used in clustering.**
5. **What is the main advantage of using the EM algorithm for learning with labeled and unlabeled data?**
6. **Describe the "spy technique" used in PU learning.**
7. **Explain the concept of co-training in the context of LU learning.**
8. **Why is it sometimes necessary to handle multiple attribute types in a dataset before clustering?**
9. **What is the main goal of PU learning? Provide an example application.**
10. **How does self-training work as an LU learning technique?**

## Quiz Answers:

1. K-means partitions data into a predetermined number (k) of clusters, while hierarchical clustering builds a hierarchy of clusters without specifying k beforehand.
2. Normalization prevents attributes with larger ranges from disproportionately influencing distance calculations, ensuring fair comparison between attributes.
3. Linkage methods define how the distance between two clusters is measured in hierarchical clustering, such as single link, complete link, or average link.

- **Euclidean distance:** Straight-line distance between two points.
- **Manhattan distance:** Distance measured along axes at right angles.
- **Jaccard distance:** Measures dissimilarity between sample sets, commonly used for binary data.

4. The EM algorithm is particularly useful for LU learning as it iteratively estimates missing labels in unlabeled data and refines the model parameters, maximizing the use of available information.
5. The spy technique in PU learning involves embedding a small portion of labeled positive examples into the unlabeled set, training a classifier, and using it to identify likely negative examples from the unlabeled set based on low probability scores.
6. In co-training, two or more classifiers are trained on different views or feature subsets of the data. They then label unlabeled instances, and those labeled with high confidence by one classifier are added to the training set of the other classifier(s). This process repeats iteratively.
7. Handling multiple attribute types is crucial because directly applying distance metrics designed for one type to another may lead to inaccurate distance estimations and, consequently, incorrect clustering results.
8. PU learning aims to build classifiers when only positive and unlabeled data are available. An example is identifying spam emails, where you have a set of confirmed spam emails and a larger set of unlabeled emails.
9. Self-training initially trains a classifier on the labeled data. Then, it uses this classifier to predict the labels of unlabeled instances. Instances with high-confidence predictions are added, along with their predicted labels, to the labeled data, and the classifier is retrained. This process iterates until a stopping criterion is met.