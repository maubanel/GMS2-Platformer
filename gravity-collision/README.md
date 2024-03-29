![](../images/line3.png)

### Gravity and Ground Collision

<sub>[previous](../setup-player/README.md#user-content-setup-player) • [home](../README.md#user-content-gms2-platformer) • [next](../gravity-collision-ii/README.md#user-content-gravity-and-ground-collision-ii)</sub>

![](../images/line3.png)

Now we have a surface to run on and we have a player to animate along this surface.  First thing we will do is add gravity and collision detection so the player stays on the ground!

<br>

---


##### `Step 1.`\|`PLTFRMR`|:small_blue_diamond:

Open up **P4v**.  Select the top folder of the **GameMaker** project. Press the <kbd>Checkout</kbd> button.  Checkout out all files in P4V so that they are all writable (otherwise they will be read only and none of the changes will be saved). Select a **New** changelist and add a message describing the unit of work you will be performing. Press the <kbd>OK</kbd> button.

Open up the project you are working on in **GameMaker**. 

![checkout files and create new changelist](images/checkoutFiles.png)

![](../images/line2.png)

##### `Step 2.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: 

Press the <kbd>Add Event</kbd> and select a **Create** event. Add a variable to add an acceleration force downwards every frame to mimic gravity.  Now I feel that for this game a value of `0.2` pixels per frame will work fine and we will use a variable called `p_gravity`.

![add p_gravity of .2 to create event on player](images/createGrav.png)

![](../images/line2.png)

##### `Step 3.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press the <kbd>Add Event</kbd> and select a **Step | Step** event. We will then add a positive value to the `vspeed` to have a downwards acceleration, just like gravity!

![add positive vspeed to step event](images/addGravity.png)

![](../images/line2.png)

##### `Step 4.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **rm_test** and select the **Player** layer and move the player to the top of the screen so we can see him fall down.

![move player to top of rm_test](images/movePlayerUp.png)

![](../images/line2.png)

##### `Step 5.`\|`PLTFRMR`| :small_orange_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now the player will just fall off the bottom of the screen, but the speed looks good.

https://user-images.githubusercontent.com/5504953/157145075-7ed01007-c584-40d8-bf72-6067500ea4e8.mp4

![](../images/line2.png)

##### `Step 6.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond:

Next up we need the player to be able to collisde with the background tiles. Specifically the pink ones we created for collision events. On **obj_player** press the <kbd>Add Event</kbd> and select a **Other | Room Start** event. Why the **Room Start** event?  This way every time the player changes to a new level/room it will check for the new collision link.  This will make sure that the player is always looking at the correct collision map in each room.

For collisions to work we have to know if the player is on top of the ground falling, or inside the ground and needs to be brought up. We need to know if the tile the player is in contains a collision volume.  For this we need to check for the presense of the **ts_collisions**.  We use two functions, the first being `layer_get_id(layer_name)`.

> This function can be used to get the unique ID value for a given layer. In the IDE, all layers have a name and a type, and to be able to edit or change them through code you must give the layer ID value. This function is used to retrieve this ID by using the name (a string) of the layer (as written in the IDE). - [GMS2 Manual](https://manual.yoyogames.com/GameMaker_Language/GML_Reference/Asset_Management/Rooms/General_Layer_Functions/layer_get_id.htm).

With this **ID** we can find out the tilesheet that is assigned to this tile layer. `layer_tilemap_get_id(layer)id)` returns the tilemap (if any) that is assigned to this layer.

> This function can be used to retrieve the unique ID value of the tile map element on a layer. You supply the layer ID (which you get when you create the layer using the layer name (as a string - this will have a performance impact) and the function will return the ID value associated with the tile map element on the layer. [GMS2 Manual](https://manual.yoyogames.com/GameMaker_Language/GML_Reference/Asset_Management/Rooms/Tile_Map_Layers/layer_tilemap_get_id.htm).

![get access to layer](images/getCollisionId.png)

![](../images/line2.png)

##### `Step 7.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now I want the player to be able to stand on the ledge with one foot.  I don't want the ground collision to be the center of the player as if they are half over the ledge I want them to still be **on ground** and not falling. So in this game we will have to check both feet.  It happens to be 6 pixels to the left and to the right that is the center position of each foot when the player is in idle mode (stopped on a ledge for example).

![two collisions for feet](images/twoFootCollision.png)

![](../images/line2.png)

##### `Step 8.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now first we need to adjust the origin of all of our sprites.  The most important thing is to detect if we are on the ground and we are not rotating the sprite.  So we want the origin to be in the middle bottom as we will be checking for ground every frame. We want them to be at the bottom center of the feet. Change the **Origin** to `bottom center` for **spr_player_run**, **spr_player_jump**, **spr_player_idle**, **spr_player_fall** and **spr_player_dead**.

![bottom center origin on all player sprites](images/bottomCenterOrigin.png)

![](../images/line2.png)

##### `Step 9.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press the <kbd>Add Event</kbd> and select a **Step | End Step** event. We need to do all of our collision checking in the **End Step** as the physics of the player is updated between the step and the end step event.

Now we can check 6 pixels to the left and to the right to see if either foot is colliding with a collision tile.  We us the `tilemape_get_at_pixel(tilemap_element_id, x, y)` function to know if there is a collision tile at those two very locations.

> IMPORTANT! If the tiles in the tile map have been unchanged (ie: they are not rotated or flipped etc...), then the return value of the tile set data will be exactly equal to the index of the tile on the tile set. So you can create "collision maps" of tiles using one tile at index 1 in the tile set - for example - then use this function to check for 1 or 0 (an empty tile) to calculate collisions. - [GMS2 Manual](https://manual.yoyogames.com/GameMaker_Language/GML_Reference/Asset_Management/Rooms/Tile_Map_Layers/tilemap_get_at_pixel.htm)

Now we are not rotating these tiles so we will get the index back of where in the tilesheet we are getting a value from. We will print out the result and look at the console window for what we get back.

![check pixel on both feet](images/checkPixel.png)

![](../images/line2.png)

##### `Step 10.`\|`PLTFRMR`| :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Stop the game and look at the bottom console.  You will see that it goes from `0` for both feet (there is no tilesheet in that pixel) or `1` showing that we are seeing the first index in our tilesheet which is our collision.

![1 for collision](images/getPixelReturn.png)

![](../images/line2.png)

##### `Step 11.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: 

When the player leaves the room the value returned in `-1` indicating that there are no tiles of any sort in that area.

![-1 outside of room](images/negativeOne.png)

![](../images/line2.png)

##### `Step 12.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Open up the **Create** event on **obj_player** and add a **boolean** to track if the player is on the ground or not.  Then lets take the left and right foot ground check and turn them into two variables `bottom_left` and `bottom_right`.

![add on_ground and foot variables](images/newVars.png)

![](../images/line2.png)

##### `Step 13.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now instead of hard coding the left and right foot lets add the variable so we can adjust it easily in the create event.

![remove hard coded values](images/adjustHardCoded.png)

![](../images/line2.png)

##### `Step 14.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

So when the player is updated and is below the ground we need to move them back on top.  How do we know how many pxiels they are from the top of the current cel?

![top of cell in pixels?](images/howManyPixels.png)

![](../images/line2.png)

##### `Step 15.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: 

We can use the **modulus** function to get this.  This gives us the remainder of a division.  We represent modulus with the `%` sign.  So if we take the modulus of `6` by `2` (`6/2`) the answer is `0`.  As  6/2 is 3 with a remainder 0 (2 goes into 6 three times).  If we take the modulus of `6` by `4` the answer is `2`.  As 4 goes into 6 one time with a remainder of `2`.

So if we take the modulus of the current y position of the player and take the collision grid size modulus we will get the value we want. So if the player is at `1414` and we take the modulus of `32` we get a value of `6`.  So the player is `6` pixels from the top of the tile grid. If we take `1414 - 6` it is `1408`.  So we the 44th collision tile (1408/32 = 44).

If we want to be on top of the ground we will have to remove one more pixel and the player will be on top of the ground at pixel `1407`.

![use modulus to get y offset](images/modulus.png)

![](../images/line2.png)

##### `Step 16.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Now go back to the **Create** event and create a variable that holds the size of our collision volume.  It is `32` by `32` so we will make it so!

![add tile size variable](images/gridSize.png)

![](../images/line2.png)

##### `Step 17.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now go back to the **End Step** and take the modulus of the `grid_size` and add `1` to get one pixel on top of this tile.

![find modulus distance](images/distanceFromTop.png)

![](../images/line2.png)

##### `Step 18.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now we need to:

1. Create a temporary variable to hold how much we need to move on y if any.

2.  Check if either foot is in the ground.

3.  If one foot is in the ground we want to adjust the y

4.  If the y adjustment is a negative value then the player is in the ground and we will move the y.

5.  Lets add two debug prints to see what is happening.

![adjust y when foot is in ground](images/adjustY.png)

![](../images/line2.png)

##### `Step 19.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you will see that the player does stop and reposition. The problem is that we are continuing to increase the gravity without restricting it.  So eventually the vspeed is larger than the thickness of the collision volume and player falls through.

https://user-images.githubusercontent.com/5504953/157239663-279ce28e-620e-4b28-b589-a0af6a9c5593.mp4

![](../images/line2.png)

##### `Step 20.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond:

So when we make the ground adjustment we know the player is no longer falling.  So we can make the `vspeed` equal to `0` as they are no longer going down.

![0 out vspeed](images/addVSpeed.png)

##### `Step 21.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you will notice the player does not fall through the ground.

https://user-images.githubusercontent.com/5504953/157240612-306d4ced-18ec-4f61-a982-d8ee0042ca2c.mp4

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Gravity and Ground Collision II"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [previous](../setup-player/README.md#user-content-setup-player)| [home](../README.md#user-content-gms2-platformer) | [next](../gravity-collision-ii/README.md#user-content-gravity-and-ground-collision-ii)|
|---|---|---|
