# Trend Detection  
![Python](https://img.shields.io/badge/Python-3.7.13-blue.svg) ![Numpy](https://img.shields.io/badge/NumPy-1.21.6-range.svg) ![Pandas](https://img.shields.io/badge/Pandas-1.3.5-range.svg) ![Matplotlib](https://img.shields.io/badge/Matplolib-3.2.2-range.svg) ![ScikitLearn](https://img.shields.io/badge/ScikitLearn-1.0.2-range.svg) ![DTAIDistance](https://img.shields.io/badge/DTAIDistance-2.3.6-range.svg)

## Author  
<span> - &copy; Tom Wu (<a href="https://github.com/YenLinWu">Github</a>) </span>  

## Algorithm  
<img src='./Images_of_README/algorithm.png'>

[1] Dynamic Time Warping, DTW [ [Studying Note](https://colab.research.google.com/github/YenLinWu/Trend_Detection/blob/main/Dynamic_Time_Warping/Studying_Note.ipynb) ]    
[2] Multidimensional Scaling, MDS [ [Studying Note](https://hackmd.io/@20gd3hLfS7G4xfz9rKqycw/multidimensional_scaling) ][ [Sample Code](https://colab.research.google.com/github/YenLinWu/Trend_Detection/blob/main/Multidimensional_Scaling/Multidimensional_Scaling.ipynb) ]

## Proof Of Concept
* Sample Dataset  
The sample dataset in this work is from a real panel process by Electronic Data Capture(EDC) system. There are 95,419 data of the test item between 1st February 2021 and 19th January 2022, with 11 times parts replacement.  
<p align='left'>
  <img src='./Images_of_README/sample_data.png' width='250'>  

* Normal Pattern    
The overall pattern of the sample dataset is shown in the following figure. First, the normal pattern must be defined. We define the normal pattern by the data from 2021/2/12 01:54:44 to 2021/2/19 15:17:28, i.e., the normal pattern is in [15784, 25000] time step subinterval.  
<p align='left'>
  <img src='./Output_Images_of_POC/Normal_and_Test_Data.png' width='750'>  
  
* Test Data   
Now, we will detect the pattern of each test data (Test 1~6 in the above figure) by comparing each test data and defined normal data.  
  
* Model Performance  
  From the above figure, we intuitively get the feeling that the trend of the Test 5 and Test 6 are obviously flat. This algorithm confirms our feelings! This model detector can effectively distinguish differences in trends and the performance is stable. We can view the detection results of each test data from the following figure and gif.       
    
 
<details>  
<summary> Test 1 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_1.png' width='400'>  
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_1.gif' width='390'>  
      
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_1.gif)  
</details>   

<details>  
<summary> Test 2 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_2.png' width='400'>
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_2.gif' width='390'>  
        
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_2.gif)  
</details>   

<details>  
<summary> Test 3 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_3.png' width='400'>
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_3.gif' width='390'>  
          
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_3.gif)  
</details>   

<details>  
<summary> Test 4 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_4.png' width='400'>
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_4.gif' width='390'>  
          
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_4.gif)  
</details>   

<details>  
<summary> Test 5 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_5.png' width='400'>
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_5.gif' width='390'>  
          
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_5.gif)  
</details>   

<details>  
<summary> Test 6 Result </summary>
  <p align='left'>
  <img src='./Output_Images_of_POC/Smoothing_Normal_and_Test_6.png' width='400'>
  <img src='./Output_Images_of_POC/Detection_Output_of_Test_6.gif' width='390'>  
          
  [[View original gif]](./Output_Images_of_POC/Detection_Output_of_Test_6.gif)  
</details>   

## References  
**[1]** Similarity Measures and Dimensionality Reduction Techniques for Time Series Data Mining, Carmelo Cassisi, Placido Montalto, Marco Aliotta, Andrea Cannata and Alfredo Pulvirenti, September 2012.  [ [Download Link](https://www.intechopen.com/chapters/39030) ]
</br>   
**[2]** Identification of Out-of-Trend Stability Results, PhRMA CMC Statistics and Stability Expert Teams, April 2003. [ [Download Link](http://alfresco-static-files.s3.amazonaws.com/alfresco_images/pharma/2014/08/22/5d9c565f-81ff-4879-aaed-20acd24d0335/article-52982.pdf) ]    
</br> 
**[3]** Methods for Identifying Out-of-Trend Data in Analysis of Stability Measurements–Part I: Regression Control Chart, Máté Mihalovits and Sándor Kemény, November 2, 2017. [ [Download Link](https://cdn.sanity.io/files/0vv8moc6/pharmtech/e80e5dbb15ba554cd2a9aaa7200c6ef665ffc019.pdf) ] [ [Reading Note](https://colab.research.google.com/github/YenLinWu/Trend_Detection/blob/main/Regression_Control_Chart/Reading_Note.ipynb) ] 
</br>   
**[4]** Methods for Identifying Out-of-Trend Data in Analysis of Stability Measurements—Part II: By-Time-Point and Multivariate Control Chart, Máté Mihalovits and Sándor Kemény, December 2017. [ [Download Link](http://alfresco-static-files.s3.amazonaws.com/alfresco_images/pharma/2017/12/13/fd4d33b3-f2a5-41ec-8f57-a29194945342/PT1217_038-043_PeerReviewed.pdf) ] 
</br>  
**[5]** Learning Conﬁdence for Out-of-Distribution Detection in Neural Networks, Terrance DeVries and Graham W. Taylor, February 2018.  [ [Download Link](https://arxiv.org/pdf/1802.04865.pdf) ]
</br> 

## Further Readings    

> Articles   

**[1]** [Time Series Similarity Using Dynamic Time Warping -Explained](https://medium.com/walmartglobaltech/time-series-similarity-using-dynamic-time-warping-explained-9d09119e48ec), Abhishek Mishra, December 2020.    
**[2]** [Timeseries Classification: KNN & DTW](https://nbviewer.org/github/markdregan/K-Nearest-Neighbors-with-Dynamic-Time-Warping/blob/master/K_Nearest_Neighbor_Dynamic_Time_Warping.ipynb), Mark Regan, October 2018.

> Programming

**[1]** [dtw-python: Dynamic Time Warping in Python](https://dynamictimewarping.github.io/python/)
</br> 
**[2]** [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)
</br> 

## Acknowledgement    
Please cite this repository [Trend Detection](https://github.com/YenLinWu/Trend_Detection) if you use it.  
