**I. Web Mining: Lecture 05: Link Analysis (2/2)**

- **1. Community Detection:** Introduces the concept of community detection in networks, highlighting that community members share similarities and communities themselves can be interlinked. This section also provides diverse examples of community structures in networks like social networks, protein interactions, and citation networks.
- **2. Kernighan–Lin Algorithm:** Explains the Kernighan–Lin algorithm, used for graph partitioning. It delves into the minimum cut problem, the algorithm's steps, cost calculation, and provides illustrative examples. The section concludes with an analysis of the algorithm's complexity.
- **3. Girvan-Newman Algorithm:** Introduces the Girvan-Newman algorithm, which focuses on identifying "bridge" edges between communities using the concept of "edge betweenness." The algorithm iteratively removes these bridges to reveal community structures.
- **4. Graph Representation:** Discusses the limitations of traditional graph representations like adjacency matrices and introduces the need for low-dimensional representations.
- **5. Node2vec:** Presents the node2vec algorithm, a method for learning low-dimensional representations of nodes in a graph.
- **a) Introduction:** Briefly describes node2vec and its goal of representing nodes in a lower-dimensional space.
- **b) Skip-Gram Model:** Explains how node2vec utilizes a skip-gram model, similar to natural language processing, to predict neighboring nodes based on the current node.
- **c) Input Layer:** Describes the input layer of the model, using one-hot encoding to represent individual nodes.
- **d) Hidden Layer:** Explains the hidden layer, which generates the low-dimensional representation of nodes based on connections and weights from the input layer.
- **e) Output Layer:** Describes the output layer, predicting neighboring nodes based on the representation learned in the hidden layer, utilizing softmax activation and log-likelihood loss.
- **f) Neighborhood(vi):** Explains how the algorithm defines the "neighborhood" of a node, discussing different sampling strategies like BFS, DFS, and random walks.
- **g) Objective Function:** Details the objective function of the model, aiming to maximize the probability of observing the actual neighboring nodes given the current node's representation.
- **h) Node2vec: Biased Walks:** Introduces the concept of biased random walks to balance between local and global network structure exploration. Explains how BFS and DFS strategies capture different network views and how node2vec combines them using return parameter (p) and in-out parameter (q).
- **i) Experiments: Micro vs. Macro:** Presents experimental results comparing node2vec with other methods on tasks like multi-label classification, showcasing the algorithm's ability to capture both local and global network structure.
- **j) Edge Embedding:** Concludes by briefly mentioning how node representations from node2vec can be used to generate representations for edges in the graph.