# LESSON #1: Beginner Scripting

https://learn.unity.com/project/beginner-gameplay-scripting 

<h3>#1: Scripts as Behavior Components</h3>
Think of scripts as components that you create to allow you to create behavior for different Game Objects in your game. This could be characters, it could be environments, or it could be scripts that manage the functionality of the game. 

```C#
GetComponent<Renderer>().material.color = Color.red;
```
The <strong>Renderer</strong> in this case refer to the Mesh Renderer in Unity inspector of the specified Game Object.

<h3>#2: Variables and Functions</h3>

Think of the variables as boxes that contain information. You need a different type of boxes for different type of information. 

Functions can also be called as Methods. A function will take the boxes that we have storing information, and give us boxes back, or return as it's known. 

When we make our own functions, we can give them a specific type to return. See ```int MultiplyByTwo(int number)``` below to see how to create a function  

```C#
using UnityEngine;
using System.Collections;

pubic class VariablesAndFunctions : Monobehavior 
{
    int myInt = 5; //int means a whole number
    //declaration (int myInt) = initialization (5) where the actual box gets assigned some information to store  

    void Start() //Start is a function that doesn't return anything and its return type is void.
    {
        myInt = 55;
        Debug.log(myInt);

        myInt = MultiplyByTwo(myInt); //#3 Without the declaration of myint with the new initiation, my int would not have changed. 
        Debug.log(myInt);
    } 

    int MultiplyByTwo(int number)   //#1 Create a function - we would be feeding a number into this function to make it as an input  
    {
        //Create a temporary variable 
        int result;
        result = number * 2;
        return result; //#2 Return the outcome after processing - using return to output the result value from the function 
    }
} 
```
<h3>#3: Conventions and Syntax in Unity</h3>

Coding Syntax simply means the structure of the language, and some conventions are essential to learning to read and write code. 

<strong>The Dot Operator</strong> ```.```
For example, ```Debug.log("Hello")```
<br>
It works like writing the line of an address. Consider Debug as the country, and Log as the city. We are drilling down into things that are within Debug, Log being one of those elements. 

Tips: In Visual Studio, whenever you start a dot operator, it will give you a list of options/elements that the parent element contains.

Here is another example: ```transform.position.x```
<br>
Transform is the country, position is the city, x is the street within the city we are trying to locate 

A compound item being something that contains many elements. Transform contains position, rotation, and scale. In the example above, within Transform, we choose position, and then within position, we choose the x stands for the x position. 

<strong>The Semicolon</strong> ```;```
<br>
The semicolon is used to terminate statements, which is why it is always at the end of a line. 

Anything with curly braces ```{ }``` does not need a semicolon at the end 

<strong>Indenting</strong>
<br>
Indenting is an important part of writing code - it helps the code to look both presentable and easy to read. 

<strong>Comments</strong>
<br>
1. Single line comment 

```//This is a comment!```

2. Multiple line comment 

```C#
/*Hi There!
 *This is two lines!
 * */
```
3. Multiple line comment to disable a certain lines of code:

```C#
/*
if (transform.position.y <= 5f){
    Debug.log("About to hit the ground");
}
*/
```
<h3>#4: IF Statements</h3>
Think of an example below to see when the coffee is ready to drink:


```C#
using UnityEngine;
using System.Collections; 

public class IfStatements : MonoBehavior 
{
    float coffeeTemperature = 85.0f;
    float hotLimitTemperature = 70.0f;
    float coldLimitTemperature = 40.0f;

    void Update() 
    {
        if (Input.GetKeyDown(KeyCode.Space)) //only run the next line of code 
        //ADVICE: highly suggested to use curly braces instead 
            TemperatureTest();
        
        coffeeTemperature -= Time.deltaTime * 5f; 
    }

    void TemperatureTest()
    {
        if (coffeeTemperature > hotLimitTemperature)
        {
            print("Coffee is too hot");
        }
        else if (coffeeTemperature < coldLimitTemperature)
        {
            print("Coffee is too cold");
        }
        else 
        {
            print("Coffee is just right");
        }
    }
}

```

<h3>#5: Loops</h3>

Loops in programming are a way of repeating actions. There's a lot of flexibility in what you can do with different loops, and you should always consider using them when repeating different actions based on certain conditions. 

#### While Loop

While Loops test the condition before the loop body (anything in between the curly braces is the loop body)

```C#
public class WhileLoop : MonoBehavior 
{
    int cupsInTheSink = 4;

    void Start() 
    {
        while (cupsInTheSink > 0) 
        {
            Debug.Log("I've washed a cup!");
            cupsInTheSink--;
        }
    }
}
/*
* Output in the console should print 4 times --- "I've washed a cup!"
*/
```

#### Do While Loop

Do While Loops test the condition at the end of the body. The different between Do While Loop and While Loop means that the body of the Do While Loop is guaranteed to run at least once.  

