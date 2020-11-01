+++
title = "Lab 2"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

This second lab is about the same game than the previous one but it’s a different way to play it since we built it for android devices.
![image info](/MyBlog/lab2-1.PNG)
So the new gameplay is the following one : we no longer control  the ball it’s the gyroscope of our phone that controll the board game (wall and ground). This is you your ground need to parent all of our game objects to the ground like this.
![image info](/MyBlog/lab2-2.PNG)
For instance I forgot to make a wall child of the ground and when I pushed the game on my phone the wall was rotated by 90 degrees.

My major problem was that my phone was avilable on the run devices on the build settings window (check the first picture) but I couldn’t push my game. I searched for a long time, firstly I thought it was a problem with the keys but they were good. 

After several minutes I found the problem cam from my phone. In fact I had to check several options and not only enable debugg mode. I had to check the options “Installer via USB” and “Débogage USB (Paramètres de sécurité)” if someone has a xiaomi phone like me and you have the same problem I think this is your solution.

![image info](/MyBlog/lab2-1i.PNG)
So then I was able to build my game but…

{{< youtube f-qOpaXH5q0 >}}
{{< youtube SYHuJGs9zVw >}}
As you can see sometimes I can play and sometimes my ball disappear threw the ground.
In fact your ball can fall if you turn your phone face down since we control the orientation of the board but here my phone is face up so I don’t know what is the problem.
![image info](/MyBlog/lab2fin.jpg)

You can find my scripts on my Github : https://github.com/GuillaumeG9153/Lab2_Roll-a-ball-mobile