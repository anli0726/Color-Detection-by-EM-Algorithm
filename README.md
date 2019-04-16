# Color-Detection-by-EM-Algorithm
Implemet Expectation-Maximization Algorithm to detect buoys color in underwater surrounding
For source video "dectectbuoy.avi" please go to this drive: https://drive.google.com/drive/folders/1RLMWjPMePjDLOU0lv_CiUbqIp24ZPwHX?usp=sharing

Introduction

This project use the concept of color segmentation using Gaussian Mixture Models and Expectation Maximization techniques.
The video sequence being used has been captured underwater and shows three buoys of different colors, namely yellow, orange and green. They are almost circular in shape and are distinctly colored. However, conventional segmentation techniques involving color thresholding will not work well in such an environment, since noise and varying light intensities will render any hard-coded thresholds ineffective. In such a scenario, by applying learning method to "learn" color distributions of the buoys and use that learned model to segment them. With combination of other techneiques, a tight segmentation of each buoy for the entire video sequence can be obtained.


Data Preparation

From a number of frames of the video extract cropped samples of the buoy and save them for further
training. Ideally, the tighter your bounding polygons, the better training results you will get. You may draw simple rectangles, but that will also bring unwanted regions on the sides of the buoys. The cropping result has been provide in the folder "Crop_Image" with images being seperated by the colors. The notation "filter" means the imgaes inside are blured by Gaussain filter.


Gaussian Mixture Models and EM Algorithm

In real life, many datasets can be modeled by Gaussian Distribution (Univariate or Multivariate). So it is intuitive to assume that the clusters come from different Gaussian distributions (hereinafter called Gaussians). In other words, it is tried to model the dataset as a mixture of several Gaussians. 
EM algorithm is a method to cluster data based on the above ideology. Suppose we have several data points, we can find K Gaussians to describe the sources of each point. However, since the means and variances for these Gaussians are unknown, we will have to extract these values from data points. What we have here is a chicken-egg problem.  Therefore, an appropriate initial guess is important: the variance of each Gaussian should be large enough such that all data points can be assigned to different Gaussian appropriately, while the converge time won’t be affected too much by such guess. In other words, if the initial guess of variances are too small, many data points will be assigned with extremely small posterior probabilities from certain Gaussian, which yields overflowing of posterior probabilities to be zero in program and thus they won’t be considered during calculation.
Initially, we assume random “starting points” and then compute for each point a probability that the point was generated by each one of the distributions. Then, iteratively, we tweak the parameters to try and maximize the likelihood of the data given those assignments. Repeating this sufficient times will guarantee a local optimum. The detail algorithm is written in the file "em.py" in the "Source_code" folder.



