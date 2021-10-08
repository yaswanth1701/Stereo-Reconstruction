# STEREO-RECONSTRUCTION
Stereo reconstruction is a method by which we obtain the depth of points in a particular scene by using a pair of stereo image.
## what are stereo images:
pair images of same scene which are taken from a different angle or perspective
## basic principal involved
- epipolar geomerty:




![image](https://user-images.githubusercontent.com/92177410/136604715-c793de16-b74c-4a5a-9d92-771703ec39cb.png)


epipolar geomerty gives us a geometric relation between pair of setreo images from which depth of a point can be calculated.
This geometric relation is known as epipolar constraint according to it a point in first images lies on the epipolar line of second image.

epipolar line is line of intersection of image  plane and palne containing optical centres of stereo cameras and point in real world.



epipolar geomerty basically converts 2D search into 1D search for stereo correspondance.
### rectified epipolar geomerty:
In rectified epipolar geomerty stereo are arrange in such way that their angle rotation is zero (ie R=0).this make our search for setreo correspondance much easy.

![image](https://user-images.githubusercontent.com/92177410/136622023-1e12228b-7770-430a-9ba3-36be4357366d.png)

now we need to search only along the x direction.
## camera calibration :

![image](https://user-images.githubusercontent.com/92177410/136622429-1d8e8675-c7d3-4106-8c01-02ece1fd97b5.png)
![image](https://user-images.githubusercontent.com/92177410/136624283-b22c6c1c-99c4-4578-b971-9cba35c4bdd1.png)


externsic camera matrix:

first of all we need to convert our points from world coordinate system to camera coordinate system this is done  by the use of externsic camera matrix 



![image](https://user-images.githubusercontent.com/92177410/136623326-5e20a029-3cc2-42ae-8748-c9d4e04480a7.png)

in general we need to know atleast 6 points real world coordinates and their corresponding image coordinate to calculate externsic parameters.
Internsic camera matrix :
after getting our camera coordinates of a point we need convert 3D points(X,Y,Z) into 2D image coordinates(U,V) for this we use internsic camera matrix.

![image](https://user-images.githubusercontent.com/92177410/136624644-75b0dbe7-7f8d-494d-bd6e-46dc7200520d.png)
here Fx and Fy are focal length 
S skew of camera 
X0 and Y0 are camera offsets 
## disparity and disparity maps:
disparity is defined as the difference of position of a sepcific point or object in right image to left image.

![image](https://user-images.githubusercontent.com/92177410/136625358-0ada55c3-a154-4976-a690-924cdf94f61d.png)
the difference in position gives us the depth.
relation between disparity and depth:

Z=B*f/D

where, 
f is focal length  
B is baseline length 
Z is depth 
D is disparity 
using epipolar geomerty we obtained depth by calculating disparity.
disparity map show the disparity of each point in the scene in form a image or map its like a graph of disparity 
### stereoreprojection of points :
now after obtaining the depth we need to calculate points position in real world  to get the depth map of the scene.
for obataining the position or coordinate of points we use calibration matrix in reverse sense this known as stereo reprojection.
## Algorithm:
1) first we install opencv and matplotlib library
2) then we load our images in grayscale using _cv.imread_ which takes two arguments first image location and second is image colour
3) after loading our images we use cv.StereoSGBM_create or cv.StereoBM_create
- argumets of _cv.StereoSGBM_create_
- 







