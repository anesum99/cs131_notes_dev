---
title: Clustering
keywords: Segmentation, Cluster, Convergence, Algorithm, Convergence, Feature_Space, Smoothing, Evaluation
order: 10 # Lecture number for 2021
---




- [0 Intro to Segmentation](#0-Intro-to-Segmentation )
- [1 K-Means](#1-K-Means)
	- [1-1 Overview](#1-1-overview)
	- [1-2 Algorithm](#1-2-algorithm)
	- [1-3 Issues](#1-3-issues)
	- [1-4 Kmeans++](#1-4-Kmeans++)
	- [1-5 Smoothing](#1-5-cluster-count-choice)
	- [1-6 Cluster Count Choice](#1-6-cluster-count-choice)
- [3 Mean_shift:](#3-Mean_shift)
	- [2-1:](#3-1 )
	- [2-2:](#3-2)
	- [2-3:](#3-3)


## 0: Intro to Segmentation
<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/seg.png">
  <div class="segmentation">!</div>
</div>
- Some vision applications require us to define boundaries and specific features(e.g shapes on an image, scales on fish images e.t.c) of visual data
- this process of determining boundaries is called segmentation
- for simpler images, segmentation can be easily achieved by simple means to seperate, for instance, the main pixel information such as intensity
- such grouping of data(visual in this case) into meaningful categories is called clustering
- manually, this is nearly impossible and too tedious  with more complex images
- we therefore need a faster and more efficient way to achieve the same.

## 1 K-Means
###1-1 Overview
- K-Means aims to minimize the variance in data in each of K optimum groupings
- this is achieved by choosing centers to best reflect the data(pixel intensity) distribution on the image
- each data point is then allocated a cluster closest to it and as such minimize euclidean distance

\[begin{equation} \delta^{*} = argmin(frac{1}{N}\sum_{j=1}^{\N} \sum_{i=1}^{\k} \delta_{ij}(c_i-x_j)^{2}) \]
<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/clustering_eq.png">
  <div class="k means objective function"></div>
</div>
###1-2 Algorithm
1. initialize cluster centers C1, C2, C3,...Ck
2. clasify each data point with its closest center
3. update cluster centers as means of data points
4. update point classifications/allotment to centers
5. repeat 1-4 until the each center is the same as its predecessor(convergence)

<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/method-k-means-steps-example.png">
  <div class="k means algorithm"></div>
</div>

###1-3 Issues
- convergence could occur arbitrarily and give a non-optimum local minima
- such grouping of data(visual in this case) into meaningful categories is called clustering
###1-4 K-Means++
- an ugrade to K-Means to address bad local minima
- randomly choose first center
- update new centers proportionally with mean square distance(from centre) probability 
- repeat the center updates
- expected error is optimized at O(logK) 

###Smoothing
- pixels can be grouped on both pixel intensity and positional similarity basis 
- this ensures spatial coherence in the clustering
- Pros:
	-Simple and fast
	– onverges to a local minimum of the error function
	– Available implementations (e.g., in Matlab)
-Cons:
	–Need to pick K
	–Sensitive to initialization
	–Only finds “spherical” clusters
	–Sensitive to outliers
	
###1-6 Cluster counts choice  
- plot the objective function (sum of square distances) against successive values of K
- the optimal choice strikes a balance between maximum compression of the data using a single cluster
-  maximum accuracy is achieved by assigning each data point to its own cluster.

<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/choosing k.png">
  <div class="Choice of K"></div>
</div>

##Mean Shift
- Mean shift is very useful for clustering spatial information in addition to pixel intensity  
- The mean shift algorithm seeks a mode or local maximum of density of a given distribution

<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/meanshifT.png">
  <div class="Mean shift idea"></div>
</div>

<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/meanshff.png">
  <div class="Mean shift vector"></div>
</div>

1. Initialize random seed, and window W
2. Calculate center of gravity of the window
3. Translate the search window center to the mean
4. Repeat steps 2-3 until convergence 


<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/meanshift.png">
  <div class="k means algorithm"></div>
</div>

###Mean Shift Pros
	– Does not assume spherical clusters
	– Just a single parameter (window size)
	– Finds variable number of modes
	– Robust to outliers
###Mean Shift Cons
	– Output depends on window size
	– Computationally expensive
	– Does not scale well with dimension of feature space

### Speedup
- use basin of attraction by assigning points within a given radius to end point of the radius closest to local mean
- assign all points within each minor radius/circumference of the search path to the mode to reduce search points

<div class="fig figcenter fighighlight">
  <img src="{{ site.baseurl }}/assets/images/basin.png">
  <div class="basin of attraction">!</div>
</div>