```C#
public class DoWhileLoop : MonoBehavior 
{
    void Start() 
    {
        bool shouldContinue = false; 

        do
        {
            print("Hello World"); //The body of the Do While Loop always run at least once
        }
        while (shouldContinue == true); //if shouldContinue is equal to true, keep printing "Hello World", no Hello World should printed after the first one, because the bool is set to false 
    }
}

/*
* Output in the console should only print 1 time --- "Hello World" 
*/
```

#### For Loop

The For Loop works by creating a loop with a controllable number of iterations. 

The syntax for this has three arguments. First off, we introduce a variable that is known as the <strong>iterator</strong>. This is used to count through the iterations of the loop, meaning the loops themselves. 

The second argument is <strong>the validation condition that must be true in order for the loop to continue</strong>. 

Finally, the third argument defines <strong>what happens to the iterator in each loop</strong>. Usually this means adding to the iterator in order to step through the loop. 

It is common in programming to start counting at zero. So, for the first loop, i will be zero, and then the operation ```i++``` adding one to ```i``` will be performed. Then, on the second loop, ```i``` will be one, and so on. 

The loop will continue until ```i``` is no longer less than the ```numEnemies``` variable. 

```C#
public class ForLoop : MonoBehavior 
{
    int numEnemies = 3;

    void Start() 
    {
        for (int i = 0; i < numEnemies; i++)
        {
            Debug.Log("Creating enemy number: " + i);
        }
    }
}

/*
* Output in the console should be:
* Creating enemy number: 0
* Creating enemy number: 1
* Creating enemy number: 2
*/
```

#### Foreach Loop

```C#
public class ForeachLoop : MonoBehavior 
{
    void Start()
    {
        string[] strings = new string[3];

        strings[0] = "First string";
        strings[1] = "Second string";
        strings[2] = "Third string";

        foreach(string item in strings)
        {
            print(item);
        }
    }
}
/*
* Output in the console should be:
* First string
* Second string
* Third string
*/
```

<h3>#6: Scope and Access Modifiers</h3>

The scope of the variable is the area in code which the variable can be used in. A variable is said to be local to the place in code that it can be used. Code blocks are generally what defines a variable's scope, and these are denoted by braces ```{ }```. For example, everything within the class here can be said to be local to that class. You would say that the variables ```alpha```, ```beta```, ```gamma``` are in scope within the scope and access modifiers class. And you would say that the ```pens```, ```crayons```, and ```answer``` variables are in scope within the ```Example``` function. 

Let's talk about <strong>Public and Private Access Modifiers</strong>. Variables defined in the class as opposed to those declared within a function have an access modifier attributed to them. An <strong>access modifier</strong> is a keyword placed before a data type when declaring the variable and its purpose is to define where the variable or function can be seen from. <strong>As a general rule if other scripts need access to a variable or function then it should be public, otherwise it should be private.</strong>

#### IMPORTANT: Declaring a variable as public means that it can be accessed from outside the class. It also means that the variable is shown and editable on the component in the Inspector.

A public variable is normally used for testing purposes since the programmer is able to change the public value in the script component in the inspector. 

Even though you may have initialized the public integer ```alpha``` variable to a value of ```5```, it can still be overwritten by the value set in the inspector. However if these values are set in functions, such as ```Start``` and ```Awake```, these occur after the variable has been set in the Inspector and will not be overwritten by the Inspector. 

```C#
public class ScopeAndAccessModifiers : MonoBehavior 
{
    public int alpha = 5; // This value will be overwritten by the inspector 

    void Start()
    {
        alpha = 29; // This value will NOT be overwritten by the inspector 

        //NOTE #1: alpha can still be overwritten in the inspector, but everytime the game starts, alpha will be initialized to 29. 

        //NOTE #2: alpha can also be overwritten in the Play mode, but the changed value will not be saved once you exit the Play mode 
    }
    
    void Example(int pens, int crayons)
    {
        int answer;
        answer = pens * crayons * alpha; 
        Debug.Log(answer);
    }

    void Update()
    {
        Debug.Log("Alpha is set to: " + alpha);
    }
}

```
<Strong>Private Variables</Strong> can only be edited from within the class. In C#, private is the default access modifier for any variable that doesn't have it specified. So although the   ```beta``` and ```gamma``` are written in private, if they aren't, in default they would both become private variables. 

#### It is good practice to make all member variables, those that belong to a class rather than a function, private, unless they need to be public for a specific reason. 
--

<strong>Setting variables and functions to public can also mean that you can access them from other scripts.</strong>

