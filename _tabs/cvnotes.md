# finish project 8/31 for extra point

## Threshholding

size 256 x 256

grey scale: 64 levels (0-63)

histogram: of an image is the statistic counting of pixel values

256 256 0 63

threshold : anything in some range -> new value

Treshold Process

0 if pixel value is <1 , otherwise =1

## Image Enhancing Operations



## Neighbor Operations

[ input images ] --->  ((neighborhood operator)) ----> [output image]

Perform jobs of ( -conditioning, -labeling, -grouping )

Output at a given pixel is a function of 
1. the position of the pixed (r,c)
2. the input pixel value
3. other output values previously generated (recursive neighborhood operation)

## Types of Neighborhood

Most common ones

3x3 matrix              5x5

Other types

1x2        2x1[]      []_       2x2
                        []

In general, nxn matrix
WHere N is an odd number ( so X is in the center)

Neighborhood Operator --  AVERAGING

* Remove noise from the input image
* Also called smoothing

matrix 3x3 [a b c d x f g h i ]  Output for the new x, x' is
x' = (a+b c d x f g h +i)/9


- Averaging falls into the filtering category, since it will get rid of high/low peaks in grey-levels of an image

[greyscale]input image --> (( averaging 3x3 )) ----> smoothing output [greyscale]

## Median Filtering

- A better than the averaging operator for removing noise

Output for the new x, x' is 

x' = median(abcdxfgh,i) is the 5th element of the sorted list of (a,b,c,dxfghi)

Examples 

[90 90 91, 88 12 90, 90 90 90] -----> 12 88 90 90 [90] 90 90 90 91

[10 9 8 10 7, 11 7 9 11 9m 10 9 8 99 7, 12 9 9 10 6, 10 9 8 11 9]    ---> 6 7 8 8 9 [9] 10 11 99

The problem with averaging is that the results become askewed when the highs and the lows are far apart from the median.

The median takes into account the most recurring values in a set of data, hence it makes a smoother output

## Gaussian Filtering

Masking with a aGaussian mask

[1 2 1, 2 4 2, 1 2 1] Gaussian mask, G

[a b c, d x f, g h i] Neighborhood of x

AKA _weighted averaging_

**Output for the new x, x' is**

x' = 1/16*(1*a + 2*b + 1*c + ..... + 1*g + 2*h + 1*i)

_convolution_

16 = total weight

### Common masks: for noise removal

3X3 neighborhood
[1 1 1... ] = 1/9          
[0 1 0 1 2 1 0 1 0] = 1/6  
[0 1 0 1 4 1 0 1 0] = 1/8
[1 1 1 1 8 1 1 1 1] = 1/16
[1 1 1 1 4 1 1 1 1] = 1/12
[1 2 1 2 4 2 1 2 1] = 1/16

5X5 neighborhood
[1 2 3 2 1, 2 4 6 4 2, 3 6 9 6 3...] = 1/81

[0 3 4 3 0, 3 6 7 6 3, 4 7 8 7 4 ....] = 1/100

[1 4 6 4 1 , 4 16 24 16 4, 6 24 36 24 6...] = 1/256

### Some faults on the square-based neighborhood smoothing operators

- When can the averaging operators go wrong?
(THose 3x3 5x5, ... , simple averaging or those Gaussian weighted-averaging operators)

[1 1 1]x3 
[1 2 1, 242, 1 2 1] 
5x5 X in middle

COnsider the following image: empty spaces are 9. the average will be very low, and the median is 0. --->  yields innacurate representation of the images

000000000000000000
000000000000000000
000000 00000000000
00000   0000000000
000      000000000
0000    0000000000
00000  00000000000
000000 00000000000

Why averaging diltering will loose the ..?

THe majority of 3x3 labels are much lower than the actual pixels themselves, and median filtering reduces the total values of the corners themselves even more.


## Smoothing operator the preserves corners and edges

- 25 pixels in the 5X5 neighborhood of x

5x5 with X in middle []
[ ][ ][ ][ ][ ]
[ ][ ][ ][ ][ ]
[ ][ ][X][ ][ ]
[ ][ ][ ][ ][ ]
[ ][ ][ ][ ][ ]

Instead of taking the aberage of the 25 pixels, we group these 25 pixels into 8 groups

G1 - G8 (Regions) **X Always in the MIDDLE**
3x3 square top left, top right, bottom left, bottom right in 5x5 matrix

"triangle" on left , right, top(facing down 9 squares), bottom(facing up)

* Computer the average of each Gi = a1, a2,...,a8
* ~~~Compute the variance of each Gi: v1, v2,..., v8~~~
*  computer the difference of x's grey-level with each of 8 averages: d1, d2, ..., d8
* Assign ai to x if 
    - di is small, and
    - vi is also small 

---

Steps:
1. group x's 5x5 neighborhood into 8 groups G1...G8
2. compute 3X3 average of each group
    - result : a1,a2,....,a8 (average1,2,..)
3. computer absolute difference:
    - abs(ai - X) for each ai
        * result: d1, d2, d3, ..., d8
4. X' <--- the ai, that has the min of (d1, d2, d3, ....,d8)

**This preserves the sharpness of the image**

The idea is the following: 

> by selecting the gruping with the average that is closes to the X in question, we can get a closest approximation to the actual image while smoothing the area  



G1 preserves top left corner????? What kind of corners are preserved with G1-8?


### Framing

In order to perform Smoothing Operations we need to use **Framing**. Means that ewe pad the given image extra number ofrows and cols, This extra number of rows and columns depends on the size of the Kernel that we be using during Smoothing

Zero Framing: where each framed pixel is of value zero
- binary images

 0 0 0 0 0
 0 1 0 1 0 Binary Frame -> Original Binary iamge Framed without 0's
 0 1 1 1 0
 0 1 0 1 0
 0 0 0 0 0 

 Image is 2000X 3000 pixels
 If the neighborhood being used is 3x3
 then we add 2 rows and 2 columns to the sides of the image, and fill with 0s.

 4rows and 4 columsn for 5x5 

Mirror Framing: where each framed pixel has the value of its corresponding mirrored pixel
- greyscale images



 **Mirror Framing** Corner and Edge detection: There are 9 cases here. 

here the frame starts

 1 1 0 2 2 5 5
 1 1 0 2 2 5 5
 4 4 1 3 3 1 1
 4 4 1 3 3 1 1
 4 4 1 3 3 1 1
 9 9 4 1 1 2 2
 9 9 4 1 1 2 2

 Original image is 
1 0 2 2 5
4 1 3 3 1
4 1 3 3 1
4 1 3 3 1
9 4 1 1 2


5X5 Framing

2 0 4 2 3
4 1 1 0 2
0 1 1 0 2 2 5
2 4 4 2 3 3 1
1 4 4 1 3 3 1
    