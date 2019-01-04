## Adding some competition

Your game works and now you can collect points, get special powers from power-ups, and lose. We’re getting somewhere! Maybe it’d be fun to add some competition though — what about including a character that moves around a little, but that you're not supposed to touch? This will be similar to enemies in the traditional platform games like Super Mario that we’re inspired by here.

+ First, pick a sprite to add as your enemy. Because our player character is a cat, I chose a dog. There are lots of other sprites you could add though. I also renamed the sprite **Enemy**, just to make things clearer for me.

+ Resize the sprite to the right size, and place it somewhere appropriate to start. Here’s what mine looks like: 

![The dog enemy sprite](images/enemySprite.png)

+ Write the easiest code first: set up its block for reacting to the `game over`{:class="events"} message to make the enemy disappear when the player loses the game. 

![blocks_1546563698_2998881](images/blocks_1546563698_2998881.png)

+ Now you need to write the code for what the enemy does. You can use mine from this card, but don’t be afraid to add extra bits! (What if they can teleport around to different platforms? Or what if there’s a power-up that makes them move faster, or slower?) 

![blocks_1546563699_366202](images/blocks_1546563699_366202.png)

**Note**: if you just drag the `go to`{:class="block3motion"} block into the sprite panel and don’t change the `x` and `y` values, they’ll be the values for the current location of the **Enemy** sprite!
 
The code in the `if...then`{:class="block3control"} block will make the sprite turn around when they get to the end of the platform!

The next thing you’ll need is for the player to lose a life when their **Player Character** sprite touches the **Enemy** sprite. And you need to make sure the sprites **stop** touching really quickly, since otherwise the code that checks for touching will keep running and the player will keep losing lives. 

+ Here's how I did it, but feel free to try to improve on this code! I modified the **Player Character** sprite’s main block. Add the new code before the `if`{:class="block3control"} block that checks if you're out of lives.

![blocks_1546563700_52772](images/blocks_1546563700_52772.png)

--- collapse ---
---
title: Show me the whole updated script
---

My **Player Character** sprite's main block looks like this now:

![blocks_1546563701_636483](images/blocks_1546563701_636483.png)

--- /collapse ---

The new code hides the **Player Character** sprite, moves it back to its starting position, reduces the `lives`{:class="block3variables"} variable by `1`, and after half a second makes the sprite re-appear.
