

**1. Static Charts**
**a. 1.1 Attributes**
* This section defines key terms like data objects, attributes, and attribute vectors, explaining their significance in data visualization.

* It then classifies attribute types (nominal, binary, ordinal, interval, ratio) with examples and relevant use cases.

* Finally, it differentiates between discrete and continuous attributes, providing illustrative examples for each.

**b. 1.2 Basic Data Statistics**
* This section outlines the importance of data description through central value, distribution range, visualization, and outlier identification.

* It delves into calculating and interpreting various statistical measures:

- **Mean:** Explains its calculation, sensitivity to outliers, and use cases with weighted and unweighted data.

- **Median:** Defines the median, outlines its calculation process, and provides an approximation formula.

- **Mode:** Explains the concept of mode, multimodal distributions, and its relationship with mean and median.

- **Midrange:** Defines midrange and presents the formula for its calculation.

- **Range:** Defines range and its calculation.

- **Quantiles:** Introduces quantiles, including quartiles and percentiles, and explains interquartile range (IQR).

* It then details specific visualization techniques:

- **Boxplot:** Describes the elements of a boxplot and how they visually represent data distribution.

- **Variance and Standard Deviation:** Defines variance and standard deviation and their role in representing data dispersion.

- **Quantile Chart:** Explains the construction and interpretation of quantile charts for visualizing data distribution.

- **Quantile-Quantile Chart:** Introduces the use of Q-Q plots for comparing two univariate distributions.

- **Histogram:** Explains the use of histograms for visualizing data distribution through frequency counts in defined intervals.

- **Scatter Chart:** Discusses the application of scatter charts in visualizing the relationship between two numeric attributes and interpreting positive, negative, and null reciprocity.

- **Scatter Chart Matrix:** Explains how scatter chart matrices visualize datasets with more than four dimensions using multiple 3D scatter plots.

  

**2. Pixel-Based Visualization**
* This section describes pixel-based visualization, where pixel color intensity represents data values, useful for displaying large datasets and identifying correlations between dimensions.

* It explains how data points with multiple dimensions are represented across multiple windows.

**3. Visualization in Vector Space**
* This section highlights the limitations of pixel-based visualization in representing data density and introduces vector space visualization for multidimensional data representation in 2D.

* It explains the use of scatter charts and their limitations in representing dimensions beyond four.

* It then introduces scatter chart matrices for visualizing higher dimensional datasets using a grid of 2D scatter plots.

  

**4. Super Sphere Tree**
* This section introduces super sphere trees for visualizing large, hierarchical datasets, allowing users to focus on specific sections while maintaining the overall context.

* It explains the "fish eye" property, where the size of nodes changes based on their focus level.

  

**5. SOM (Self-Organizing Map)**
* This section introduces SOMs as neural networks that learn 2D representations of multidimensional data.

* It describes the architecture of a SOM, including the input and competition layers, and explains competitive learning for weight update based on minimizing distance between input and corresponding neurons.

* It then introduces WEBSOM, a specific application of SOM for visualizing document collections based on word frequency and identifying areas of high textual density.