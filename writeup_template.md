# **Finding Lane Lines on the Road** 


### Reflection

### 1.Pipeline

My pipeline consisted of following steps:
1. convert input to grayscale
2. smooth noice with gaussian with kernel=3
3. find edges by canny detector
4. cut region of interest
5. find lines using hough_lines

hough_lines is modified to drop lines with incorrect slope.

All parametes are tuned by hands.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by
1. split all input lines to left and right groups
2. for each group
    1. filter outliers by mean/std statistic
    2. compute average slope/intercept
    3. comput two poins with y = 540, 320
    4. draw single line

### 2. Potential shortcomings

- It is possible that no lines will be found
- Sometimes extra lines at road will be found (not lane lines, just defects on asphalt)
- The geometry of camera is not linear, as a result straight lines are not straight
- Parameters are not optimal

### 3. Possible improvements to the pipeline

- If line is not found we can make parameters more weak and repeat search
- If we found one line (e.g. left) we can use information about this to find another one (right)
- We can make parameters more weak and use statistical filtering in hough_lines
- We can fix camera geometry
- We can tune parameters (but we need train/test sets on images with lines annotation)

PS. Sorry for my english :)