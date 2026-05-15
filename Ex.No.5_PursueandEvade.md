# Ex.No: 5  Implementation of Steering behaviour-Pursue and Evade in Unity
### DATE:    15-05-2026                                                                        
### REGISTER NUMBER : 212223240115
### AIM: 
To write a program to simulate the process of Pursue and Evade behavior in Unity using NavigationMeshAgent. 
### Algorithm:

1.Create a New Unity Project by Open the Unity Hub and create a new 3D Project.

2.Name the project "SteeringBehaviors" and select a location. Click Create.

3.Open Unity Scene (default is SampleScene). In the Hierarchy, create a Plane: Right-click → 3D Object → Plane (this will be the ground). Set its Scale to (10, 1, 10) for a larger surface. Create three Capsule
for the Player, Pursuer, and Evader: Rename them to "Player", "Pursuer", and "Evader". Set their Y Position to 0.5 (so they sit on the ground). Change their Material for better distinction (optional).

4.Add NavMesh and Bake Window → AI → Navigation (opens the Navigation tab). Select the Plane, go to the Navigation tab, and mark it as Navigation Static. Go to the Bake tab and click Bake. or Add navMeshSurface to plane and bake

5.Add NavMeshAgent Component Select Pursuer, and Evader. Click Add Component → Search for NavMeshAgent and add it. Adjust NavMeshAgent Settings speed. 

6.Write a script for Player_movement behavior and save it

7.Write script for Pursuer and Evader.

8.Attach the Script to each player,pursuer and Evader. Drag & Drop the Target from the Hierarchy into the "Target" field in the script component ( For pursuer and Evader).

9.Run the game

## Player:
```

using UnityEngine;

public class player : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    public float speed;
    void Start()
    {
        float xdir = Input.GetAxis("Horizontal") * speed;
        float zdir = Input.GetAxis("Vertical") * speed;
        transform.position=new Vector3(xdir,zdir);
        
    }

    // Update is called once per frame
    void Update()
    {

        
    }
}
```
## Pursuer:
```

using UnityEngine;

public class pursuer : MonoBehaviour
{
    public UnityEngine.AI.NavMeshAgent agent;
    public Transform target;
    public float speed = 5f;

    void Start()
    {
        agent = GetComponent<UnityEngine.AI.NavMeshAgent>();

        target = GameObject.Find("player").transform;
    }

    void pursue()
    {
        Vector3 targetvelocity = target.position - transform.position;

        Vector3 futurepos =
            target.position +
            targetvelocity.normalized * speed;

        agent.SetDestination(futurepos);
    }

    void Update()
    {
        pursue();
    }
}
```

## Evader:
```

using UnityEngine;

public class evader : MonoBehaviour
{
    // Start is called before the first frame update
    public UnityEngine.AI.NavMeshAgent agent;
    public Transform target;
    public float evadespeed;
    void Start()
    {
        agent= GetComponent<UnityEngine.AI.NavMeshAgent>();
    }

    void evade()
    {
        Vector3 fleedir = transform.position - target.position;
        Vector3 evadeposition = transform.position + fleedir.normalized * evadespeed;
        agent.SetDestination(evadeposition);

    }
    // Update is called once per frame
    void Update()
    {
        evade();          
     }
}
```

### Output:

<img width="1918" height="1107" alt="image" src="https://github.com/user-attachments/assets/e7179f63-4520-48dd-bfbd-3b676d7a334d" />

<img width="1912" height="1110" alt="image" src="https://github.com/user-attachments/assets/7f2fb1b5-131d-4ffc-b04e-f1b8f794a778" />

### Result:
Thus the simple pursue and evade behavior was implemented successfully.
