<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Jumping and Ceiling Collision

<sub>[previous](../lateral-collision-ii/README.md#user-content-lateral-movement-and-wall-collision-ii) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../jumping-ceiling-ii/README.md#user-content-jumping-and-ceiling-collision-ii)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Now it is not much of a platformer without being able to jump.  lets add the ability to jump and also add ceiling collision so the player can't pentrate the top of a tile.

<br>

---


##### `Step 1.`\|`SPCRK`|:small_blue_diamond:

Open up **obj_player | Create** event.  Lets add a variable that holds how much force will be applied on the player for jumping in pixels. 

![add jump force variable](images/jumpForce.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

Move the **Step** event and add to the bottom a check for the space bar and add an upwards force so the player jumps.

![step event jump logic](images/jumpStep.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Press the jump button.  Notice though that you do not collide with ceilings.

https://user-images.githubusercontent.com/5504953/157585633-337765c2-efb2-4b5f-9a5d-006cff9f1373.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now open up the jump animation.  Make sure the first two frames is the inbetween of going from standing to jumping.  It loops from the 2nd frame onwards just like the fall animation.

https://user-images.githubusercontent.com/5504953/157586295-98232f42-187d-4b56-b78a-ab9f8ee03b40.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`SPCRK`| :small_orange_diamond:

Open up the **obj_player | Animation End** and a loop from the second frame onwards.  We can use the same logic as for the fall animation just add this logic for both the fall and the jump animation.

![player jump animation loop](images/playerJumpES.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond:

Open up **obj_player | End Step** event and add to the bottom a check for not being on the ground and with a negative `vspeed` (moving updwards).  We will then switch to the `spr_player_jump` animation.

![open up end step and play jump animation](images/endStepJump.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you will see different animations for jumping versus falling.

https://user-images.githubusercontent.com/5504953/157645417-7015e161-9ba0-4b32-a8ea-45145b51d978.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

The top feelers will be a bit further apart from the feet.  The ears are sticking up so we will use the middle of the ear as the point for checking for ceiling.  This is +-12 pixels from the center. We are only making the player 96 pixels high so the ears will clip behind the platforms.

![illustration of top feelers](images/topFeelers.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **obj_polayer | Create** event and add two variables for the x offsets of the collision.

![x offset variables](images/topLeftRightOff.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`SPCRK`| :large_blue_diamond:

*Right click* on **Scripts** and select **New | Script** and name it `check_ceiling`. The first thing we will check for is if we are falling downwards.  If we are falling down, there is no point in checking for ceiling collisions.

![check for going down in ceiling collision](images/checkCeilingFunc.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: 

Now lets check to see if either of the two top feelers are colliding with a collision tile.

![check top feelers](images/checkTopFeelers.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Now if there are no collisions then return a false.  There is nothing else to do.

![return false if no collision](images/checkIfNoCollision.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now we do the same thing as the other collisions by taking the ceiling of the current y position (we are checking the feet so dpon't need to add 96 then subtract 96 to check the ceiling feelers). We then multiply it by 32 and it will return the next pixel in the grid square below.

![sets grid square below diagram](images/collisionMath.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now lets change that into code.  Open up `check_ceiling` and add a check to see if there is a collision then adjust the player to the cell beneath the one they are in.

![adjust cell downwards](images/colllisionInScript.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: 

Place a collision platfrom one grid piece above the player's head.

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now the player collides.  But the player gets "stuck" on the ceiling as it takes a while for gravity to reverse the upwards force especially on a short jump.

https://user-images.githubusercontent.com/5504953/157647158-262fc276-8544-4d88-9927-c4d32d63a591.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 16.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

I think I would like to keep a bit of ceiling friction.  Sliding the head along the ceiling is kind of fun.  What we will do is have that collision slow down the player by 20% each collision frame, making gravity take over much faster.

![adjust vspeed on ceiling collision](images/reduceCeilingFriction.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 17.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **obj_player | End Step** and call `check_ceiling()` after you have checked the lateral collisions.

![call check_ceiuling() in obj_player end step event](images/checkCeilingCol.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 18.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Jump into the ceiling again.  Now it looks and feels a lot better!

https://user-images.githubusercontent.com/5504953/157653357-9763e7ea-6929-4a0c-bc9e-c37b03f66a16.mp4

___


<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Jumping and Ceiling Collision II">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [previous](../lateral-collision-ii/README.md#user-content-lateral-movement-and-wall-collision-ii)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../jumping-ceiling-ii/README.md#user-content-jumping-and-ceiling-collision-ii)|
|---|---|---|
