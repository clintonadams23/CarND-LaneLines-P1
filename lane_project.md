#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./images/masking.jpg "Masked region"

---

### Reflection

    My pipeline consisted of 5 steps. The first step was to convert the image to grayscale. Once that was done, I applied gaussian filtering with a kernal size of 3 to reduce noise in the grayscale image. Canny edge detection was then applied to the image to identify boundaries. After generating an image with boundaries identified, everything except for the region corresponding to typical lane locations was masked. 
The following image shows the masked region:
![alt text][image1]
    Finally, the masked image was put through a Hough transformation function to generate a series of lines that are likely to be lane markers.  

    In order to merge these lines into two final lines, each representing the left and right lane boundaries, I modified the draw_lines function. First, I divided the lines into lists of left and right lines according to their slopes. Then, I used maximum and minimum values to find the extent of the lines and create a single pair of lines. Then, I used the slope to extrapolate the x value for each line when the y value is at the bottom of the image.  
 
    The image detection system relies on the lanes being relatively straight lines. It would likely fail on very long curves in roads. 
Another shortcoming could be that it relies on a specific orientation of the camera. On inclines it is possible that the lines would be outside of the masked region.

    The pipeline is vulnerable to noise. One potential improvement would be to use color to further reject lines that are not lane markings.Another potential improvement would be to use a moving average of the slope in order to reduce jitter in the lane markers.