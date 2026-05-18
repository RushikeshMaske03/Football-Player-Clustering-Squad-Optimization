# Football Player Clustering & Squad Optimization
## 📌Overview
This project applies Data Science, Unsupervised Machine Learning, and Optimization techniques on a dataset of 16K+ professional football players to analyze player attributes, 
segment players into meaningful archetypes, and identify cost-efficient strategies for building elite football squads.

The objective of this project is to build a data-driven framework capable of:
1. Grouping players based on playing style
2. Evaluating clustering quality using multiple metrics
3. Identifying optimal investment thresholds for squad building
4. Comparing current player performance vs future player potential

## 📂Dataset Information

Dataset contains:
- 17K+ professional football players
- Player demographics
- Market values and wages
- Skill attributes
- Positions
- Overall and potential ratings

## ⚙️Project Workflow

### 1. Exploratory Data Analysis:
Analyses Performed
- Top football-producing countries
- Age vs overall rating analysis
- Offensive player wage comparison
- Skill distribution analysis
- Overall vs potential comparison

### Key EDA Insights
#### 1. Peak Player Age:
Players typically reach peak performance between 29 – 34 years

#### 2. Highest Paid Offensive Position:
Right Winger(RW) receive the highest wages then followed by Left Winger(LW) and striker(ST)

#### 3. Football-Producing Countries:
European countries dominate elite football player.england at top then germany,spain,france

### 2. Data Preprocessing:
#### 1. Separated goalkeepers from outfield players:
Goalkeepers have completely different skill distributions compared to outfield players.

Including them caused:
- Cluster distortion
- Poor separation
- Outlier effects

Therefore Goalkeepers were analyzed separately.Clustering focused only on outfield players

#### 2. Handled missing values
missing values are handled by imputing with median.why median because Median is robust to outliers and prevents distortion caused by extremely high-value players.

#### 3. scaling
Standardized features using StandardScaler

## model traing(clustering)
### optimal k value finding
before implementing different models need to find optimal k value so by using elbow method optimal k is find.
<img width="350" height="200" alt="download" src="https://github.com/user-attachments/assets/6af2aeaf-d881-4e10-bbc5-adcdb9657df4" />

Three unsupervised learning algorithms were trained and evaluated KMeans,Agglomerative,Gaussian Mixture Model (GMM)

## 📊Model Performance
Since clustering is unsupervised learning Therefore, internal clustering metrics were used

|Metric|	Purpose|
|-------|---------|
|Silhouette Score|	Measures cluster separation & cohesion|
|Davies-Bouldin Index|	Measures cluster overlap (lower is better)|
|Calinski-Harabasz Score	|Measures cluster compactness & separation|

 |Model | Silhouette  |Davies_Bouldin  |Calinski_Harabasz  |
 |-------|------------|---------------|--------------------|
 |KMeans |   0.264845 |       1.300407    |    7069.673860 |  
   |  GMM   | 0.200654     |   1.609310       | 5328.428932|   
|Agglomerative    |0.197624  |      1.434836  |      4746.105325|
<img width="550" height="200" alt="download" src="https://github.com/user-attachments/assets/485b3510-6722-48c6-8694-ad0eb7425845" />

### Final Model Selection:
Final Model Selected is **KMeans Clustering**

because KMeans achieved:
1. Highest cluster separation
2. Lowest cluster overlap
3. Highest cluster compactness

### Cluster Stability Validation:
Bootstrap Stability Analysis was performed using Adjusted Rand Index (ARI)

#### Why Used
To verify whether clusters remain consistent across:
1. random sampling
2. multiple training iterations

### Stability Results:
|Model	|Stability ARI|
|-------|-------------|
|KMeans	|0.954707|
|GMM	|0.957913|
|Agglomerative	|0.352465|

results showed that KMeans achieved the very good stability score(0.9547) indicating that it produces the most consistent cluster assignments across different data samples.

<img width="350" height="180" alt="download" src="https://github.com/user-attachments/assets/b5fed361-88fe-4070-a7c2-6067c9cb54c6" />

### Cluster Interpretation: 
| Cluster|pace|   shooting|    passing|  dribbling|  defending |    physic |   
|---------|----|----------|---------|---------|--------------|-------------|
|0     |   72.609054 | 59.247412  |56.233199  |65.532901 | 33.553255 | 57.301632|
|1   |     59.272946|  35.479895  |47.613418 |50.776442| 61.292395 | 67.436189|
|2     |   69.476454|  58.559075 | 65.567119|  68.679906 | 61.276688  |70.148651|

- Cluster 0: High Pace,Good Dribbling,moderate shooting and passing,low defending that means These players Are fast,Good with ball,Not defensive,Not extremely physical Most likely: **Wingers / Supporting Attackers**
- cluster 1: High Defending,High Physic,moderate pace,low shooting and passing so This cluster represents **defensive players**.
- cluster 2: high physic,pace,dribbling,better passing and defending so this cluster represents **midfielders players**

###   0: "Attackers",
###   1: "Defenders",
###   2: "Midfielders"
<img width="350" height="180" alt="download" src="https://github.com/user-attachments/assets/1d234320-6079-4060-9273-96c03b767cee" />

<img width="350" height="180" alt="download" src="https://github.com/user-attachments/assets/e40bc785-c19b-44b5-a332-3923705fc0db" />