```C#
public class AnotherClass
{
    public int apples;  //public - can be accessible any any other classes
    public int bananas; //public - can be accessible any any other classes

    private int stapler;
    private int sellotape;

    public void FruitMachine (int a, int b) //public - can be accessible any any other classes
    {
        int answer;
        answer = a + b;
        Debug.Log("Fruit total: " + answer);
    }

    private void OfficeSort (int a, int b)
    {
        int answer;
        answer = a + b;
        Debug.Log("Office Supplies total: " + answer);
    }
}

```

```C#
public class ScopeAndAccessModifiers : MonoBehavior 
{
    public int alpha = 5; 

    private int beta = 0;
    private int gamma = 5;

    private AnotherClass myOtherClass; //calling the class called "AnotherClass" and declared it in this class as a private variable and called as "myOtherClass" 

    void Start()
    {
        alpha = 29;  

        myOtherClass = new AnotherClass(); //this variable myOtherClass is a new instance of the class "AnotherClass"

        myOtherClass.FruitMachine(alpha, myOtherClass.apples); //we can access this AnotherClass instance, which means any public variables or functions in the AnotherClass script, we can access all of them here. 

        //FruitMachine() function is a public function 
        //apples and bananas are both public variables 
        //these are all accessible by the myOtherClass instance 
    }
    
    void Example(int pens, int crayons)
    {
        int answer;
        answer = pens * crayons * alpha; 
        Debug.Log(answer);
    }

    void Update()
    {
        Debug.Log("Alpha is set to: " + alpha);
    }
}

```
<h3>#7: Awake and Start</h3>

These are the two Unity initialization functions: ```Awake``` and ```Start```

In the lifetime of the script, Start and Awake will only be called <strong>one</strong>. 

```Awake``` is useful as it allows you to initialize settings for an object before enabling that script componenet, without the need for splitting the script into several different scripts. 

```C#
using UnityEngine;
using System.Collections;

public class AwakeAndStart : MonoBehaviour
{
    void Awake ()   //References between scripts, initialization 
    //For example: Use Awake to set Ammo for the enemy 
    {
        Debug.Log("Awake called.");
    }
    
    
    void Start () //Once script component is enabled 
    //For example: Use Start to allow enemy to shoot 
    {
        Debug.Log("Start called.");
    }
}
```

<h3>#8: Update and FixedUpdate</h3>

```Update``` is the most commonly used function in Unity. It's called <strong>once per frame on every script</strong> that uses it. Almost anything that needs to be changed or adjusted regularly happens here. 

```C#
void Update()
{
    // Called every frame
    // Used for regular updates, such as:
    //-> moving non-physics objects
    //-> simple timers
    //-> receiving Input 

    //Update interveral times vary 

    Debug.Log("Update time: " + Time.deltaTime);    
}

    /* Output should look similar to below: 
    * Update time: 0.0171322
    * Update time: 0.0252334
    * Update time: 0.3333333
    * Update time: 0.0169745
    * .... 
    */

```
NOTE: ```Update``` is not called on a regular timeline. If one frame takes longer to process than the next, then the time between the Update calls will be different. 

```FixedUpdate``` has a similar function as ```Update```, but it has a few important differences. 

```FixedUpdate``` is called on a regular timeline, and will have the same time between calls. Immediately after ```FixedUpdate``` is called, any necessary physics calculations are made. As such, anything that affects a Rigidbody, meaning a physics object, should be executed in ```FixedUpdate``` rather than ```Update```. 

When scripting physics in the ```FixedUpdate``` loop, it is good practice to use forces for movement. 

```C#
void FixedUpdate()
{
    // Called every physics step 
    // FixedUpdate intervals are consistent 
    // Used for regular updates such as: 
    // -> Adjusting physics (Ridgidbody) objects 

    Debug.Log("FixedUpdate time: " + Time.deltaTime);
}

    /* Output should look similar to below: 
    * FixedUpdate time: 0.02
    * FixedUpdate time: 0.02
    * FixedUpdate time: 0.02
    * .... 
    */

```
###### TIPS: When testing the script in Unity, click on the console to see the output. You can click on Collapse to see the difference clearly. ```FixedUpdate``` output will be collapsed into 1 line in the console which has 1 consistent update time, whereas the ```Update``` output will have multiple lines in the console since the update time is different. 

```Update``` and many other special functions in Unity can be created quickly and easily in Visual Studio by using the MonoBehavior scripting wizard:  

1. In Visual Studio, position the cursor where you want the new function to be inserted, 
2. then press ```Control+Shift+M``` to launch the wizard (_see below for a screenshot of the wizard_). 

