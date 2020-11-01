+++
title = "Unity Lab"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

In this Topic I will present you my Unity game named Floor is Lava 2k20. The game is separated in 4 rooms. 

# Here is the first one : 
![image info](/unity1.PNG)

This room is like a tutorial since it makes you understand that you need all collectibles in a room in order to remove the wall that is blocking you the access and that if you fall on the lava you respawn at the beginning of the zone. 

Here is the script that unable the wall (in blue on the last picture) : 
```js
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class disableWall : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        gameObject.GetComponent<Renderer>().enabled = true;
        gameObject.GetComponent<BoxCollider>().isTrigger = false;
    }

    // Update is called once per frame
    void Update()
    {
        if (FindObjectOfType<PlateformerSceneManager>().firstWallUnable())
        {
            gameObject.GetComponent<Renderer>().enabled = false;
            gameObject.GetComponent<BoxCollider>().isTrigger = true;
            
        }
        
    }
}

```

# Second room : 


![image info](/unity3.PNG)
In this room you still must collect all the collectibles to pass the wall but here there are some moving platforms. In order to make the player moving with the platform I made a script that make the platform parent of the player when it triggers it.

Here is the script : 
```js
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class addConstantVelocity : MonoBehaviour
{
  


    public GameObject Player;

    private void OnTriggerEnter(Collider other)
    {

        if (other.gameObject == Player)
        {
            other.transform.SetParent(this.transform);
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.gameObject == Player)
        {
            other.transform.SetParent(null);
            

        }
    }
}
```

# Third room :

![image info](/unity5.PNG)
Here I created a little puzzle, in fact when you climb up the first block you see that some of the next boxes become green or red. Then, when you leave this block the green and red boxes become black again and so you have to remember the pattern to pass the zone as the colliders of red boxes are Trigger.

Here is the script of the color reveal : 
```js
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class revealBlock : MonoBehaviour
{
	private GameObject[] Green;
	private GameObject[] Red;
	[SerializeField]
	private Material inMaterial1;
	[SerializeField]
	private Material inMaterial2;
	[SerializeField]
	private Material outMaterial;
	[SerializeField]
	private GameObject player;
	
	void Start()
	{

		Green = GameObject.FindGameObjectsWithTag("vert");
		Red = GameObject.FindGameObjectsWithTag("rouge");
	}

	private void OnTriggerEnter(Collider other)
	{
		if (other.name == player.name)
		{
			foreach(GameObject i in Green)
            {
				i.GetComponent<Renderer>().material = inMaterial1;

			}

			foreach (GameObject j in Red)
			{
				j.GetComponent<Renderer>().material = inMaterial2;

			}

		}


	}
	private void OnTriggerExit(Collider other)
	{
		if (other.name == player.name)
		{

			foreach (GameObject i in Green)
			{
				i.GetComponent<Renderer>().material = outMaterial;

			}

			foreach (GameObject j in Red)
			{
				j.GetComponent<Renderer>().material = outMaterial;

			}
		}



	}
}

```

# Fourth room : 

![image info](/unity6.PNG)
On this room, the gameplay is quite easy : if you touch one of the red wall you die and you respawn.

Here is the script :

```js
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class wallRespawn : MonoBehaviour
{
    // Start is called before the first frame update

    void OnTriggerEnter(Collider other)
    {

        if (other.gameObject.tag == "player")
        {
            FindObjectOfType<DeathWall>().reposition();
        }
    }
}

```

# Additional gameplay features : 

I added a collectible counter and a timer that displayed the number of collectibles you have and how long it takes you to complete the level. 

Here are the respective scripts : 
```js
public void Collect()
    {
        collectibleCounter++;
        Counter.text = "Collectible :" + collectibleCounter.ToString() +" / " + collectibleGoal.ToString();
        if (collectibleCounter >= collectibleGoal)
        {
            Counter.text = "Collectibles = max";
            Counter.color = Color.green;
        }

        


    }

```

```js
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class Timer : MonoBehaviour

   
{
    public float temps = 0;
    public Text timertext;
    //public int tempsInt;
    public int minute;
    public int seconde;
    public EndZone Endzone;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        //tempsInt = Mathf.RoundToInt(temps);
        minute = Mathf.FloorToInt(temps / 60);
        seconde = Mathf.FloorToInt(temps % 60);

        timertext.text = (minute + " : " + seconde);
        if(Endzone.gameFinished == false)
        {  
            temps += Time.deltaTime;

        }
    }
}


```

There is also a script that change the respawn location each time you enter a room :
```js

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class newRespawn1 : MonoBehaviour   
{
    [SerializeField]
    GameObject newCubeRes = default;
    public DeathWall DeathWall;
    // Start is called before the first frame update
    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "player")
        {
           DeathWall.cubeRes = newCubeRes;
        }
    }
}

```

So now you know the theorical part, there is a video of the gameplay : 

{{< youtube iQjg5uu649A >}}
