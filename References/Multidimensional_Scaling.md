<style>
  body[style],
  body[style*="background-color: white;"]
  {
    background-color: #1e1e1e !important;
  }
  body
  {
    color: #abb2bf;
    background-color: #ae1e !important;
          stroke-width: 2;
      stroke: #aaf;
      fill: #aa6;
      font-family: Microsoft JhengHei;
      font-weight: 500;
      font-style: normal;
  }
    .markdown-body pre.sequence-diagram.actor {
    }
</style>
# Multidimensional Scaling, MDS <br/> 多維標度法

## Abstract 

* MDS is a technique that creates a map displaying the relative positions of a number of objects, given only a table of the distances between them.( <font color=#FFFF00>利用低維度的空間，來呈現原始數據集中樣本間彼此的"距離"。</font> ) 
* In general, MDS is a technique used for analyzing **similarity(相似性)** or **dissimilarity(相異性)** data. It attempts to model similarity or dissimilarity data as distances in a geometric spaces.( <font color=#FFFF00>MDS 可用來分析資料的相似性或相異性。</font> )  
  * Similarities represent how close (in some sense) two objects are.
  * Dissimilarities represent the distance between two objects. MDS algorithms use the dissimilarities directly.

* There exists two types of MDS algorithm: **metric(公制)** and **non metric(非公制)**.

## Introduction 

Consider the following set of data:

|Label|X|Y|
| -------- | -------- | -------- |
|A|1|5|
|B|1|5|
|C|1|5|
|D|3|5|

- The actual distance between two points $i$ and $j$ may be computed numerically using the Euclidean distance formula: 
\begin{aligned}d_{ij}=\sqrt{\sum_{k=1}^{p} (x_{ik}-x_{jk})^2}\end{aligned}
where $p$ is the number of dimensions. 
* These distances are arranged in matrix format as follows:   
  
  <font color=#00FF00>*Distance Matrix(距離矩陣)*</font>
  ||A|B|C|D|
  |:---|:---|:---|:---|:---|
  |A|0.00000|1.00000|4.00000|2.82843|
  |B|1.00000|0.00000|3.00000|2.23607|
  |C|4.00000|3.00000|0.00000|2.82843|
  |D|2.82843|2.23607|2.82843|0.00000|
  
  Note that since the distance from A to D is the same as the distance from D to A, **the distance matrix is symmetric**. The final distance matrix will be:
  
  **Upper-Triangular Distance Matrix**
  ||A|B|C|D|
  |:---|:---|:---|:---|:---|
  |**A**|0.00000|1.00000|4.00000|2.82843|
  |**B**||0.00000|3.00000|2.23607|
  |**C**|||0.00000|2.82843|
  |**D**||||0.00000|

* The task attempted by MDS is that 
  <font color=#00FF00>**<p align='right'>given only a distance matrix, 
  find the original data so that a map (scatter plot) of the data may be drawn.</p>**</font>
  
Some of the difficulties facing :
1. As the number of objects increases, the possible number of dimensions increases as well. If we have three objects, these will at most define a two-dimensional plane. With four objects, we will usually find a three-dimensional space. And so on, <font color=#FF0000>with each new object adding one more possible dimension.</font> ( <font color=#FFFF00>隨著資料集樣本數的增加，可降維的空間維度也隨之增加。</font> )  
2. If the data are shifted in such a way that their positions relative to each other are maintained (rotated, translated, or transposed), the computed distance matrix will be the same. Hence, <font color=#FF0000>the distance matrix could have come from numerous sets of data.</font> ( <font color=#FFFF00>無法僅從樣本彼此間的距離，明確地得知彼此間的相對位置。</font> )
3. When the distances themselves are not actually known. We might only be given knowledge, of their relative size.( <font color=#FFFF00>實務上，距離矩陣中的數值，往往不是樣本彼此間的真實幾何距離，可能存有量測的誤差，或者，不代表樣本彼此間的幾何距離，而是某種特性(或定性)的相對大小，例如 : 溫度的相對差異等。</font> )</font> 

## Goodness of Fit(適合度)

In the case of MDS, we are trying to model the distances. Hence, the most obvious choice for a goodness-of-fit statistic is one based on the differences between the actual distances and their predicted values. Such a measure is called <font color=#00FF00>***stress***</font> and is calculated as values:
\begin{aligned}\text{stress}=\sqrt{\frac{\sum(d_{ij}-\hat d_{ij})^2}{\sum d_{ij}^2}}\end{aligned}
where $\hat d_{ij}$ is predicted distance based on the MDS model. 
In Kruskal's original paper [[3](https://link.springer.com/article/10.1007/BF02289565)] gave following advise about stress values based on his experience:

|Stress|Goodness of Fit|
|---|---|
|0.000|perfect|
|0.025|excellent|
|0.050|good|
|0.100|fair|
|0.200|poor|

More recent articles caution against using a table like this since <font color=#FF0000>acceptable values of stress depends on the quality of the distance matrix and the number of objects in that matrix.</font>
    
## Metric and Non-Metric MDS 
### Metric MDS(公制 MDS) 

The elements of a **distance matrix $D$**, denoted $d_{ij}$ , may be calculated from $X=\{\mathbb{X}_1, \mathbb{X}_2, \cdots, \mathbb{X}_n\}$, where $\mathbb{X}_i=(x_{i1}, x_{i2}, \cdots, x_{ip})^T$, using the following formula  
\begin{align}d_{ij} &= \sqrt{\sum_{k=1}^{p} (x_{ik}-x_{jk})^2}\\ &= (\mathbb{X}_i-\mathbb{X}_j)^T(\mathbb{X}_i-\mathbb{X}_j)=||\mathbb{X}_i-\mathbb{X}_j|| \end{align}
The steps in the classical MDS algorithm are as follows:  

  - Step 1: 
  Define $A = \big[ −d_{ij}^2/2 \big]_{n\times n}$.  
  - Step 2: 
  Let $B=\big[ b_{ij} \big]_{n\times n}=\big[ \mathbb{X}_i^T\mathbb{X}_j \big]_{n\times n}$ be a Kernel matrix(內積矩陣). From $A\equiv[a_{ij}]_{n\times n}$ calculate $B = \big[a_{ij}-a_{i.}-a_{.j}+a_{..}\big]$, where $a_{i.}$ is the average of all $a_{ij}$ across $j$, we obtain
    $$B = CAC,$$ where $C=I-\frac{1}{n}E$ and $E$ is the all-ones matrix.
  - Step 3:  
  Because $B$ is a [symmetric matrix(對稱矩陣)](https://mathworld.wolfram.com/SymmetricMatrix.html), it's [positive semi-definite(半正定)](https://mathworld.wolfram.com/PositiveSemidefiniteMatrix.html) and orthogonally diagonalizable(正交對角化), i.e., $$B=QMQ^T \quad\quad\cdots\cdots\text{正交對角化}$$
  where $M=diag(\lambda_1,\cdots,\lambda_n)$ with eigenvalues $\lambda_1\geq\cdots\geq\lambda_n\geq0$ and corresponding eigenvectors $Q=[v_1 \cdots v_n]$ with $Q^T=Q^{-1}$.
  
In general case $n>p$, there are not more than $p$ nonzero eigenvalues. Therefore, we get
\begin{align}B &=\begin{bmatrix}v_1 & \cdots & v_p\end{bmatrix}\begin{bmatrix}
\lambda_1&& \\ &\ddots& \\ &&\lambda_p \end{bmatrix}\begin{bmatrix}v_1^T\\\vdots\\v_p^T\end{bmatrix}\\ &=\begin{bmatrix}\sqrt{\lambda_1}v_1 & \cdots & \sqrt{\lambda_p}v_p\end{bmatrix}\begin{bmatrix}\sqrt{\lambda_1}v_1^T\\\vdots\\\sqrt{\lambda_p}v_p^T\end{bmatrix},\end{align}

then new coordinate matrix is defined as  $X \equiv\begin{bmatrix}\sqrt{\lambda_1}v_1 & \cdots & \sqrt{\lambda_p}v_p\end{bmatrix}$. Note that $X$ is not unique because of, let $X'=XP_{p\times p}$ with $P^T=P^{-1}$, i.e., $P_{p\times p}$ is an orthogonal matrix, $$X' X'^{T}=(XP)(XP)^T=XPP^TX^T=XX^T=B.$$
  
<font color=#00FF00>The classical solution is optimal in the least-squares sense. That is, when a direct solution is possible (i.e., when $D$ is truly a Euclidean distance matrix), the solution, $X$, minimizes the sum of squared differences between the actual $d_{ij}$’s (elements of $D$) and the $\hat d_{ij}$’s based on $X$.</font> Another way of saving this is that it minimizes the value of stress, where stress was defined above.

### Non-Metric MDS(非公制 MDS)  

* Implicit in the metric MDS is the assumption that there is a true configuration in $p$ dimensions, i.e., **that $D$ is a distance matrix.**
* Often, it is more realistic to assume a less stringent relationship between the observed distances (or dissimilarities) $d_{ij}$ and the true distances, denoted $\delta_{ij}$. That is, suppose we assume that
\begin{aligned}d_{ij}=f(\delta_{ij}+e_{ij})\end{aligned}
where $e_{ij}$ represents errors of measurements, distortions(扭曲；變形), etc. Also, we assume that $f(x)$ is an unknown, monotonically increasing function.  
* <font color=#00FF00>For this model, the only information we can use is the **rank order** of the $d_{ij}$.</font> Usually, this approach is used when $D$ is simply a dissimilarity matrix rather than a true distance matrix. This assumption is often more plausible in practical situations.
* An algorithm to produce a solution based only on the **rank order** information was provided by Kruskal (1964). We note that <font color=#00FF00>Kruskal’s algorithm minimizes stress.</font> 

## Number of Dimensions  

One of the main tasks the analyst has is determining the number of dimensions in the MDS model. 
* <font color=#00FF00>One of the goals of the MDS analysis is to keep the number of dimensions as small as possible. Usually, the analyst will anticipate select two or, at most, three dimensions.</font> 
* If more are required, you may decide that MDS is not appropriate for your data.

## References  

[1] [Multidimensional Scaling](https://ncss-wpengine.netdna-ssl.com/wp-content/themes/ncss/pdf/Procedures/NCSS/Multidimensional_Scaling.pdf) from [NCSS Statistical Software](https://www.ncss.com/).  
[2] [古典多維標度法(MDS)](https://ccjou.wordpress.com/2013/05/29/%E5%8F%A4%E5%85%B8%E5%A4%9A%E7%B6%AD%E6%A8%99%E5%BA%A6%E6%B3%95-mds/), May 2013, 周志成教授.  
[3] [Multidimensional scaling by optimizing goodness of fit to a nonmetric hypothesis](https://link.springer.com/article/10.1007/BF02289565), March 1964, J. B. Kruskal.  