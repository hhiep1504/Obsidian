**content**
[[#1. Tổng quan về hệ gợi ý]]
[[#2. Các phương pháp đánh giá]]
[[#3. Lọc cộng tác dựa trên kNN]]
[[#4. Lọc cộng tác dựa trên MF]]
[[#5. NCF]]
[[#6. Gợi ý theo phiên]]
## 1. Tổng quan về hệ gợi ý

## 2. Các phương pháp đánh giá

## 3. Lọc cộng tác dựa trên kNN 
## 4. Lọc cộng tác dựa trên MF 
## 5. NCF 
## 6. Gợi ý theo phiên


## Table of Contents: Understanding Recommendation Systems

**Source:** Excerpts from "L08-RecommendationSystems.pdf"

**I. Overview of Recommendation Systems**

- **Why Recommendation Systems are Necessary:** Explores the information overload users face and the need for personalized recommendations to enhance sales and service quality.
- **Recommendation Systems vs. Search Engines:** Differentiates recommendation systems from search engines, highlighting that recommendation systems cater to users who may not have specific desires.
- **Applications:** Provides a comprehensive list of domains where recommendation systems are utilized, including e-commerce, online entertainment, news platforms, social networks, research, and online dating.
- **Illustrative Examples:** Presents case studies of Amazon, Netflix, and Google News, showcasing the significant impact of recommendation systems on revenue and user engagement.
- **Recommendation Methods:** Outlines various approaches, including content-based filtering, collaborative filtering (user-based and item-based), session-based recommendations, and hybrid methods.
- **The Netflix Prize Competition:** Discusses the Netflix Prize competition, highlighting its role in advancing recommendation system research.
- **Challenges in Recommendation Systems:** Examines the inherent difficulties, including data sparsity, cold-start problems, and the dynamic nature of user preferences and product availability.

**II. Evaluation Methods**

- **Dataset Description:** Describes the typical dataset structure with users, items, ratings, and timestamps.
- **Rating Scales:** Discusses different rating scales, such as 5-star ratings and binary ratings.
- **Train/Test Split:** Explains the process of dividing the dataset into training and testing sets for model evaluation.
- **Evaluation Metrics:** Introduces common evaluation metrics like Mean Absolute Error (MAE), Normalized MAE (NMAE), Root Mean Squared Error (RMSE), and ranking-based metrics (Precision, Recall, F-score).
- **A/B Testing:** Describes the A/B testing methodology for comparing different recommendation systems in a real-world setting.

**III. Collaborative Filtering Based on k-Nearest Neighbors (kNN)**

- **Introduction:** Explains the concept of collaborative filtering using kNN, emphasizing its reliance on the user-item interaction matrix and the absence of a training phase.
- **User-Based Collaborative Filtering:** Details the process of finding similar users (neighbors) and predicting ratings based on their preferences.
- **User Similarity Calculation:** Presents formulas for computing user similarity, focusing on the Jaccard coefficient and cosine similarity.
- **Rating Prediction:** Illustrates how to predict ratings using the weighted average of neighbors' ratings.
- **Example:** Provides a numerical example to demonstrate the kNN-based collaborative filtering process.
- **Disadvantages:** Discusses the drawbacks of kNN, including the need for frequent updates and computational complexity.
- **Item-Based Collaborative Filtering:** Explores item-based collaborative filtering, highlighting its suitability for systems with fewer items than users and the ability to pre-compute item similarities.
- **Item Representation and Similarity:** Explains item representation based on the user-item interaction matrix and discusses item similarity computation.
- **Rating Prediction in Item-Based Filtering:** Demonstrates rating prediction in item-based filtering, leveraging the weighted average of similar items' ratings.
- **Example of Item-Based Filtering:** Offers a numerical example to illustrate the item-based collaborative filtering process.

**IV. Collaborative Filtering Based on Matrix Factorization (MF)**

- **Conceptual Framework:** Introduces matrix factorization as a method for capturing latent features of users and items from the overall interaction patterns.
- **Singular Value Decomposition (SVD):** Explains how SVD decomposes the user-item matrix into user-feature and item-feature matrices, enabling the representation of users and items in a latent feature space.
- **Rating Prediction using MF:** Describes how to predict ratings using the dot product of user and item feature vectors.
- **Model Training:** Discusses the objective function (error function) and the gradient descent optimization technique for learning the model parameters (user and item feature vectors).
- **Gradient Descent Algorithm:** Presents the gradient descent update equations for user and item feature vectors.

**V. Neural Collaborative Filtering (NCF)**

- **Limitations of Traditional MF:** Explains the limitations of traditional MF in capturing complex user-item interactions.
- **Advantages of Neural Networks:** Highlights the ability of neural networks to learn hierarchical feature representations, overcoming the limitations of MF.
- **NCF Architecture:** Describes the architecture of NCF, including input layers, embedding layers, multi-layer perceptron (MLP), and the output layer.
- **Input and Embedding Layers:** Explains the representation of users and items using one-hot encoding and embedding vectors.
- **MLP Layer:** Describes the role of the MLP layer in capturing non-linear interactions between user and item embeddings.
- **Loss Function:** Discusses the use of binary cross-entropy loss for implicit feedback scenarios.

**VI. Session-Based Recommendations**

- **Context and Motivation:** Explains the scenarios where user identification and explicit feedback are difficult to obtain, necessitating session-based recommendations.
- **Problem Formulation:** Defines the session-based recommendation task, aiming to predict the next item in a sequence of user interactions.
- **Implicit Feedback and Session Data:** Discusses the use of implicit feedback data (e.g., clicks, views) in session-based recommendations.
- **Recurrent Neural Network (RNN) Architecture:** Describes the use of RNNs for modeling sequential data in session-based recommendations.
- **Input, Embedding, and Recurrent Layers:** Explains the representation of items using one-hot encoding, the embedding layer for dimensionality reduction, and the recurrent layer for capturing temporal dependencies.
- **MLP Layer and Output:** Discusses the role of the MLP layer in generating predictions and the output layer for providing item probabilities.
- **Loss Function:** Introduces the pairwise ranking loss function used to optimize the model for ranking relevant items higher than irrelevant ones.