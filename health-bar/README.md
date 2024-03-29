![](../images/line3.png)

### Health Bar

<sub>[previous](../ground-hazards/README.md#user-content-ground-hazards) • [home](../README.md#user-content-gms2-platformer) • [next](../lives/README.md#user-content-lives)</sub>

![](../images/line3.png)

Instead of using the built in health bar that we have been using lets do something more original.  Lets use 5 hearts with 4 pieces repreensting the player's health.

<br>

---

##### `Step 1.`\|`PLTFRMR`|:small_blue_diamond:

Open up **P4v**.  Select the top folder of the **GameMaker** project. Press the <kbd>Checkout</kbd> button.  Checkout out all files in P4V so that they are all writable (otherwise they will be read only and none of the changes will be saved). Select a **New** changelist and add a message describing the unit of work you will be performing. Press the <kbd>OK</kbd> button.

Open up the project you are working on in **GameMaker**. 

![checkout files and create new changelist](images/checkoutFiles.png)

![](../images/line2.png)

##### `Step 2.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: 

Download [spr_health_strip5.png](images/spr_health_strip5.png). *Right click* on **Sprites** and select **New | Sprite** and name it `spr_health`. Press **Edit Image** and select **Image | Import Strip Image**. You have a heart with 4 quarters as well as an empty one.  Change **Number of Frames** and **Frames per Row** to `5` as there are 5 `32` by `32` hearts.

![spr_health hearts](images/stripOfHearts.png)

![](../images/line2.png)

##### `Step 3.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

![import spr health hearts](images/healthHearts.png)

Now you should have a strip of hearts called `spr_health`.

![](../images/line2.png)

##### `Step 4.`\|`PLTFRMR`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now open up **obj_game | draw** and erase the entire script.  Lets start over. Now lets divide the player health by 5 and take the floor of the number so that we have an integer in return.

![fifth of a hundred](images/FifthOfHun.png)

![](../images/line2.png)

##### `Step 5.`\|`PLTFRMR`| :small_orange_diamond:

With the `fifth` variable of the result of health / 20 we will render the last heart with a result of 16 to 20.  Then we take the reverse remainder to pick which image_index to pick.  We need to also select index 4 when the heart is empty.

![hearts for hud 85 to 100](images/hearts85.png)

![](../images/line2.png)

##### `Step 6.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now play the game and take damage.  You see the heart goes from a full health all the way to none for the fifth heart.

https://user-images.githubusercontent.com/5504953/158066446-252f35a3-5d11-4595-a89e-e1ad975b2fa0.mp4

![](../images/line2.png)

##### `Step 7.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets do the same thing for 65% to 80%.  We will look at values beetween 15 and 13.

![last two hearts](images/lastTwoHeartws.png)

![](../images/line2.png)

##### `Step 8.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now play the game and take damage.  Look at the last two hearts working.

https://user-images.githubusercontent.com/5504953/158066461-06814c85-7693-4bcd-b454-1eb5ac7650fb.mp4

![](../images/line2.png)

##### `Step 9.`\|`PLTFRMR`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

We just repeat the same formula to finish the first three hearts. Now we should have a range between `0` and `100` health.

![add 0 to 65% for health indicators](images/restOfHealth.png)

![](../images/line2.png)

##### `Step 10.`\|`PLTFRMR`| :large_blue_diamond:

Now *press* the <kbd>Play</kbd> button in the top menu bar to launch the game. Now you should be able to go from `100` per cent health to `0`. 

https://user-images.githubusercontent.com/5504953/158066479-c48a4074-eb8f-472a-a3b0-051da639244d.mp4

![](../images/line2.png)

##### `Step 11.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: 

Select the **File | Save Project**, then press **File | Quit** (PC) **Game Maker | Quit** on Mac to make sure everything in the game is saved.

![save then quit gamemaker](images/saveQuit.png)

![](../images/line2.png)

##### `Step 12.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Open up **P4V**.  Select the top folder and press the **Add** button.  We want to add all the new files we created during this last session.  Add these files to the last change list you used at the begining of the session. Make sure the message accurately represents what you have done. Press the <kbd>OK</kbd> button.

![add new and changed files to p4v](images/add.png)

![](../images/line2.png)

##### `Step 13.`\|`PLTFRMR`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now you can submit the changelist by pressing both <kbd>Submit</kbd> buttons.

![submit changelist to p4v](images/submit.png)

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Lives"> -->

![next up - ](images/banner.png)

![](../images/line.png)

| [previous](../ground-hazards/README.md#user-content-ground-hazards)| [home](../README.md#user-content-gms2-platformer) | [next](../lives/README.md#user-content-lives)|
|---|---|---|
