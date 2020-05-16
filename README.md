# **Complex Lane Lines Detection**
The project is focussed on detecting lane lines of the road with complicated curvature and determining vehicle position with respect to the center of lane using the footage from the camera mounted on the hood of the vehicle. 

## Steps involved in finding lane lines of the road: -

- The camera calibration matrix and distortion coefficients were computed using a set of chessboard images.
- Distortion correction was applied to the raw images.
- Color transforms and gradients were used to create a thresholded binary image.
- Perspective transform was applied to rectify binary image ("birds-eye view").
- Detected the lane pixels and fit to find the lane boundary using the Sliding window method.
- The curvature of the lane and vehicle position with respect to the center was determined.
- The detected lane boundaries were warped back onto the original image.
- Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle positions.

## Camera Calibration

An array named “object points” was created in order to store the 3-D coordinates of the chessboard corners in the world space. Similarly, an array named “image points” was created in order to store the 2-D coordinates of the chessboard corners in the image space. Then the calibration images, which included 16 chessboard images taken by the vehicle's camera, were iterated to get the coordinates of the chessboard corners for each image using OpenCV function called “findChessboardCorners”. The algorithm was developed in such a way that if the corners were detected in any calibration image, the coordinates of the corners of that chessboard image in the image plane will be appended in the array “image points”. “object” is a mess grid which will be same for a given chessboard size is appended in the array “object points” every time when corners were detected. The OpenCV function “calibrateCamera()” was used to get the camera matrix and distortion co-efficient using the object points and image points. This camera matrix and distortion co-efficient were given as an input to the OpenCV function “undistort()” to obtain the undistorted image.

<p align="center">
  <b>Undistorted Chessboard image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_e9efb4c1a09f414ab38f2aa36b2b0c52~mv2.png/v1/fill/w_1726,h_506,al_c/Screen%20Shot%202020-04-09%20at%202_51_00%20PM.png">
</p>

