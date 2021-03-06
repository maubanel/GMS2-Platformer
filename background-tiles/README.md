<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Background Tiles

<sub>[previous](../setting-up/README.md#user-content-setting-up) • [home](../README.md#user-content-gms2-top-down-shooter) • [next](../setup-player/README.md#user-content-setup-player)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Lets set up a playground so that we can test various elements of a platormer.  Lets start by putting down some tiles that we can get our collision detection system working.

<br>

---


##### `Step 1.`\|`SPCRK`|:small_blue_diamond:

Download [spr_platformer_tiles.png](images/spr_platformer_tiles.png). *Right click* on **Sprites** and select **New | Sprite** and name it `spr_platformer_tiles`. Press the <kbd>Import</kbd> button to bring in a basic set of tiles.  

![import spr_platformer_tiles and create sprite](images/importTiles.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

*Right click* on **Tile Sets** and select **New | Tile Set** and name it `tls_platformer_bkg`. Assign **spr_platformer_tiles** to this **Tile Set**. Change the **Tile Width** and **Tile Height** to `64`.  This is the size I used when creating the tiles.

![create tileset with above sprite](images/tlsPlatformer.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Open up **Room Test**.  Chnage the **Width** and **Height** of the room to `4032` wide by `1536` high.  Select `Enable Viewport` and open up **Viewport 0** and click on `Visible`.  Add a new **Tileset** layer and call it `Platforms`.  Assign the **tls_platformer_bkg** to this layer.

![setup room to receive tiles](images/assignRoomTileset.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`SPCRK`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Select the new **Platforms** layer and select the solid ground tile.  Place it along the bottom of the room to establish a floor, so the player can't go beneath the bottom of the screen.

![add floor tiles](images/layGroundwork.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`SPCRK`| :small_orange_diamond:

Lets establish a ground layer and select the full block of ground with grass on top.  This will tile on top of our ground layer.  Also add 6 boxes at either side of the level to prevent the player from leaving.

![add grass ground and box in player](images/boxAndGrass.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond:

Lets build an area close to the start (the bottom left of the screen) with some jump platforms.  We should be able to single jump onto both of these platforms.

![add jump platforms](images/testJumpingArea.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets offset the camera so it starts at the bottom left of the level.  Open up **rm_test** and change the **Viewport 0 | YPos** to `768` which brings the starting window to the correct spot. 

![alt_text](images/offsetCam.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Download [spr_collisions.png](images/spr_collisions.png). We will use this as our collision detection layer. We need some way to have a separate layer that tells players where they can and cannot move into.  The smaller these are the more expensive they get.  We made ours `32` by `32`.  *Right click* on **Sprites** and select **New | Sprite** and name it `spr_collisions`. Press the <kbd>Import</kbd> button to bring in a single collision tile.  

![download spr_collisions.png](images/sprCollisions.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`SPCRK`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

*Right click* on **Tile Sets** and select **New | Tile Set** and name it `tls_collisions`. Assign **spr_collisions** to this **Tile Set**. Change the **Tile Width** and **Tile Height** to `32`.  

![create collision tileset](images/createCollisionTileset.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`SPCRK`| :large_blue_diamond:

Open up **rm_test** and add another **Tile Set** layer and call is `Collisions`.  Assign tls_collisions.
![add collisions layer](images/collisionLayer.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: 

Select the **Collisions** layer and start to put the single pink tile to where you want the player to not enter.  So this would be the far left edge of the wall and the top edge of the floor.  This will be hidden when the game is ready is played, and is visually just showing us the collision volume so we can test our collision detection system.

![add collision to level](images/startCollisions.png)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`SPCRK`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Now continue and add collision volumes along the entire bottom section of the level including both side walls.

![finish collisions](images/collisionEntireBottom.png)

___


<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Setup Player">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [previous](../setting-up/README.md#user-content-setting-up)| [home](../README.md#user-content-gms2-top-down-shooter) | [next](../setup-player/README.md#user-content-setup-player)|
|---|---|---|
