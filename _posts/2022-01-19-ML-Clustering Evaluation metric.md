---
title: ML/Clustering Evaluation
date: 2022-01-19 00:00:01
categories:
- ML
tags:
- Clustering
- Evaluation Metric
- Silhouette 
---

# [ML/Clustering] Evaluation
비지도 학습의 특성상 어떠한 지표라도 정확하게 성능을 평가하기 어렵지만,일반적으로 **실루엣 분석**을 많이 사용한다. 

대부분의 군집화 데이터는 비교할만한 타깃레이블을 가지고 있지 않는다. 또한 군집하는 분류와 유사하게 보일 수 있으나 성격이 많이 다르다.  <br>데이터 내에 숨어있는 별도의 그룹을 찾아서 의미를 부여하거나 동일한 분류값에 속하더라도 그 안에서 더 세분화된 군집화를 추구하거나 더 넓은 군집화 등의 영역을 가지고 있다.

---

## Silhouette Method
군집화 방법중 하나로 각 군집간의 거리가 얼마나 효율적으로 분리 되어 있는지를 나타낸다. 효율적으로 잘 분리됐다는 것은 다른 군집과의 거리는 떨어져 있고 동일 군집끼리의 데이터는 서로 가깝게 뭉쳐있다는 의미다.

실루엣분석은 실루엣계수를 기반으로 한다. <br>실루엣계수는 개별 데이터가 가지는 군집화 지표다. <br>개별 데이터가 가지는 실루엣 계수는 해당 데이터가 같은 군집 내의 데이터와 얼마나 **가깝게 군집화** 되어있고 다른 군집에 있는 데이터와는 얼마나 **멀리 분리** 되어있는지를 나타내는 지표다.

<img src='https://drive.google.com/uc?export=download&id=1jrViQfj9hwcfla3Rd0oiWGIrfssYWKOy' width=450>

---

### Silhouette coeffiecient

특정 데이터 포인트의 실루엣 계수는 해당 데이터포인트와 **같은 군집 내**에 있는 다른 데이터포인트와의 거리를 평균한 값 a(i) = 평균(a12,a13,a14), 해당 데이터포인트가 **속하지 않는 군집중 가장 가까운 군집**과의 평균거리 b(i) = 평균(b15,b16,b17,b18)를 기반으로 계산된다. <br>두 군집간의 거리는 b(i)-a(i)으로 이값을 정규화하기 위해 max 거리값으로 나눠준다. <br>i번째 데이터 포인트의 실루엣계수 s(i)는 다음과 같다.

$$
s(i) = \frac{(b(i)-a(i))}{Max((a(i),b(i)))}
$$

실루엣계수는 -1에서 1 사이의 값을 가지며 1에 가까워질수록 군집간의 거리가 크다는 뜻이다. 음수가 나올경우, 아예 다른 군집에 데이터포인트가 할당되었음을 의미한다.

좋은 군집화가 되려면아래 두 조건을 만족해야한다.
1. 전체 실루엣계수의 평균값, 즉 사이킷런의 silhouette_score() 값은 0-1 값을 가지며 1에 가까울 수록 클러스터가 분리가 잘 되었음을 뜻함
2. 전체 실루엣계수의 평균값과 더불어 개별 군집의 평균값의 편차가 크면 안된다. <br>즉 , 개별 군집의 실루엣계수 평균값이 전체 실루엣계수의 평균값에서 크게 벗어나지 않는것이 중요하다. <br>특정 군집만 실루엣계수가 매우 낮을 경우 좋은 군집화 조건이라고 할 수 없다.<br>그러므로 일부 클러스터의 실루엣 계수가 높다고 해서 반드시 최적의 군집 수로 군집화가 잘 되었다고 볼 수는 없다.

---

## Tutorial 
`silhouette_samples`, `silhouette_score` 를 활용해서 각 샘플별 클러스터별 실루엣 계수를 구해보자.
[ref](https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html) 

