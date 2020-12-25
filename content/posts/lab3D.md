+++
title = "lab: 3D reconstruction"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

The goal of this lab was to implement a 3D reconstruction from multi-views of human pose.
We had to reconstruct the 3D skeleton of a person from the matching joints of multi-views.
To do so we had data: videos of subjects doing different movements
OP2DTXT, containing text files of 25 joints on each sequences of each subject, this is the format of every line

![image info](/MyBlog/khoa1.jpg)

 X and y are horizontal and vertical pxiels and r is the reliability score

			OP3DTXT, containing text files of the coordinates output of first 15 joints after 
triangulation from multiviews of 2D joints

![image info](/MyBlog/khoa2.jpg)

**Task 1: **Our first task consisted of drawing points stored on 2DTXT on the original video

```js
import numpy as np
import cv2


# read

fichier = open("data/OP2DTXT/Lea/burpees_1_0.0.txt", "r")
lines = fichier.readlines()
tab = []
for line in lines:
    points = []
    z = line.split(" ")
    for i in range(0, len(z) - 1, 3):
        x = float(z[i])
        y = float(z[i + 1])
        points.append([x, y])
    tab.append(points)
fichier.close()

#draw
cap = cv2.VideoCapture('data/Videos/Lea/burpees_1_0.0.avi')
frame_width = int(cap.get(3))
frame_height = int(cap.get(4))
size = (frame_width, frame_height)
result = cv2.VideoWriter('result/output.avi', cv2.VideoWriter_fourcc(*'MJPG'), 60, size)
i = 0
while (True):
    ret, frame = cap.read()
    if ret == True:
        for points in tab[i]:
            image = cv2.circle(frame, (int(points[0]), int(points[1])), radius=3, color=(0, 0, 255), thickness=-1)
        cv2.imshow('Frame', image)
        result.write(frame)
        i += 1
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
    else:
        break

cap.release()
result.release()

cv2.destroyAllWindows()

```
First of all we read the file and extract all of the points, then we open the video file and thanks to the openCV library we draw the points we just read.

![image info](/MyBlog/khoa3.jpg)

![image info](/MyBlog/khoa4.jpg)


**Task 2:** Now we do the same with the 3DTXT file, in this task we had to project these coordinates on the frame of different camera frame.

In this task the main issue was to determine the shifting matrix to shift the origin from view 0 to 1 and from 1 to 2

![image info](/MyBlog/khoa5.jpg)

![image info](/MyBlog/khoa6.jpg)

After that we load the 2D pose on view 2, the 3D pose after triangulation and finally we load the video capture on view 2

![image info](/MyBlog/khoa7.jpg)

Then we can project on view 2:

![image info](/MyBlog/khoa8.jpg)

We draw as the same way we did on task 1.

This is the full code:

```js
import numpy as np
import cv2
import os
import sys
from tools2D3D import DB2D3DManager


def originShift(point,P):
    point = np.append(point, np.array([1]))
    point = np.dot(P,point)
    return point

dbMan = DB2D3DManager("./data")
subject ="Lea"
action ="soulevedeterre_1_0"
nbJ = 15 #Number of joints after triangulation
P01 = dbMan.loadExtrinsic(0) #origin shift matrix from 0 to 1
P12 = dbMan.loadExtrinsic(1) #origin shift matrix from 1 to 2
lst_f,lst_c  = dbMan.loadIntrinsic() #Loading intrinsic parameter of all cameras
pose2Dv2 = dbMan.load2DTXT(subject,action,2) #Load the 2D pose on view 2
pose3Dv0 = dbMan.load3DTXT(subject,action) #Load the 3D pose after triangulation, reference at view 0
cap = dbMan.loadVideoCapture(subject,action,2) #Load the video capture object on view 2
if cap==None:
    exit()
nF = int(cap.get(cv2.CAP_PROP_FRAME_COUNT)) 
vidWriter = cv2.VideoWriter("demo2.avi",cv2.VideoWriter_fourcc('M','J','P','G'), 30, (640,480)) #VideoWriter for output
assert(pose2Dv2.shape[0]==pose3Dv0.shape[0])
#assert(nF == pose2Dv2.shape[0])
step = 255.0/(nbJ-1) 

for i in range(351):
    sys.stdout.write('\r')
    sys.stdout.write("{}/{}".format(i,nF))
    cap.set(cv2.CAP_PROP_POS_FRAMES,i)
    ret, frame = cap.read() # Retrieve frame from video capture
    if (not ret):
        exit()
    for j in range(nbJ):
        #Retrieve the X,Y from OpenPose
        X = int(pose2Dv2[i,3*j+0]) 
        Y = int(pose2Dv2[i,3*j+1])

        pos3Dv0 = pose3Dv0[i,4*j+1:4*j+4] #Retrieve the 3D point at view 0 
        pos3Dv1 = originShift(pos3Dv0,P01) #Shifting origin from view 0 to view 1 of 3D point 
        pos3Dv2 = originShift(pos3Dv1,P12) #Shifting origin from view 1 to view 2 of 3D point 
        #Note : you can make a direct shifting matrix from 0 to 2 by transforming 
        #the 3x4 shifting matrix P01,P12 into homogenous matrix 4x4 by adding row at the bottom [0 0 0 1]
        #Then the P02homo = P12homo*P01homo
        pos3Dv2 =pos3Dv2[:2]/pos3Dv2[2] #Normalize 3D coordinate
        pos2Dx = lst_f[2]*pos3Dv2 + lst_c[2] #Project into 2D point on view2, using the intrinsic of cam 2

        cv2.circle(frame,(X,Y),8,(255,255-j*step,j*step),-1) #Draw the points of OpenPose by big color circle
        cv2.circle(frame,tuple(pos2Dx.astype('int')),4,(0,0,255),-1) #Draw the projected point after origin shifting with smaller red circle
        
    vidWriter.write(frame)
print("")
cap.release() 
vidWriter.release() 
```
