# STEREO-RECONSTRUCTION
Stereo reconstruction is a method by which we obtain the depth of points in a particular scene by using a pair of stereo image.
## what are stereo images:
pair images of same scene which are taken from a different angle or perspective
##  Algorithm explanation:
### disparity and disparity maps:
disparity is defined as the difference of position of a sepcific point or object in right image to left image.
![image](https://user-images.githubusercontent.com/92177410/136625358-0ada55c3-a154-4976-a690-924cdf94f61d.png)

Z=B*f/D

where, 
f is focal length  

B is baseline length 

Z is depth 

D is disparity 

using epipolar geomerty we obtained depth by calculating disparity
#### principle :
 epipolar geomerty:




![image](https://user-images.githubusercontent.com/92177410/136604715-c793de16-b74c-4a5a-9d92-771703ec39cb.png)


epipolar geomerty gives us a geometric relation between pair of setreo images from which depth of a point can be calculated.
This geometric relation is known as epipolar constraint according to it a point in first images lies on the epipolar line of second image.

epipolar line is line of intersection of image  plane and palne containing optical centres of stereo cameras and point in real world.



epipolar geomerty basically converts 2D search into 1D search for stereo correspondance.
#### code:
1) first we install opencv and matplotlib library
2) we load our images in grayscale using _cv.imread_ which takes two arguments first is image location and second is image colour
3) after loading our images we use _cv.StereoSGBM_create_ or _cv.StereoSGBM_create_ .
#####  paramters of _cv.StereoSGBM_create_:
* mindisparity
* numDisparities = (maxdisparity - mindisparity):this parameter much divisble by 16
* blockSize(should be a odd number)
* P1 & P2(controls smoothness of disparity map)
* uniqueness Ratio
* speckleWindowSize
* speckleRange

[click here](https://docs.opencv.org/4.5.3/d2/d85/classcv_1_1StereoSGBM.html) for more parameters 

4) now compute disparity using _stereo.compute_
##### parameters of  _stereo.compute_ :
* right image 
* left image

5) we obtained disparity map. 
6) apply gaussian blur on diaprity map for better results
7) for visualization of disparity map we use matplotlib function _plt.imshow_
#####  parameters of _plt.imshow_
*  disparity or any other image we want to show.
*  colormap(for current project we use **jet** colormap)

for more info about colormaps [click here.](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

8) then we pass _plt.show_ to display output.
### reprojection of image points(u,v) to 3D coordinates:
#### principle:

to  convert 3D points(X,Y,Z) into 2D image coordinates(U,V) for this we use internsic camera matrix.

![image](https://user-images.githubusercontent.com/92177410/136624644-75b0dbe7-7f8d-494d-bd6e-46dc7200520d.png)

here Fx and Fy are focal length 

S skew of camera 

X0 and Y0 are camera offsets
we  use calibartion matrix to obtain 3D coordinates using disparity.
#### code :

9) after visualization we use _cv.reprojectImageTo3D_ to obtain 3D coordinates of points.
##### parameters of _cv.reprojectImageTo3D_ :
* diparity map
* calibration matrix (numpy array containing camera parameters)
10) obtain points colour using _cv.cvtColor_
##### parameters of _cv.cvtColor_ :
* image
* color space
11) thresholding 3D points to remove points having no diparity or very large depth.
### creating point cloud:
#### code:
12) creating point cloud using ply file 

13) defining elements and property of elemenst using ply header 

14) save all the points and their respective in color in _.ply_ file

15) finally open _.ply_ file in meshlab to visualize the point cloud 

## samples images:
### right image:

![im0](https://user-images.githubusercontent.com/92177410/136657519-c2395431-d5b7-43fc-a766-90c4100e3322.png)

### left image:
![im1](https://user-images.githubusercontent.com/92177410/136672788-222a72bb-4c28-4a8c-a0b2-0cc12e4ce558.png)

### disparity map:
<img width="287" alt="bike" src="https://user-images.githubusercontent.com/92177410/136672832-91e53378-8655-43e3-b125-5a6fb6f27dad.png">
### result:



