+++
title = "Lab 3"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

This new lab is still about the roll a ball game but this time we no longer use our phone to control the game board, this time we will be able to grab it with our hands thanks to VR. It was the most difficult labs of the 3, firstly, we had to import an oculus package to enable VR. Note that I used an oculus quest so I had to build the game like an android game.
![image info](/MyBlog/lab3-2.PNG)
When we imported the roll a ball package in the VRTK project we had to create an empty object that will parent the game and add a box collider to it (in order to grab it).
![image info](/MyBlog/lab3-3.PNG)
We also had to remove all the part of the controller script related to the movement of the ball and we also had to remove the physic relation between the VR grab object and the roll a ball game because we don’t want the physics of the board to affect the physic of the ball (no bouncing) we also had to remove the tilting ground script.

After that we had to think that it’s a VR game so we built a table to rise the game board up.
![image info](/MyBlog/lab3-1.PNG)
 Also when we launch the game we spawn at the center of the scene so we had to move objects (table and board game) and reduce their size however the game board would be huge. For instance here, before moving objects I spawn inside the table.
![image info](/MyBlog/lab3-5.PNG)
![image info](/MyBlog/lab3-3.PNG)
And so after doing the manipulations I can play the game, the only issue is that, as you can see on the video, there is an y offset when I grab the game board so I have to put my hands lower to see the ball and the collectibles.
{{< youtube hqTp8mMuOyc >}}

You can find my scripts on my Github : https://github.com/GuillaumeG9153/Lab3_Roll-a-ball-VR