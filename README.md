# Complex Lane Lines Detection
The project is focussed on detecting lane lines of the road with complicated curvature and determining vehicle position with respect to the center of lane using the footage from the camera mounted on the hood of the vehicle. 

**Steps involved in finding lane lines of the road: -**

- The camera calibration matrix and distortion coefficients were computed using a set of chessboard images.
- Distortion correction was applied to the raw images.
- Color transforms and gradients were used to create a thresholded binary image.
- Perspective transform was applied to rectify binary image ("birds-eye view").
- Detected the lane pixels and fit to find the lane boundary using the Sliding window method.
- The curvature of the lane and vehicle position with respect to the center was determined.
- The detected lane boundaries were warped back onto the original image.
- Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle positions.
