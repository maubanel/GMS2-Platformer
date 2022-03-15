<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Jump Through Collisions

<sub>[previous](../) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Lets do one final plaformer trope and that is a platform type you can jump through.  We will have a cloud and there will only be ground collision with no side or ceiling collision.

<br>

---


##### `Step 1.`\|`SPCRK`|:small_blue_diamond:

Download [spr_jump_cloud.png](images/spr_jump_cloud.png).  *Right click* on **Sprites** and select **New | Sprite** and name it `spr_cloud`. 

![import spr_jump_cloud to its own sprite](images/sprClous.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

*Right click* on **Objects** and select **New | Object** and name it `obj_cloud`. Set the **Sprite** to `spr_cloud`. Press the <kbd>Parent</kbd> button and select **obj_collision_parent**.

![add obj_cloud and add collision parent](images/objCloud.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **rm_test** and remove the three jump platforms.  We will replace them with the jump clouds.

![remove jump platforms](images/removeJumpPlatforms.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Don't forget to remove the hidden collisions as well!

![remove collisions for removed platforms](images/removeColl.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`SPCRK`| :small_orange_diamond:

Now we need to add some cloud platforms one above the other so you can jump through them.

![add cloud jump platforms](images/objCloudInLevel.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond:

Open up **obj_collision_parent**. Press the <kbd>Add Event</kbd> and select a **Create** event. Add variable called `can_jump_through` and set the default to `false` so we don't mess with our previous working platforms.

![add create event to obj_collision_parent](images/canJumpThroughVar.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now we need to open up **check_ceiling** and when we check the object `else if (left_check_obj || right_check_obj) and check to see if you can't jump through the platforms.  If you can't resolve the collision or otherwise let the person go through returning false.

![check for can_jump_through in ceiling](images/addCheckForCeiling.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you can jump under the cloud but the side collisions push you out to the side.  Also check the old platform to see if it works.  Woops, we get a carsh bug!

https://user-images.githubusercontent.com/5504953/158473648-636322bf-ca87-481c-8fcf-eb3437c0d890.mp4


<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Why did we get this error?  We have a variable declared in the parent so **obj_platform** should inherit it.  Open up **obj_platform**. Woops, it already has a **Create** event so we have overriden the parent.  This is an easy fix, just add a `event_inherited()` to inherit the parents vars.  We don't need to adjust it as we want it to be the default of `false`.

![add event_inherited to obj_platform](images/inherit.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`SPCRK`| :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Test it again and it still collides and this time with no error!

https://user-images.githubusercontent.com/5504953/158474701-90a60029-898d-4674-b63a-df88873f9a04.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: 

Now lets fix the lateral collision. Open up the **check_lateral** script and add a check before adjusting for an object collision checking the `can_jump_through` variable. Do this for the left and the right direction.

![add check for can_jump_through in lateral](images/adjustLateral.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now jump through the platforms.  The only issue is that is pulling the player up and not letting them jump above and falling down onto the platform.  

https://user-images.githubusercontent.com/5504953/158481370-5452445b-b0d7-4b69-8229-342778960015.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Open up **check_for_ground** and before you adjust the object collision accept it if `can_jump_through` is false or if `can_jump_through` is `true` and the previous frame is higher than the platform.  We ust `yprevious` to get the last fraome position.  So we want the player to jump above the platform then land, so the previous frame must be **less** (or higher) than the current one.

![check for ground adjustment for jumping through clouds](images/checkForPrevFrame.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now I changed the layout in **rm_test** and separated them by 4 collision blocks and put some blocks at the bottom left.

![reconfigured jump platforms](images/reconfiguredPlatforms.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`SPCRK`| :large_blue_diamond: :small_orange_diamond: 

https://user-images.githubusercontent.com/5504953/158481339-af0838df-bee2-4150-903f-8aa92867eba5.mp4

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

| [previous](../)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../)|
|---|---|---|