![Screenshot 2021-07-06 221944](https://user-images.githubusercontent.com/24945340/124691334-aee4c680-dea9-11eb-85ff-c442c88fc268.png)

3. In the Create Script Methods window, mark the check box next to the name of each method you want to add. 
4. Choose the "Okay" button to exit the wizard and insert the methods into your code. 

Using the wizard in this way can help you to avoid errors in your code, and also help you to discover what functions are available as you're learning. 

<h3>#9: Vector Maths</h3>

In Game Development, we use vectors to define meshes, directions, and all manner of other calculations, which make them essential to understand. A vector is a line drawn between two points, vectors also have a length known as their magnitude. 

#### 2D Vectors 

A 2D vector is a way of represending a point from the origin, the 0,0 point on a graph, to any point on a 2D plane. Since it is from the origin, it has an implied direction. It made up of two components, X and Y, these represent the distance from zero along the X and Y in each axis. 

#### 3D Vectors 

This also applies to subtraction, 3D vectors work the same as 2D, but extrapolated into the Z-axis, which represents depth. The X and Z Axes make up a horizontal plane and Y is the direction that points up. 


#### Dot Product

The <strong>Dot Product</strong> takes 2 vectors and produces a scaler, a single value, from them. To find the Dot Product from 2 vectors, we take their component parts, the X, Y, Z values and multiply them together to find the sum of the resultant values. This is expressed for example as ```(AxBx) + (AyBy) + (AzBz)```, with this product you can find out information about the 2 vectors you've specified. 

#### The Cross Product 

The Cross Product is a different way of combining two vectors, instead of producing a scaler, a single value, the Cross Product produces another vector, specifically, a vector that is perpendicular to the original 2. 

```A ^ B = C```

```Vector3.Cross(VectorA,VectorB)```

Example: Using a rotation torque as an example, the turret is facing in direction (A), and then we would like it to be rotated to face the target item (B), using the perpendicular vector (C) of the other 2 vectors to rotate the turret from direction A to direction B. 

<h3>#10: Enabling and Disabling Components</h3>

Using Enabled flag to toggle over a component (like turning something on or off). 

```C#
using UnityEngine;
using System.Collections;

public class EnableComponents : MonoBehaviour
{
    private Light myLight; 

    void Start()
    {
        myLight = GetComponent<Light>();
    }

    void Update()
    {
        if (Input.GetKeyUp(KeyCode.Space))
        {
            myLight.enabled = !myLight.enabled; 
            //When the light is on (true), then set it to off (false)
            //When the light is off (false), then set it to on (true)
        }
    }
}
```
<h3>#11: Activating GameObjects</h3>

> Active status of GameObjects 

> activeSelf/ activeInHierarchy 

In order to active a GameObject, using the ```SetActive()``` method: 

```C#
using UnityEngine;
using System.Collections;

public class ActiveObjects : MonoBehaviour
{
    void Start ()
    {
        gameObject.SetActive(false); //means that you will see the gameobject greyed out in the hierarchy
    }
}
```
Here is how you are able to check the state (whether it is active on its own or active in hierarchy): 

```C#
using UnityEngine;
using System.Collections;

public class CheckState : MonoBehaviour
{
    public GameObject myObject;
    
    
    void Start ()
    {
        Debug.Log("Active Self: " + myObject.activeSelf);
        Debug.Log("Active in Hierarchy" + myObject.activeInHierarchy);
    }
}
```

When activating or deactivating a gameobject, it is really crucial to be aware of the parent and child relationship. If the parent gameobject is deactivate in hierarchy, the children gameobject can still be active, but since the parent is deactivated, the children also will not be visible in the game. 

> KEY TAKEAWAY: you cannot make a child object active, until the parent is activated again. 

SetActive uses to toggle over the GameObject to see if it should be activated or not. 

<h3>#12: Translate and Rotate</h3>

These are the two transform functions that are used to effect a non-rigidbody object's position and rotation. 

```C#
using UnityEngine;
using System.Collections;

public class TransformFunctions : MonoBehaviour
{
    public float moveSpeed = 10f;
    public float turnSpeed = 50f;
    
    
    void Update ()
    {
        if(Input.GetKey(KeyCode.UpArrow))
            transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime); //move in meter per second instead of meter per frame 
        
        if(Input.GetKey(KeyCode.DownArrow))
            transform.Translate(-Vector3.forward * moveSpeed * Time.deltaTime); //move backward setting negative vector3.forward
        
        if(Input.GetKey(KeyCode.LeftArrow))
            transform.Rotate(Vector3.up, -turnSpeed * Time.deltaTime); //turn left 
        
        if(Input.GetKey(KeyCode.RightArrow))
            transform.Rotate(Vector3.up, turnSpeed * Time.deltaTime); //turn right
    }
    //Vector3.forward and Vector3.Up are relative to the axis of the GameObject 
}
```

>KEY TAKEAWAY: We should not use ```Translate``` and ```Rotate``` for a gameobject that is going to interact with physics. Only use them for non-rigidbody only without physics interaction.

<h3>#13: Look At</h3>

We are moving the camera focus to another target using the function ```LookAt```

```C#
using UnityEngine;
using System.Collections;

public class CameraLookAt : MonoBehaviour
{
    public Transform target;
    
    void Update ()
    {
        transform.LookAt(target);
    }
}

```
Placed the script at the ```MainCamera``` object, then move a gameObject (that you would like the camera to look at) to the public variable ```target```, then you should see your camera is looking at the gameObject you want it to target on. 

You can toggle local and global view in Unity to have a different view on the target. 

<h3>#14: Linear Interpolation</h3>

> Interpolate (dictionary definition): means insert (sth of a different nature) into something else 

In order to linearly interpolate between two values, this can be done using the function called ```Lerp```.

#### Mathf.Lerp

```
The Mathf.Lerp function takes 3 float parameters: 
(1) the value to interpolate from
(2) the value to interpolate to
(3) how far to interpolate 
```

```C#
float result = Mathf.Lerp (3f, 5f, 0.5f); 
//0.5f means 50%
//result = 4f

float result = Mathf.Lerp (3f, 5f, 0f); 
//0f means original value (from)
//result = 3f

float result = Mathf.Lerp (3f, 5f, 1f); 
//1f means the final value (to)
//result = 5f
```

#### Vector3.Lerp

Same principle applies in ```Vector3.Lerp``` - there are 3 floats (x, y, z) for the position

```C#
Vector3 from = new Vector3 (1f, 2f, 3f);
Vector3 to = new Vector3 (5f, 6f, 7f);

// Here result = (4, 5, 6)
Vector3 result = Vector3.Lerp (from, to, 0.75f);

```

#### Color.Lerp

Same principle applies in ```Color.Lerp```. Colours are represented by 4 floats representing ```red, blue, green, alpha```

#### Intensity (smooth over time)

We can use ```Lerp``` function to smooth a value over time

```C#
void Update () //no deltaTime: change to intensity would happen per frame
{
    light.intensity = Mathf.Lerp(light.intensity, 8f, 0.5f);
}

```

```C#
void Update () //with deltaTime: change to intensity would happen per second
{
    light.intensity = Mathf.Lerp(light.intensity, 8f, 0.5f * Time.deltaTime);
}
```

>Please note when smoothing a value, it is often best to use the ```SmoothDamp``` function. Only use ```Lerp``` for smoothing if you are sure of the effect you want


<h3>#15: Destroy</h3>

```Destroy()``` function is used to remove GameObjects and Components at runtime. 

#### Destroy Basic

```C#
using UnityEngine;
using System.Collections;

public class DestroyBasic : MonoBehaviour
{
    void Update ()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(gameObject, 3f); 
            //By adding the second parameter, 
            //it means that there is a delay 
            //of 3 seconds before the gameObject 
            //is destroyed 
        }
    }
}
```

#### Destroy Other

```C#
using UnityEngine;
using System.Collections;

public class DestroyOther : MonoBehaviour
{
    public GameObject other;
    
    
    void Update ()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(other);
        }
    }
}
```

#### Destroy Components 

```C#
using UnityEngine;
using System.Collections;

public class DestroyComponent : MonoBehaviour
{
    void Update ()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(GetComponent<MeshRenderer>());
        }
    }
}
```

<h3>#16: GetButton and GetKey</h3>

These two input function would return a boolean. 

#### KeyInput

```C#
using UnityEngine;
using System.Collections;

public class KeyInput : MonoBehaviour
{
    public GUITexture graphic;
    public Texture2D standard;
    public Texture2D downgfx;
    public Texture2D upgfx;
    public Texture2D heldgfx;
    
    void Start()
    {
        graphic.texture = standard;
    }
    
    void Update ()
    {
        bool down = Input.GetKeyDown(KeyCode.Space);
        bool held = Input.GetKey(KeyCode.Space);
        bool up = Input.GetKeyUp(KeyCode.Space);
        
        if(down)
        {
            graphic.texture = downgfx;
        }
        else if(held)
        {
            graphic.texture = heldgfx;
        }
        else if(up)
        {
            graphic.texture = upgfx;
        }
        else
        {
            graphic.texture = standard; 
        }
        
        guiText.text = " " + down + "\n " + held + "\n " + up;
    }
}
```

#### ButtonInput

In Unity, you can set the button inputs in the ```Edit > Project Settings > Input Manager```. 

```C#
using UnityEngine;
using System.Collections;

public class ButtonInput : MonoBehaviour
{
    public GUITexture graphic;
    public Texture2D standard;
    public Texture2D downgfx;
    public Texture2D upgfx;
    public Texture2D heldgfx;
    
    void Start()
    {
        graphic.texture = standard;
    }
    
    void Update ()
    {
        bool down = Input.GetButtonDown("Jump");
        bool held = Input.GetButton("Jump");
        bool up = Input.GetButtonUp("Jump");
        
        if(down)
        {
            graphic.texture = downgfx;
        }
        else if(held)
        {
            graphic.texture = heldgfx;
        }
        else if(up)
        {
            graphic.texture = upgfx;
        }
        else
        {
            graphic.texture = standard;
        }
    
        guiText.text = " " + down + "\n " + held + "\n " + up;
    }
}
```

<h3>#17: GetAxis</h3>

This input function would return a float value between -1 and 1.

- Negative Button: Left 

- Positive Button: Right

- Gravity: the higher the gravity, the faster the return to 0 after the button has been released. Vice Versa. 

- Sensitivity: the opposite of gravity, the higher the number, the more responsive, the lower the number, the more smooth 

- Dead: 

    - If we were using a joystick to represent our axis, then we wouldnt necessarily want to feel an effect from very small amounts of joystick movement. 
    - To avoid this, we have a Dead Zone
    - The higher the Dead value is, the larger the Dead zone, and the further the joystick must be moved in order for GetAxis to return a non-zero value. 

- Snap: 

    - allows you to return zero if both positive and negative buttons are held 
    
Add an instance of ```Input.GetAxis("Horizontal")``` to receive a value from horiztontal axis, same for vertical, see below: 

##### Basic Axis 

```C#
using UnityEngine;
using System.Collections;

public class AxisExample : MonoBehaviour
{
    public float range;
    public GUIText textOutput;
    
    
    void Update () 
    {
        float h = Input.GetAxis("Horizontal");
        float xPos = h * range;
        
        transform.position = new Vector3(xPos, 2f, 0);
        textOutput.text = "Value Returned: "+h.ToString("F2");  
    }
}

```

##### Dual Axis

```C#
using UnityEngine;
using System.Collections;

public class DualAxisExample : MonoBehaviour 
{
    public float range;
    public GUIText textOutput;
    
    
    void Update () 
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        float xPos = h * range;
        float yPos = v * range;
        
        transform.position = new Vector3(xPos, yPos, 0);
        textOutput.text = "Horizontal Value Returned: "+h.ToString("F2")+"\nVertical Value Returned: "+v.ToString("F2");    
    }
}

```

##### Axis Raw

Input.GetAxis Raw to only return whole numbers and nothing in between (best for 2D games with precise control rather than smooth values), see below: 

```C#
using UnityEngine;
using System.Collections;

public class AxisRawExample : MonoBehaviour
{
    public float range;
    public GUIText textOutput;
    
    
    void Update () 
    {
        float h = Input.GetAxisRaw("Horizontal");
        float xPos = h * range;
        
        transform.position = new Vector3(xPos, 2f, 0);
        textOutput.text = "Value Returned: "+h.ToString("F2");  
    }
}

```
    
<h3>#18: OnMouseDown</h3>
Uses to detect a click on a collider or GUI text element. On the game object, add the Rigidbody and the Mesh Collider components in the inspector. 

```C#
using UnityEngine;
using System.Collections;

public class MouseClick : MonoBehaviour
{
    void OnMouseDown ()
    {
        rigidbody.AddForce(-transform.forward * 500f);
        rigidbody.useGravity = true;
    }
}

```

<h3>#19: GetComponent</h3>
- GetComponent is used to access other scripts that attach to the same game object, or even on other game object, as well as the components on the same or other game object.  

- ```GetComponent<AnotherScript>()```- the type of the GetComponent parameter is AnotherScript 

- Usually call in the Awake or Start function

For Example: 

On the GameObject A 
```C#
using UnityEngine;
using System.Collections;

public class UsingOtherComponents : MonoBehaviour
{
    public GameObject otherGameObject;
    
    
    private AnotherScript anotherScript;
    private YetAnotherScript yetAnotherScript;
    private BoxCollider boxCol;
    
    
    void Awake ()
    {
        anotherScript = GetComponent<AnotherScript>();
        yetAnotherScript = otherGameObject.GetComponent<YetAnotherScript>();
        boxCol = otherGameObject.GetComponent<BoxCollider>();
    }
    
    
    void Start ()
    {
        boxCol.size = new Vector3(3,3,3);
        Debug.Log("The player's score is " + anotherScript.playerScore);
        Debug.Log("The player has died " + yetAnotherScript.numberOfPlayerDeaths + " times");
    }
}

```

On the GameObject A 
```C#
using UnityEngine;
using System.Collections;

public class AnotherScript : MonoBehaviour
{
    public int playerScore = 9001;
}

```

On the GameObject B 
```C#
using UnityEngine;
using System.Collections;

public class YetAnotherScript : MonoBehaviour
{
    public int numberOfPlayerDeaths = 3;
}

```

<h3>#20: DeltaTime</h3>

- means the difference between two values 
- using ```Time.deltatime``` will help to smooth out the movement of an object 
- The effect of using ```Time.deltaTime``` is that it gives us a change in values per second rather than per frame 

```C#
using UnityEngine;
using System.Collections;

public class UsingDeltaTime : MonoBehaviour
{
    public float speed = 8f; 
    public float countdown = 3.0f;

    
    void Update ()
    {
        countdown -= Time.deltaTime;
        if(countdown <= 0.0f)
            light.enabled = true;
        
         if(Input.GetKey(KeyCode.RightArrow))
            transform.position += new Vector3(speed * Time.deltaTime, 0.0f, 0.0f);
    }   
}
```

<h3>#21: DataTypes</h3>

- Value type: 
    - int 
    - float 
    - double
    - bool
    - char
    - Structs 
        - Vector2
        - Quaternion

- Any variable that is an object of a class is a reference type 

- Reference type:
    - Classes
        - Transform 
        - GameObject 

- Difference between Value and Rerence types: 
    - Value type: 
        - variables actually contain some values
        - if the value type changes, only that specific variable is affected  
    - Reference type: 
        - variables contain a memory address where the value is stored 
        - if reference type changes, all variables that contain that memory address will also be affected 

- Charles and Quentin Example in Unity Learn 
    - Value Type: Quentin creates a copy of Charles House. Any changes happen to Quentin's house will have no influence to Charles' house 
    - Reference Type: Quentin visiting Charles' house - since Quentin knows the memory address of Charles' house, he can make a note and then return to that address whenever he needs to.  

```C#
using UnityEngine;
using System.Collections;

public class DatatypeScript : MonoBehaviour 
{
    void Start () 
    {
        //Value type variable
        Vector3 pos = transform.position;
        pos = new Vector3(0, 2, 0);
        
        //Reference type variable
        Transform tran = transform;
        tran.position = new Vector3(0, 2, 0);
    }
}
```
<h3>#22: Classes</h3>

- Variables are boxes, functions are machines, Classes would be factories that these boxes and machines are in! 

- OOP: **Object-Oriented-Programming** - organizational tool - split the script up into multiple scripts

For Example: 

- A Single Script - that contains a lot of functionalities 

```C#
using UnityEngine;
using System.Collections;

public class SingleCharacterScript : MonoBehaviour
{
    public class Stuff
    {
        public int bullets;
        public int grenades;
        public int rockets;
        
        public Stuff(int bul, int gre, int roc)
        {
            bullets = bul;
            grenades = gre;
            rockets = roc;
        }
    }
    
    
    public Stuff myStuff = new Stuff(10, 7, 25);
    public float speed;
    public float turnSpeed;
    public Rigidbody bulletPrefab;
    public Transform firePosition;
    public float bulletSpeed;
    
    
    void Update ()
    {
        Movement();
        Shoot();
    }
    
    
    void Movement ()
    {
        float forwardMovement = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        float turnMovement = Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;
        
        transform.Translate(Vector3.forward * forwardMovement);
        transform.Rotate(Vector3.up * turnMovement);
    }
    
    
    void Shoot ()
    {
        if(Input.GetButtonDown("Fire1") && myStuff.bullets > 0)
        {
            Rigidbody bulletInstance = Instantiate(bulletPrefab, firePosition.position, firePosition.rotation) as Rigidbody;
            bulletInstance.AddForce(firePosition.forward * bulletSpeed);
            myStuff.bullets--;
        }
    }
}
```
Using OOP to split up the single script into the following 3 scripts to make it more organized, easy to read: 

- Script #1: Inventory 
```C#
using UnityEngine;
using System.Collections;

public class Inventory : MonoBehaviour
{
    public class Stuff
    {
        public int bullets;
        public int grenades;
        public int rockets;
        public float fuel;
        
        public Stuff(int bul, int gre, int roc)
        {
            bullets = bul;
            grenades = gre;
            rockets = roc;
        }
        
        public Stuff(int bul, float fu)
        {
            bullets = bul;
            fuel = fu;
        }
        
        // Constructor
        public Stuff ()
        {
            bullets = 1;
            grenades = 1;
            rockets = 1;
        }
    }
    

    // Creating an Instance (an Object) of the Stuff class
    public Stuff myStuff = new Stuff(50, 5, 5);
    
    public Stuff myOtherStuff = new Stuff(50, 1.5f);
    
    void Start()
    {
        Debug.Log(myStuff.bullets); 
    }
}
```

- Script #2: Movements Control
```C#
using UnityEngine;
using System.Collections;

public class MovementControls : MonoBehaviour
{
    public float speed;
    public float turnSpeed;
    
    
    void Update ()
    {
        Movement();
    }
    
    
    void Movement ()
    {
        float forwardMovement = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        float turnMovement = Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;
        
        transform.Translate(Vector3.forward * forwardMovement);
        transform.Rotate(Vector3.up * turnMovement);
    }
}
```

- Script #3: Shooting
```C#
using UnityEngine;
using System.Collections;

public class Shooting : MonoBehaviour
{
    public Rigidbody bulletPrefab;
    public Transform firePosition;
    public float bulletSpeed;
    
    
    private Inventory inventory;
    
    
    void Awake ()
    {
        inventory = GetComponent<Inventory>();
    }
    
    
    void Update ()
    {
        Shoot();
    }
    
    
    void Shoot ()
    {
        if(Input.GetButtonDown("Fire1") && inventory.myStuff.bullets > 0)
        {
            Rigidbody bulletInstance = Instantiate(bulletPrefab, firePosition.position, firePosition.rotation) as Rigidbody;
            bulletInstance.AddForce(firePosition.forward * bulletSpeed);
            inventory.myStuff.bullets--;
        }
    }
}
```
<h3>#23: Instantiate</h3>

- Use Instantiate to **create clones of a Prefab** during runtime 

- One type of Instantiate: takes 1 parameter - the object that we would like to clone - normally this will set to the default position which is zero

- Another type of Instantiate: takes 3 parameters - the object, the position, and the rotation

```C#
using UnityEngine;
using System.Collections;

public class UsingInstantiate : MonoBehaviour
{
    public Rigidbody rocketPrefab;
    public Transform barrelEnd;
    
    
    void Update ()
    {
        if(Input.GetButtonDown("Fire1"))
        {
            Rigidbody rocketInstance;
            rocketInstance = Instantiate(rocketPrefab, barrelEnd.position, barrelEnd.rotation) as Rigidbody; 
            rocketInstance.AddForce(barrelEnd.forward * 5000);
        }
    }
}
```

```C#
using UnityEngine;
using System.Collections;

public class RocketDestruction : MonoBehaviour
{
    void Start()
    {
        Destroy (gameObject, 1.5f);
    }
}
```

<h3>#24: Arrays</h3>

```C#
using UnityEngine;
using System.Collections;

public class Arrays : MonoBehaviour
{
    public GameObject[] players;

    void Start ()
    {
        players = GameObject.FindGameObjectsWithTag("Player");
        
        for(int i = 0; i < players.Length; i++)
        {
            Debug.Log("Player Number "+i+" is named "+players[i].name);
        }
    }
}
```

<h3>#25: Invoke</h3>

Invoke() 
```C#
using UnityEngine;
using System.Collections;

public class InvokeScript : MonoBehaviour 
{
    public GameObject target;
    
    
    void Start()
    {
        Invoke ("SpawnObject", 2);
    }
    
    void SpawnObject()
    {
        Instantiate(target, new Vector3(0, 2, 0), Quaternion.identity);
    }
}
```

InvokeRepeating() 
```C#
using UnityEngine;
using System.Collections;

public class InvokeRepeating : MonoBehaviour 
{
    public GameObject target;
    
    
    void Start()
    {
        InvokeRepeating("SpawnObject", 2, 1);

        //CancelInvoke("SpawnObject"); //this is used to stop the invoke function
    }
    
    void SpawnObject()
    {
        float x = Random.Range(-2.0f, 2.0f);
        float z = Random.Range(-2.0f, 2.0f);
        Instantiate(target, new Vector3(x, 2, z), Quaternion.identity);
    }
}
```

**Invoke can only take on function that has no parameters and can only have a return type of void in order to work successfully.**

<h3>#26: Enumerations</h3>

- Enumerations allow us to create a collection of related constants. Often called as ```enum```- a special data type that has a specific subset of possible values

- Enumerations can be created either inside or outside of a class. 

- Changing the type of enums normally is for optimization 

```C#
using UnityEngine;
using System.Collections;

public class EnumScript : MonoBehaviour 
{
    enum Direction {North, East, South, West};

        void Start () 
    {
        Direction myDirection;
        
        myDirection = Direction.North;
    }
    
    Direction ReverseDirection (Direction dir)
    {
        if(dir == Direction.North)
            dir = Direction.South;
        else if(dir == Direction.South)
            dir = Direction.North;
        else if(dir == Direction.East)
            dir = Direction.West;
        else if(dir == Direction.West)
            dir = Direction.East;
        
        return dir;     
    }
}
```

<h3>#27: Switch Statements</h3>

```C#
using UnityEngine;
using System.Collections;

public class ConversationScript : MonoBehaviour 
{
    public int intelligence = 5;
    
    
    void Greet()
    {
        switch (intelligence)
        {
        case 5:
            print ("Why hello there good sir! Let me teach you about Trigonometry!");
            break;
        case 4:
            print ("Hello and good day!");
            break;
        case 3:
            print ("Whadya want?");
            break;
        case 2:
            print ("Grog SMASH!");
            break;
        case 1:
            print ("Ulg, glib, Pblblblblb");
            break;
        default:
            print ("Incorrect intelligence level.");
            break;
        }
    }
}
```

