---
layout: post
title: Counting stars
---

People have since the beginning of time been curious towards stars. In current age we can identify the constituent elements of sky objects with the help of sectroscopy. This article presents solution to much simpler problem which is to count the number of stars in a given night sky photograph.

While manually counting stars in the night sky, we are never sure if what we are seeing is actually a star. Also with the time of gazing more stars seem to appear and dissapear. While in a photograph taken with the help of configurable exposure cameras we can not only find more stars but also see many faint stars along with the bright ones with more surety. There are different types of photographs which cause different problems for counting stars.
For the experiment sample images are taken from the internet with preference to high resolution pictures.

Let's start with the results. Following is a picture form hubble deep field and the most of the objects in the picture are galaxies.

<img style="float: left;" src="/assets/img/Galaxies-Hubble-Ultra-Deep-Field-Partial.JPG" width="600">

photo credits: unknown

The result picture is contains the identified objects with a green circle around them. The total number of objects turn out to be 2632.

<img style="float: left;" src="/assets/img/result-2632.jpg" width="600">

But this is mostly little bigger objects and not like very tiny dots. I wanted to count the number of stars in a picture something like the below photograph. This picture contains my favourite constellation orion.

<img style="float: left;" src="/assets/img/test3.jpg" width="600">
photo credits: unknown

The resultant picture contains 495 stars, but this doesn't count faint stars. We will capture them in the next photograph.

<img style="float: left;" src="/assets/img/result-495.jpg" width="600">

The next example was to find the number of stars in those pictures which also have bewildering star dust or glow or clouds in the background. Also I wanted to count the faintest of the stars in the photograph. Here's an example.

<img style="float: left;" src="/assets/img/test7.jpg" width="600">
photo credits: unknown

For the final example there turned out to be 4383 stars.

<img style="float: left;" src="/assets/img/result7(3)-4383.jpg" width="600">

__Approach__

This is problem of blob detection in an image. Blobs are bright on dark or dark on bright regions in an image. Blob detection methods are aimed at detecting regions in a digital image that differ in properties, such as brightness or color, compared to surrounding regions. Informally, a blob is a region of an image in which some properties are constant or approximately constant; all the points in a blob can be considered in some sense to be similar to each other. The most common method for blob detection is convolution. 

Given some property of interest expressed as a function of position on the image, there are two main classes of blob detectors: (i) differential methods, which are based on derivatives of the function with respect to position, and (ii) methods based on local extrema, which are based on finding the local maxima and minima of the function. With the more recent terminology used in the field, these detectors can also be referred to as interest point operators, or alternatively interest region operators.

I have made use of laplacian of guassian and difference of gaussian. Difference of gaussian being faster. both the algorithms are slow when we try to detect larger blobs. Both of them belong to first type of blob detectors.

The Laplacian is a 2-D isotropic measure of the 2nd spatial derivative of an image. The Laplacian of an image highlights regions of rapid intensity change and is therefore often used for edge detection (see zero crossing edge detectors). The Laplacian is often applied to an image that has first been smoothed with something approximating a Gaussian smoothing filter in order to reduce its sensitivity to noise. The operator normally takes a single graylevel image as input and produces another graylevel image as output.

Difference of Gaussians is a feature enhancement algorithm that involves the subtraction of one blurred version of an original image from another, less blurred version of the original. In the simple case of grayscale images, the blurred images are obtained by convolving the original grayscale images with Gaussian kernels having differing standard deviations. 

Blurring an image using a Gaussian kernel suppresses only high-frequency spatial information. Subtracting one image from the other preserves spatial information that lies between the range of frequencies that are preserved in the two blurred images. Thus, the difference of Gaussians is a band-pass filter that discards all but a handful of spatial frequencies that are present in the original grayscale image

As a feature enhancement algorithm, the difference of Gaussians can be utilized to increase the visibility of edges and other detail present in a digital image. A wide variety of alternative edge sharpening filters operate by enhancing high frequency detail, but because random noise also has a high spatial frequency, many of these sharpening filters tend to enhance noise, which can be an undesirable artifact. The difference of Gaussians algorithm removes high frequency detail that often includes random noise, rendering this approach one of the most suitable for processing images with a high degree of noise. A major drawback to application of the algorithm is an inherent reduction in overall image contrast produced by the operation
But to plot the detected stars I have plotted them against the original image hence while comparing they look same.

In its operation, the difference of Gaussians algorithm is believed to mimic how neural processing in the retina of the eye extracts details from images destined for transmission to the brain. This is interesting.

Besides minor technicalities, difference of Gaussians (DoG) is in essence similar to the Laplacian and can be seen as an approximation of the Laplacian operator. In a similar fashion as for the Laplacian blob detector, blobs can be detected from scale-space extrema of differences of Gaussians—see (Lindeberg 2012, 2015) for the explicit relation between the difference-of-Gaussian operator and the scale-normalized Laplacian operator. This approach is for instance used in the scale-invariant feature transform (SIFT) algorithm.

A natural approach to detect blobs is to associate a bright (dark) blob with each local maximum (minimum) in the intensity landscape. A main problem with such an approach, however, is that local extrema are very sensitive to noise. To address this problem, Lindeberg (1993, 1994) studied the problem of detecting local maxima with extent at multiple scales in scale space. A region with spatial extent defined from a watershed analogy was associated with each local maximum, as well a local contrast defined from a so-called delimiting saddle point. A local extremum with extent defined in this way was referred to as a grey-level blob.

Another approach Determinant of Hessian (DOH) wasn't tried because reportedly small blobs(<3px) are not detected accurately.

The full script can be found at  ([here](https://github.com/unosonu/miscelleneous-scripts/blob/master/count-stars.py)) 

__References__

http://micro.magnet.fsu.edu/primer/java/digitalimaging/processing/diffgaussians/index.html
https://en.wikipedia.org/wiki/Difference_of_Gaussians#Details_and_applications
https://en.wikipedia.org/wiki/Marr%E2%80%93Hildreth_algorithm
https://en.wikipedia.org/wiki/Spatial_frequency
http://scikit-image.org/docs/dev/auto_examples/features_detection/plot_blob.html
http://fourier.eng.hmc.edu/e161/lectures/gradient/node8.html
https://homepages.inf.ed.ac.uk/rbf/HIPR2/log.htm
