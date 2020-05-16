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

## Pipeline to detect lane lines

Initially, the camera matrix and distortion co-efficient were used to undistort the raws images from the camera. Then for creating the binary image of the undistorted camera image, I used Sobel operator in the x-direction, the magnitude of the gradient found using the Sobel operator, “Value” value from the HSV color space and “Saturation” value from the HLS color space. The thresholds used for the different methods to create the binary images are given in table 1. The source points for drawing the polygon in the normal camera view and destination points for drawing the rectangle in the perspective transformed view used in the pipeline is given in table 2. The source and destination points were given to the OpenCV function “getPerspectiveTransform” to get the perspective transform matrix.

<p align="center">
  <b>Table 1: Parameters used for creating a binary image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_5e5118925b864f17a1c06db5b1cb855c~mv2.png/v1/fill/w_1290,h_330,al_c,lg_1/Screen%20Shot%202020-04-12%20at%209_16_25%20PM.png">
</p>

<p align="center">
  <b>Table 2: Source and destination points used for perspective transform</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_84489be224c247c8910ab6077a358537~mv2.png/v1/fill/w_1394,h_470,al_c/Screen%20Shot%202020-04-12%20at%209_23_28%20PM.png">
</p>

After applying calibration, thresholding, and a perspective transform to a road image, the sliding window method was used to get the initial estimate of the lane lines. After that new lane line fits were calculated by searching the activated pixels using the previous polynomial fit. 

<p align="center">
  <b>Original Image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_66cad3bf7a1f4eb09b682c2961b6846e~mv2.jpg/v1/fill/w_1280,h_720,al_c,q_90/Original_Image.jpg">
</p>

<p align="center">
  <b>Undistorted Image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_10b434f95b264fc1bfc2279778e07841~mv2.jpg/v1/fill/w_1280,h_720,al_c,q_90/Undistorted_Image.jpg">
</p>

<p align="center">
  <b>Perspective Transformation (Bird's eye view)</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_da0882bf60e94fb68c4e7109756c0de0~mv2.png/v1/fill/w_1930,h_670,al_c/Screen%20Shot%202020-04-09%20at%202_53_32%20PM.png">
</p>

<p align="center">
  <b>Binary Thresholded Image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_c38bc56b38bb40c6bd2b0fb6b6ffd206~mv2.jpg/v1/fill/w_1280,h_720,al_c,q_90/Binary_Image.jpg">
</p>

<p align="center">
  <b>Warped Binary Lane Lines Image</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_6f64d9b8470d474face9b4e863d5210a~mv2.png/v1/crop/x_6,y_41,w_1286,h_715/fill/w_1286,h_715,al_c/Screen%2520Shot%25202020-04-09%2520at%25202_51_e.png">
</p>

<p align="center">
  <b>Image with the calculated radius of curvature, offset and lanes lines</b><br>
  <img src="https://static.wixstatic.com/media/bb5837_6b0be90dc3c449a189121615d710bfe1~mv2.jpg/v1/fill/w_1280,h_720,al_c,q_90/Lane_lines_Image.jpg">
</p>
