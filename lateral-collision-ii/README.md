![](../images/line3.png)

### Lateral Movement and Wall Collision II

<sub>[previous](../lateral-collision/README.md#user-content-lateral-movement-and-wall-collision) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../jumping-ceiling/README.md#user-content-jumping-and-ceiling-collision)</sub>

![](../images/line3.png)

Lets add the collision for moving right.

<br>

---


##### `Step 1.`\|`PLTFRMR`|:small_blue_diamond:

Now the collision on the right will be similar to the collision on the left.  Since the player's right hand side is colliding it will hit the collision volume's left side.  So we round down (`floor()`) the collision then multiply by `32` to get the begining of the cell.  We subtract 1 as we need the player to be one pixel outside the collision volume.

![adjust player left when right collides illustration](images/rightCollisionExplanation.png)

![](../images/line2.png)

##### `Step 2.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: 

We can reuse the left Y positions as they are the same for looking right the feelers will be at the same height.  Lets just add the x offset which is 32 pixels from the right or origin (center) of our player sprite. Open **obj_player | Create** event and add this new variable.

![add right offset in craete event](images/rightX.png)

![](../images/line2.png)

##### `Step 3.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up the `check_lateral` script and move the left collision movement inside the `if` statement.  I put it in the wrong place and to check right we will need to fix this.

![move check left](images/moveCollision.png)

![](../images/line2.png)

##### `Step 4.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now we will add an `else` when `check_left` is `false`.  We will then try three feelers to the right of the player to see if they are colliding with an object on the right.

![add three right collision checks](images/checkRightSide.png)

![](../images/line2.png)

##### `Step 5.`\|`PLTFRMR`| :small_orange_diamond:

Now we adjust the player leftwards to the end of the cell prior to the one that the feeler is in.  So we round down (`floor(n)`) then multiply by `32` then subtract `1` to get to the edge on the left hand side of the collision volume.

![move player left](images/newFormula.png)

![](../images/line2.png)

##### `Step 6.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond:

Now we need to go the **obj_player | End Step** and add a call to check the right hand side of the collision.  We call the same function `check_lateral` but pass it `false` so it checks the right hand side.

![call check lateral function for right hand collsion](images/checkRight.png)

![](../images/line2.png)

##### `Step 7.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now create a mirror of the same collisions on the left to test the four zones (first three with collisions and the player should be able to pass under the fourth). 

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Check all the collision feelers and it should work correctly.

https://user-images.githubusercontent.com/5504953/157450269-d54a530b-382b-4a18-9ba4-387abef01eef.mp4

___

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Jumping and Ceiling Collision"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [previous](../lateral-collision/README.md#user-content-lateral-movement-and-wall-collision)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../jumping-ceiling/README.md#user-content-jumping-and-ceiling-collision)|
|---|---|---|
