+++
title = "Lab 1"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

This game project was easy to follow since we already had labs on Unity before in order to build our proper game. First of all, building the objects that compose the game was the first task and as I said it was a quick task and this is how I did it.

So the scene is composed by a ground and 4 walls (I created an empty game object that parented them), on this board game I added a ball that will be our player and cubes that will be our collectibles.
You can also see texts, notice that at the difference of our last Unity project we use TextMeshPro instead of Text but we used them as the same.

{{< figure src="/lab1-1.PNG" title="Proposed solving solution" >}}

Then we added a Camera Controller script that will permit the camera to follow the ball during the game. The most important script is probably the player controller one which allow a speed to the ball and that also carry the collectible counter function.

![image info](/docs/lab1-2.PNG)
![image info](/lab1-3.PNG)
This last part of the script was really helpful to me to build my other game since I discovered here the notion of Tag (as you can see here you compare the object that trigger the player thanks to his tag, here “pickups”)

![image info](/lab1-4.PNG)
![image info](/lab1-5.PNG)
I also learnt how to make a collectible counter and display it on the game.
So enjoy my game and my IPP flavor material

{{< youtube RwA4n383KIw >}}

You can find my scripts on my Github : https://github.com/GuillaumeG9153/Lab1_roll-a-ball
