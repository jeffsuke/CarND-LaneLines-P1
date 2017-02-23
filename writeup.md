#**Finding Lane Lines on the Road**

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Find out lane lines on the road in the images and movies.

This process is summarized in `def findLaneLineWithImage(image):` method below:

```
def findLaneLineWithImage(image):
    gray_image = grayscale(image)
    blur_image = gaussian_blur(gray_image, 5)
    canny_image = canny_(blur_image)
    masked_image = region_of_interest_(canny_image)
    hough_image = hough_image_(masked_image)
    result = weighted_img(hough_image, image)
    return result
```

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I apply Gaussian blur filter. I applied Canny edge detection to the image to find out edges then masked only relevant places on the image. After that, I used Hough Transform to find out Lines and weighted the lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by detecting left and right lane lines by checking the slope. I also filtering out lines with slope less than the threshold, and also adding assumption that lines with negative slope are located in the left side of the image and positive slope in the right side of the image.


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are some white lines on the road except for the lane lines such as numbers and letters. The current system assumes that the drawn lines came from the lane lines and does not handle the situations the system mistakenly detected other objects.

###3. Suggest possible improvements to your pipeline

A possible improvement would be to calibrate the parameters especially around Canny Edge Detection.

Another potential improvement could be to use lane line information form previous images when iterating on videos. By doing so, the lines will be more stable.
