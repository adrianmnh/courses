# cv class 5

Binary image noise suppresion /object extraction via Mathematical morphology

## Morphology


# Computer Vision class 7
September 15

## Run Length Encoding Part II

Run-length encoding method 1 is used for Fax Machines

Run-Length encoding method 1 Algorithm

```
Step 0:     inFile <- open input image file
            numRows, numCols, minVal, maxVal <- inFile
            row <- 0
            length <0 0
            
Step 1:     col <- 0
            length <- 0
            currVal <- inFile
            
Step 2:     output <- row, col, currVal
            length++
            
Step 3:     col++
            
Step 4:     nextVal <- infile
            
Step 5:     if nextVal == currVal
                length++
            else
                output <- length
                length <- 1
                currVal <- nextVal
                output <- row, col, currVal
                
Step 6:     repeat steap 3 to step 5 until END OF TEXT LINE
            
Step 7:     row++
            
Step 8:     repeat Step 1 to step 7 until end of file
            
Step 9:     close all files
```

> Quiz example

Exam :
* Deepest Concavity

Why is framing necesssary? 

It helps reducing the amount of computation by reducing the amount of cases we test for. Corners(4), Edge pixel(4), nont edge or corner(1 case)

> Counting Algorithm

### Connected Neighbor
> Connected neighbor

> connected component algorithm Image 
- A simple grouping(clustering) algorithm
- WOrks on binary images
- Assign unique labels to connected sets of objects pixels
- Compute a list of attributes for each component

```
    110011110
    011011000
    001111001    -> zero frame
    110000101
    001111100

    00000000000
    01100111100
    00110110000
    00011110010
    01100001010
    00011111000
    00000000000
```

```
image <- given the BInary image
newLabel <- 0 (background is 0)
eqTable <- Equivalency Table

scan the image Left -> Right and Top->Bottom
P(i,j) <- next pixel

if P(i,j) > 0
    look at: a,b,c,d

    4 connectedness

    ___| a |____
     b |(i,j)|____
    
    8-connectedness                
    a | b | c
    d | P(i,j) | 

Which connectedness should you apply? meaning 4 or 8 conntectedness?

case 1: a= =b =c =d =0
        newLabel++
        P(i,j) <- newLabel

case 2: some/all of a,b,c,d alread have the same label 
        P(i,j) <- same label

case 3: some/all of a,b,c,d already have labels but their label are NOT the same(excluding 0)
        P(i,j) <- minLabel = min(a,b,c,d)


```

> cases