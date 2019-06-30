# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on the process of finding lane lines by computer vision technics

---
[//]: # (Image References)

[image1]: ./examples/line-segments-example.jpg "HoughLines"

### Reflection

### 1. Pipe line of finding lane lines on single image

a. Turn the original image into a grayscale image.
b. Apply gaussian smoothing and use Canny Edge Detection to extract edges from the image.
c. Create a mask of region of interest to filter and save all pixels inside of the region. 
d. Apply Hough Transform to indentify straight lines that form lane lines
e. Draw straight lines to represent lane lines by the line information produced in (d.) .

### 2. Draw Lane Lines

In this project, each lane line are drawn as a signle straight line as the lanes are straight forward in all videos.
Thus, the **polyfit** function in Numpy is employed to drawn lines.
The pipe line of drawing the lane lines from Hough Transformation is as the following:

1. Sort all line segments samples into left/right lane by their slopes(<0 for left line, else for right line).
2. Filter and delete line segments that have abnormal slope.
3. Use **polyfit** function to calculate the line functions which y coordinate is the variable.
4. Draw lines from the bottom to top of the region of interest

#### 2.1 Filter abnormal segments
Lines segments from Hough Transformation often have ones with abonormal slopes (such as the horizontal segment in this picture).
![alt text][image1]
Thus, abnormal lines are filtered out by a slope threshhold and (y2 - y1) threshhold. 

### 3. Potential shortcomings

#### 3.1 Robustness
The major shortcoming of this program is its robustness. It only works well when no large objects in front of the car and the road is straight. In the challenge video, even if the region of interest is tuned to match exactly the lane lines, the shaodow of trees can still produce noisy data.

#### 3.2 Dotted lane lines
In addition, during tuning the program, the program had a hard time to identify dotted lane lines while avoid noisy data. Thus, this program may have trouble identifying dotted lane lines.

### 3. Possible improvements 

To improve robustness, multiples masked regions may be utilized to detect lane lines and the program should be able adjust the identification parameters.
Such as in the videos with dotted lane lines, two masked regions should be created to identify left and right lines seperately. In addition, as dotted lane lines is hard to detect, the program may need to refine its parameters to avoid missing lane line or producing too much noisy data.