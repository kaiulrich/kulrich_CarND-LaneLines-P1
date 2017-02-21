#**Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

###1. Describe your pipeline.

My pipeline consisted of 7 steps.
 
* Converted the images to grayscale. 
* Gaussian smoothing to reduce image noise and reduce detail. I used a a kernel size of 5. has enough less blurring and keeps enough struktur.
* Process of Canny edge detection. 
* Masking the Region of Interest.
* Extract linesegments via hough transformation
* draw the lines
* merge the original and line picture


In order to draw a single line on the left and right lanes, I modified the draw_lines() function.
First I sorted the linesegments by their signature (positiv / negativ) slope. (segments with slope < 0.2 and slope > -0.2 are ignored)
Than I calculated the average slope and the average intercept of the two sets of linesegments.
Now it is possiple to calculate the start and end points of the two extrapolated lines.
y1 is the bottom of the image.
y2 is the smaller y coordinate of the mask. 

Example result: 

[//]: # (Image References)

[image1]: ./resultimages/solidWhiteCurve.jpg_first_result.png "first SolidWhiteCurve"
[image1]: ./resultimages/solidWhiteCurve.jpg_result.png "Endresult SolidWhiteCurve"

(more pictures in the resultimages floder)

###2. Identify potential shortcomings with your current pipeline

* The pipline produces a bit nervous lines. The reason is the way of creating the two lines. All segments do have the same influence. Long segments the same than short segments.
* The result of the optional film ist not verry good. There are to many "wrong" results after the houghtransformation.
* The mask is not optimal so the are many short inexact segments from the top of the image in the result.  


###3. Suggest possible improvements to your pipeline

* The calculations to create the two lines should weight the segments. Long segments should have a stronger influance. A linear regression on the endpoints of the segments should have a better result. 
* The filtering should be improved. Segments whitch have a too big or to small slope should be ignored. 
* Setup a better mask.
* Use a bigger min_line_len for the hough transformation
