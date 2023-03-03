![](../images/line3.png)

### Moving Platforms

<sub>[previous](../jumping-ceiling-ii/README.md#user-content-jumping-and-ceiling-collision-ii) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../moving-platforms-ii/README.md#user-content-moving-platforms-ii)</sub>

![](../images/line3.png)

Now another key feature of platformers is platforms that move.  We do have an issue though.  We cannot control our tiles like we do a game object and animation is limited.  We will need to use a game object to animate so we will have to add another entire section to our collisions for solid tiles.

<br>

---


##### `Step 1.`\|`PLTFRMR`|:small_blue_diamond:

Download [jumpPlatformSourceArt.png](images/jumpPlatformSourceArt.png). *Right click* on **Sprites** and select **New | Sprite** and name it `spr_platform`. Import the above image.

![import image to spr_platform](images/sprPlatforms.png)

![](../images/line2.png)

##### `Step 2.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: 

*Right click* on **Objects** and select **New | Object** and name it `obj_platform`. Set the **Sprite** to `spr_platform`. 

![create obj_platform with platform spriate](images/objPlatform.png)

![](../images/line2.png)

##### `Step 3.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press the **Variable Definitions** button on **obj_platform** as we want to have different start and end points on each platform in the level.  If we set it in the create event we would only be able to have one begining and end position.  We only need to use integers as you can't be placed in between pixels in the game.

![add four integers for begining and end](images/addFourIntegers.png)

![](../images/line2.png)

##### `Step 4.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

 Press the <kbd>Add Event</kbd> and select a **Create** event. Create a variable to track the direction the platform is moving in (to target or back to start), the speed the platform moves at as well as the delay of how long it waits before switching to new direction.

![three vars in create event](images/createEvent.png)

![](../images/line2.png)

##### `Step 5.`\|`PLTFRMR`| :small_orange_diamond:

Press the <kbd>Add Event</kbd> and select a **Step | Step** event. Then check to make sure we are moving towards the target.  Then lets stop the platform from overshooting its target.  Look at the distance between the current position and the target.  Then move the player toward the target with either the platform speed to the distance to the end whichever is smaller.

![move to target logic](images/platformStep.png)

![](../images/line2.png)

##### `Step 6.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond:

 Open up **rm_test** and add another **Instance** layer and call it `MovingPlatform`.  Drag **obj_platform** to the level and place it under the end of the platform we were at.

![add instance layer and platform to test level](images/addPlatformToLevel.png)


![](../images/line2.png)

##### `Step 7.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Double click the platform in the level and press the **Variables** button.  Click the pencil icon on **start_x** and **start_y**. Put in the room x and y position that you have. In my case it is an **x** of `2048` and **y** of `1376`.

![set platform start position](images/addStartVars.png)

![](../images/line2.png)

##### `Step 8.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now move the platform to its final position.  Record its end position in **end_x** and **end_y**.

![add end position](images/endPlatform.png)

![](../images/line2.png)

##### `Step 9.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Move platform back to its starting position.  Move the player next to the platform.

![move platfrom back to begining](images/movePlatform.png)

![](../images/line2.png)

##### `Step 10.`\|`PLTFRMR`| :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now the platform moves up to its target and there is no player platfrom collision.

https://user-images.githubusercontent.com/5504953/157665732-25129c80-e4d6-4937-bc0f-6d0a0d7a34b6.mp4

![](../images/line2.png)

##### `Step 11.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: 

Now we need to add a delay then return to the start.  So lets check to see if the `dist` variable is false (`0`) then we know that you have arrived to the destination.  The `alarm[n]` is set to -1 by default.  We only want to call it once otherwise it will keep moving the alarm forward.  In **Step Events** it is good practice to wrap an alarm in a conditional `if (alarm[0] < 0)`.  Then if both are true we trigger the alarm.

![call alarm when arrived at end](images/addAlarmPlatf.png)

![](../images/line2.png)


##### `Step 12.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Press the <kbd>Add Event</kbd> and select a **Alarm | Alarm 0** event.

Now lets invert the direction of the platform.  Our switch for this is 
`going_to_target`.  If we make it `!going_to_target`, this will change **true** to **false** or **false** to **true**. This means we do not care which direction it is going in, we will be going in the opposite direction after the not.

![alarm 0 invert going_to_target](images/invertDir.png)

![](../images/line2.png)

##### `Step 13.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now we add an `else` statement and do the exact same thing as the `if` except we change the target to `start_x` and `start_y`.

![go back to start](images/goBackToStart.png)

![](../images/line2.png)

##### `Step 14.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. The platform now goes up and down and pauses.

https://user-images.githubusercontent.com/5504953/157869258-385c4e90-3087-482f-abbc-b494980eb24a.mp4

![](../images/line2.png)

##### `Step 15.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: 

Now we may want to collide with multiple objects in our game.  So lets not check collisions with this one object. Lets create an object parent type that all object that want to collide with players can subscribe to.  

*Right click* on **Objects** and select **New | Object** and name it `obj_collision_parent`. DO NOT set a sprite.

![create collision parent](images/collisionParent.png)

![](../images/line2.png)

##### `Step 16.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Now go to **obj_platform** and press the <kbd>Parent</kbd> button.  Assign `obj_collision_parent`.

![assign obj_collision_parent to obj_platform](images/collisionParent2.png)

![](../images/line2.png)

##### `Step 17.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now we need to call a different function to get collisions from the platform.  We will use `collision_point(x, y, obj, prec, notme)`

> Collision_point checks the point specified by the arguments x1,y1 for a collision with any instance of the object specified by the argument "obj".  - [GameMaker Manual](https://manual.yoyogames.com/GameMaker_Language/GML_Reference/Movement_And_Collisions/Collisions/collision_point.htm)

This function will return a reference to the id of the instance of the object that contains `obj_collision_parent`.  We will pass it the same **x** and **y** fealers as we did for the tile.  We will set **prec** to false and **notme** to false (we will not collide with ourself as the player does not have the same parent).

![check for foot collision with platform](images/checkFeeforForObject.png)

![](../images/line2.png)

##### `Step 18.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **check_for_ground**.  We need to move the code tha that moves the player up for a tile collision into the `if` condition.

![move logic](images/moveIf.png)

![](../images/line2.png)

##### `Step 19.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets add another check if the there are no tile collisions check for a collision with an object.  If we do have a collision with either foot we need to get a link to the object instance.  Now we might only have a single valid collision.  We will store the first valid collision in `platorm_collide`.  We will then move the foot of the player (origin bottom center) to one pixel above the platform (whose origin is `0,0` or top left corner).

![move player to object](images/checkPlatform.png)

![](../images/line2.png)

##### `Step 20.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Jump on top of the platform and you should now have ground collision!

https://user-images.githubusercontent.com/5504953/157880588-36a3a062-6906-4e5a-bcc7-abb0dbd761b8.mp4

___


![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Moving Platforms II"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [previous](../jumping-ceiling-ii/README.md#user-content-jumping-and-ceiling-collision-ii)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../moving-platforms-ii/README.md#user-content-moving-platforms-ii)|
|---|---|---|
