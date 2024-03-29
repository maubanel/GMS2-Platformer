![](../images/line3.png)

### Moving Platforms II

<sub>[previous](../moving-platforms/README.md#user-content-moving-platforms) • [home](../README.md#user-content-gms2-platformer) • [next](../ground-hazards/README.md#user-content-ground-hazards)</sub>

![](../images/line3.png)

Lets get collision detection working on objects.

<br>

---


##### `Step 1.`\|`PLTFRMR`|:small_blue_diamond:

For the platform check we cannot just check 1 pixel below the player's feet as the platform is moving. We have to move the speed of the platform to the check to see if the player is still standing on the platform.  To do this we need to open up **obj_platform | Create** and **obj_platform | Step** events and chnage `platform_speed` to `global.platform_speed`.


![change platform_speed to global](images/changeGlobal.png)

![](../images/line2.png)

##### `Step 2.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: 

 Open up `check_for_ground`. Now we need to also check in the `if (on ground)` section to see if the pixel below is on ground of a moving platform.  We look 1 + the platform speed pixels below to check for being right on top of the ground.

![check one pixel above](images/checkBelow.png)

![](../images/line2.png)

##### `Step 3.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up `check_lateral` and lets add collision for moving laterally.  We check left to the same zones as we do with the tiles but move as an offset off of the position of the object we collided with.

![left collision](images/checkLateral.png)

![](../images/line2.png)

##### `Step 4.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Run into the moving platform from the left and collisions should work.

https://user-images.githubusercontent.com/5504953/158065724-25ba6232-cbf7-47e5-aca9-6403b02cab70.mp4

![](../images/line2.png)

##### `Step 5.`\|`PLTFRMR`| :small_orange_diamond:

Now we need to do the same thing to the right.  We need to place the offset left side one pixel to the left of the playeform.

![add right collision](images/adjustToRight.png)

![](../images/line2.png)

##### `Step 6.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond:

Check you brackets very carefully to make sure they are in the correct spot or the logic will not work.

![check brackets](images/check_brackets.png)

![](../images/line2.png)

##### `Step 7.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. The collision to the right works now!

https://user-images.githubusercontent.com/5504953/158003271-ea9380de-edd4-4c50-89a8-95132e3c89a2.mp4

![](../images/line2.png)

##### `Step 8.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now open up `check_ceiling` and we will add a duplicate check of any object the player could run into. We use the same feelers distance as we did for the tiles.  We also now look for no collision acress tiles OR objects before deciding that there is no collsioin.

![add check to ceiling](images/checkCeiling.png)

![](../images/line2.png)

##### `Step 9.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now we will have to adjust the player to just below the sprite we have collided with to get into the right space just before the collision. 

![adjust player](images/checkForObjCol.png)

![](../images/line2.png)

##### `Step 10.`\|`PLTFRMR`| :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now we collide with the top of the platform.  The issue now is that the platform will push the player into the platform if the player is under it and cause a pretty glichy bug as they will zap to the right.

https://user-images.githubusercontent.com/5504953/222923007-ca24fde9-d92a-41cf-8c41-810fbf41c82b.mp4

![](../images/line2.png)

##### `Step 11.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: 

Now we will reverse the direction of the platform if it collides with the player.  So we will add a check in the platfrom to see if the player is within 92 pixels and still collides with the platformer then reverse direction.  We will need to do this in an end step and access the distance variable.  Open up **obj_platform | Step** event and move the `dist` variable to outside the brackets so it is good everywhere in this script.

We want to look to after the platform has moved to the new position.  We will use `instance_place(x, y, obj)` to determine if there is still a collision between the player and the platform.  Now there is no guarantee that the player will run its collision detection and move the player out of the way. So we will only reverse direction if the collision volume is within 92 pixels (the player is 92 pixels tall) of its desitnation (`dist`).  This should stop the platform from pushing the player off to the right.

![alter dist from local var to normal var](images/alterDist.png)

![](../images/line2.png)

##### `Step 12.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 


Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now run around the platform and it only seems to reverse when crushing the player.

https://user-images.githubusercontent.com/5504953/158018940-2dd167a8-8174-4448-b5ad-7e98043a438c.mp4


![](../images/line2.png)

##### `Step 13.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 


Turn on the **Collision** layer so we can see it.  Select the **Platform** tile layer and on the right side of the room add two jump platforms that you need to double jump to (three blocks high).  Add another moving platform to take you from one end to another.

![add jump area](images/jumpArea.png)


![](../images/line2.png)

##### `Step 14.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 


Now go back to the **Collision** layer and add the collisions to these two new platforms.

![add collision to new platforms](images/addCollisions.png)


![](../images/line2.png)

##### `Step 15.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: 


Turn the **Collisions** view off.

![turn collisions off](images/viewOff.png)


![](../images/line2.png)

##### `Step 16.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

You now should bring the moving platform to the starting point on the far right.  You can get the **start_X**, **start_Y** and **end_Y** based on its position.

![set three points on moving platform](images/changeStartEnd.png)

![](../images/line2.png)

##### `Step 17.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now you can move the platform to the left to its target position and set the **end_x**.

![set end_x](images/setEndX.png)

![](../images/line2.png)

##### `Step 18.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now jump on the sideways platform.  Woops the platform moves underneath the player.  We want the player to move with the platform.

https://user-images.githubusercontent.com/5504953/158022971-00a35221-91c1-4392-8f0a-a3cf2802c446.mp4

![](../images/line2.png)

##### `Step 19.`\|`PLTFRMR`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **check_for_ground** and we will need to also turn off the gravity when the player lands on an object (like we did when they land on the tile).  Set `vspeed` to `0` when they are colliding with an object.

![remove fractional error on ground in end_step](images/neutralizeFalling.png)

![](../images/line2.png)

##### `Step 20.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond:

So we now open up **check_for_ground** and in the checking for 1 pixel below ground we look to see if we are on a moving platform (object collision).  If we are get a reference to the valid collision result then adjust the player's `x` by the `hspeed` of the platform.

![adjust player to move along collision box](images/moveAlongGround.png)

![](../images/line2.png)

##### `Step 21.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you will move along with the platform when standing on it.  I also tested that the platform can't crush the player into the platform horizontally (our previous code should work here).

https://user-images.githubusercontent.com/5504953/158024490-4cf62262-32c2-4441-9a60-d5d73c80c938.mp4

![](../images/line2.png)

##### `Step 22.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond: small_blue_diamond:

Select the **File | Save Project**, then press **File | Quit** (PC) **Game Maker | Quit** on Mac to make sure everything in the game is saved.

![save then quit gamemaker](images/saveQuit.png)

![](../images/line2.png)

##### `Step 23.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond: small_blue_diamond: small_blue_diamond:

Open up **P4V**.  Select the top folder and press the **Add** button.  We want to add all the new files we created during this last session.  Add these files to the last change list you used at the begining of the session. Make sure the message accurately represents what you have done. Press the <kbd>OK</kbd> button.

![add new and changed files to p4v](images/add.png)

![](../images/line2.png)

##### `Step 24.`\|`PLTFRMR`| :large_blue_diamond: :large_blue_diamond: :small_blue_diamond: small_blue_diamond: small_blue_diamond: small_blue_diamond:

Now you can submit the changelist by pressing both <kbd>Submit</kbd> buttons.

![submit changelist to p4v](images/submit.png)

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Ground Damage"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [previous](../moving-platforms/README.md#user-content-moving-platforms)| [home](../README.md#user-content-gms2-platformer) | [next](../ground-hazards/README.md#user-content-ground-hazards)|
|---|---|---|