```python
from sklearn.datasets import make_blobs
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_samples, silhouette_score

import matplotlib.pyplot as plt
import matplotlib.cm as cm
import numpy as np

# Generating the sample data from make_blobs
# This particular setting has one distinct cluster and 3 clusters placed close
# together.
X, y = make_blobs(
    n_samples=500,
    n_features=2,
    centers=4,
    cluster_std=1,
    center_box=(-10.0, 10.0),
    shuffle=True,
    random_state=1,
)  # For reproducibility

range_n_clusters = [2, 3, 4, 5, 6]

for n_clusters in range_n_clusters:
    # Create a subplot with 1 row and 2 columns
    fig, (ax1, ax2) = plt.subplots(1, 2)
    fig.set_size_inches(18, 7)

    # The 1st subplot is the silhouette plot
    # The silhouette coefficient can range from -1, 1 but in this example all
    # lie within [-0.1, 1]
    ax1.set_xlim([-0.1, 1])
    # The (n_clusters+1)*10 is for inserting blank space between silhouette
    # plots of individual clusters, to demarcate them clearly.
    ax1.set_ylim([0, len(X) + (n_clusters + 1) * 10])

    # Initialize the clusterer with n_clusters value and a random generator
    # seed of 10 for reproducibility.
    clusterer = KMeans(n_clusters=n_clusters, random_state=10)
    cluster_labels = clusterer.fit_predict(X)

    # The silhouette_score gives the average value for all the samples.
    # This gives a perspective into the density and separation of the formed
    # clusters
    silhouette_avg = silhouette_score(X, cluster_labels)
    print(
        "For n_clusters =",
        n_clusters,
        "The average silhouette_score is :",
        silhouette_avg,
    )

    # Compute the silhouette scores for each sample
    sample_silhouette_values = silhouette_samples(X, cluster_labels)

    y_lower = 10
    for i in range(n_clusters):
        # Aggregate the silhouette scores for samples belonging to
        # cluster i, and sort them
        ith_cluster_silhouette_values = sample_silhouette_values[cluster_labels == i]

        ith_cluster_silhouette_values.sort()

        size_cluster_i = ith_cluster_silhouette_values.shape[0]
        y_upper = y_lower + size_cluster_i

        color = cm.nipy_spectral(float(i) / n_clusters)
        ax1.fill_betweenx(
            np.arange(y_lower, y_upper),
            0,
            ith_cluster_silhouette_values,
            facecolor=color,
            edgecolor=color,
            alpha=0.7,
        )

        # Label the silhouette plots with their cluster numbers at the middle
        ax1.text(-0.05, y_lower + 0.5 * size_cluster_i, str(i))

        # Compute the new y_lower for next plot
        y_lower = y_upper + 10  # 10 for the 0 samples

    ax1.set_title("The silhouette plot for the various clusters.")
    ax1.set_xlabel("The silhouette coefficient values")
    ax1.set_ylabel("Cluster label")

    # The vertical line for average silhouette score of all the values
    ax1.axvline(x=silhouette_avg, color="red", linestyle="--")

    ax1.set_yticks([])  # Clear the yaxis labels / ticks
    ax1.set_xticks([-0.1, 0, 0.2, 0.4, 0.6, 0.8, 1])

    # 2nd Plot showing the actual clusters formed
    colors = cm.nipy_spectral(cluster_labels.astype(float) / n_clusters)
    ax2.scatter(
        X[:, 0], X[:, 1], marker=".", s=30, lw=0, alpha=0.7, c=colors, edgecolor="k"
    )

    # Labeling the clusters
    centers = clusterer.cluster_centers_
    # Draw white circles at cluster centers
    ax2.scatter(
        centers[:, 0],
        centers[:, 1],
        marker="o",
        c="white",
        alpha=1,
        s=200,
        edgecolor="k",
    )

    for i, c in enumerate(centers):
        ax2.scatter(c[0], c[1], marker="$%d$" % i, alpha=1, s=50, edgecolor="k")

    ax2.set_title("The visualization of the clustered data.")
    ax2.set_xlabel("Feature space for the 1st feature")
    ax2.set_ylabel("Feature space for the 2nd feature")

    plt.suptitle(
        "Silhouette analysis for KMeans clustering on sample data with n_clusters = %d"
        % n_clusters,
        fontsize=14,
        fontweight="bold",
    )

plt.show()
```
클러스터 수를 4로 지정했을때 실루엣계수가 균등하고 클러스터가 잘 분리 된것으로 확인 할 수 있다.

<img src='https://drive.google.com/uc?export=download&id=1-4Rwp6dyMhw1VSCVZ7U8ce8-yRCF1klF' width=600>
<img src='https://drive.google.com/uc?export=download&id=1-6blZheLy_yLLHc9PjZMqjmXxMJsjtXR' width=400>

---

##  Practice

- Clustering [link](https://github.com/ominiv/Plot_Collection/blob/master/Silhouette_analysis.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적

