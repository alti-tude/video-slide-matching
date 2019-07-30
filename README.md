# video-slide-matching

### Image Contrast Enhancement using CLAHE(Contrast Limited Adaptive Histogram Equalisation) on LAB color space
One important aspect of the frames from the videos is the fact that they are usually shot with cameras with low dynamic range or low quality, such that colors become faded and much contrast is lost. This fact led us to use CLAHE technique on the LAB color space to enhance our contrast. The method is useful in images with backgrounds and foregrounds that are both bright or both dark. Like in the latest episode of GOT people were complaining of the darkness (low light) of episode which resulted in very less visible detail. So this technique can help increase contrast and hence detail but there is a drawback it may increase the contrast of background noise, while decreasing the usable signal.

***So how is this helping in our task?***

There were some slides where there was some handwritten diagrams which were of very low contrast meaning color of the text/drawing was very similar to the white background of slides so in that cases normal cross correlation was giving wrong answers so we applied
this and the results got better in such cases 
1. Decompose our image into the L*A*B* color space, where L is the intensity. Since we are working in greyscale, enhancing only L suits our case.
2. Run CLAHE on the L plane.
  a. Clahe uses small windows(8x8 in our case) that it runs over the entire image.
  b. It draws a histogram of the values and then equalises the histogram. Since it is done in local regions, the local contrasts are enhanced. This is what we are interested in.
3. Combine and convert to grayscale.  

### Kernel Filtering

To further sharpen our image features we use kernel filter, so that the edges of text and other things are further enhanced. This is done to because in the actual slides, the text etc, have very sharp outlines.

<p align=center> 
[-1, -1, -1]<br>   
[-1, 9, -1]<br>    
[-1, -1, -1]<br>    
</p>

### Normalised Cross Correlation

We used normalised cross correlation on the all the slides for each of the frames. The slide with the ma value per frame is the required best matching slide.
