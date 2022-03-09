<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Lateral Movement and Wall Collision

<sub>[previous](../gravity-collision-ii/README.md#user-content-gravity-and-ground-collision-ii) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Now we have the player falling but no lateral movement.  We can't move the player left to right.  We also have no left and right collision.  Lets remedy that!

<br>

---


##### `Step 1.`\|`SPCRK`|:small_blue_diamond:

Lets add a variable to **obj_player | Create** event to track the speed the player runs at.

![add run velocity variable](images/runAcceleration.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

Now we can subtract the `vk_left` key from the `vk_right` key which is subtracting two booleans.  So if the player is holding the left arrow it will be `-1` (0 - 1).  If the player is holding the right key it will be `1` (1 - 0).  If the player is holding no or both keys it will be `0` (0 - 0 or 1 - 1).  So we can now multiply this by our `run_velocity` and it will move either left or right or stay in the same spot.

![set hspeed to input](images/setHspeed.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now run laterally and you can move left and right.  You can also move up to the platforms as the ground collision is doing its job.

https://user-images.githubusercontent.com/5504953/157279964-41c29a59-09d1-48e9-b663-824291ab4184.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:
 
Now lets have the player face in the direction they are supposed to point in. If the player is not moving laterally we will leave the last direction.  If the player is moving then set the `image_xscale` to the `sign (hspeed)`.  This sets it to -1 or 1.  The sign will return `-1` for any negative number (player moving left) and +1 for when `hspeed` is any number above `0`.  This will flip the orientation of the sprite at +1 for right and -1 for left.

![flip player horizontally](images/flipPlayerHor.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`SPCRK`| :small_orange_diamond:

We have done collision detection for the feet.  Now we need to do collision detection for the sides.  We want it to check three collision zones to the left.  Now since the feet narrow and the dog's head is so large we want our side feelers to be further out so in this case it will be `x - 32` pixels away.  On the **y** axis we will be checking three 32 pixels collision zones.  The top of the bottom zone at `-31`, the top of the middle zone at `-63` and the bottom of the top zone at `-65`.  This way our side feelers will not be in the way of the ground or ceiling checks making sure that we are not doing both a ground or ceiling as well as a lateral when not wanted.  

![lateral collisoin diagram](images/lateral_collision.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond:

So lets add these offsets above for our side wall feelers for the player in the **obj_player | Create** event.

![side feeler variables in obj_player](images/sideCreate.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

*Right click* on **Scripts** and select **New | Script** and name it `check_lateral`. This function will work for both left and right.  Lets start with getting left working.  This will take one parameter a boolean called `check_left` that wil tell the function whether to check left or right.

Set the **Sprite** to `spr_foo`.We will use the same function `tilemap_get_at_pixel` to look and see if one of our player's side feelers is inside a collision tile.

![alt_text](images/checkLateral.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

The math is fairlty straight forward to get the player out of the collision area.  We find out which tile they are in and then go the begining of the next tile.  So if we divide the **x** position by the **tile_size** we get a fraction.  We found it up (using `ceil(n)`). We then multiply it by the tile size and it gets to the beginning of the next tile.  In this illustration tile 1 goes from 0 to 31, second from 32 to 63 and the begining of the third tile is `64`. 

![illusttration of collision math for sides](images/collisionMath.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/grid_size.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`SPCRK`| :large_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 16.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 17.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 18.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 19.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 20.`\|`SPCRK`| :large_blue_diamond: :large_blue_diamond:

![alt_text](images/.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 21.`\|`SPCRK`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

![alt_text](images/.png)

___


<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - ADD NEXT PAGE">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [previous](../gravity-collision-ii/README.md#user-content-gravity-and-ground-collision-ii)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../)|
|---|---|---|
