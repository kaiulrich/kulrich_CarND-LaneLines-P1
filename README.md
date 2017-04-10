#** Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline.

My pipeline consisted of 7 steps.
 
* Converted the images to grayscale. 
* Gaussian smoothing to reduce image noise and reduce detail. I used a a kernel size of 5. has enough less blurring and keeps enough struktur.
* Process of Canny edge detection. I used a low_threshold = 50 and high_threshold = 150.  
* Masking the Region of Interest. It is an rhomb with (0, max_y),(460, 325), (500, 325), (max_x, max_y)
* Extract linesegments via hough transformation (rho = 1, theta = np.pi/180, threshold = 30, min_line_length = 1, max_line_gap = 2)
* filter and split segments to 2 lists, extrapolate 2 lines from the segments and draw this two lines
* merge the original and line picture

In order to draw a single line on the left and right lanes, I modified the draw_lines() function.
First I sorted the linesegments by their slope signature (positiv / negativ - segments with slope < 0.2 and slope > -0.2 are ignored)
Than I calculated the average slope and the average intercept of the two sets of linesegments.
Now it is possiple to calculate the start and end points of the two extrapolated lines.
y1 is the bottom of the image.
y2 is the smallest y coordinate of the mask. 

Example result: 

[//]: # (Image References)

[image1]: ./resultimages/solidWhiteCurve.jpg_first_result.png "Firstresult SolidWhiteCurve"
[image2]: ./resultimages/solidWhiteCurve.jpg_result.png "Endresult SolidWhiteCurve"

[image3]: ./resultimages/solidWhiteRight.jpg_first_result.png "Firstresult SolidWhiteRight"
[image4]: ./resultimages/solidWhiteRight.jpg_result.png "Endresult SolidWhiteCurve"

[image5]: ./resultimages/solidYellowCurve.jpg_first_result.png "Firstresult SolidYellowCurve"
[image6]: ./resultimages/solidYellowCurve.jpg_result.png "Endresult SolidYellowCurve"

[image7]: ./resultimages/solidYellowCurve2.jpg_first_result.png "Firstresult SolidYellowCurve2"
[image8]: ./resultimages/solidYellowCurve2.jpg_result.png "Endresult SolidYellowCurve2"

[image9]: ./resultimages/solidYellowLeft.jpg_first_result.png "Firstresult SolidYellowLeft"
[image10]: ./resultimages/solidYellowLeft.jpg_result.png "Endresult SolidYellowLeft"

[image11]: ./resultimages/whiteCarLaneSwitch.jpg_first_result.png "Firstresult WhiteCarLaneSwitch"
[image12]: ./resultimages/whiteCarLaneSwitch.jpg_result.png "Endresult WhiteCarLaneSwitch"

(more pictures in the resultimages floder)

First Result | End Result
------------ | -------------
![alt text][image1] | ![alt text][image2]
![alt text][image3] | ![alt text][image4]
![alt text][image5] | ![alt text][image6]
![alt text][image7] | ![alt text][image8]
![alt text][image9] | ![alt text][image10]
![alt text][image11] | ![alt text][image12]


### 2. Identify potential shortcomings with your current pipeline

* The pipline produces a bit nervous lines (see video). One reason is the way of creating these two lines. All segments do have the same influence. Long segments the same than short segments.
* The result of the optional film ist not verry good. There are to many "wrong" results after the houghtransformation.
* The mask is not optimal. There are many short inexact segments from the top of the image in the result.  

### 3. Suggest possible improvements to your pipeline

* The calculations to create the two lines should weight the segments. Long segments should have a stronger influance. A linear regression on the endpoints of the segments should have a better result. 
* The filtering should be improved. Segments with too big or to small slope should be ignored. 
* Setup a better mask.
* Use a bigger min_line_len for the hough transformation
* Split the picture based on the colorchanel. So it is possible to find edges in a color contrast system or ignore them. 
 

