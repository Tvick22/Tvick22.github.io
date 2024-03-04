---
toc: true
comments: true
layout: post
title: Individual Review
description: This post goes over everything I learned and did during the Game Project
type: tangibles
courses: { blogs: {week: 7} }
---

# The Canvas HTML Element

During the span of the project, most of the work focused and revolved around the Canvas HTML Element. Along with my team I looked at the different methods and ways I could incorperate and utilize the Canvas element to create my own game in Javascript.

### X and Y coordinates

The Canvas Element makes x and y coordinates a lot easier to incorperate and integarte with each other. For example, while I was adding collsions between objects, I needed to use exact x and y coordinates. The Canvas element made this very easy to do as it gave me exact x and y coordinates of each object on the canvas.

### [drawImage()](https://www.markdownguide.org/basic-syntax/)

```js
drawImage(image, dx, dy)
drawImage(image, dx, dy, dWidth, dHeight)
drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)
```

This is the drawImage() method which takes in an image as the parameter, along with dimensions of the size and width along with x and y coordinates to make drawing the image a lot easier.

- I used this to draw almost all of the elements that appear on the screen (the player sprite, the background, etc.)

# Player movement with classes

## Lopez (player) class

```js
class Lopez {
        constructor() {
            this.image = document.getElementById("lopezSprite");
            this.x = START_X;
            this.y = START_Y;
            this.width = SPRITE_WIDTH*SCALE_FACTOR
            this.height = SPRITE_HEIGHT*SCALE_FACTOR
            this.minFrame = 0;
            this.maxFrame = FRAME_LIMIT -1;
            this.frameX = 0;
            this.frameY = 0;
            this.currentDirection = 'down'; 
        }

        resize() {
            this.width = SPRITE_WIDTH*backgroundImage.playerScaleFactor
            this.height = SPRITE_HEIGHT*backgroundImage.playerScaleFactor
        }
        draw(context) {
            context.drawImage(
                this.image,
                this.frameX * SPRITE_WIDTH,
                this.frameY * SPRITE_HEIGHT,
                SPRITE_WIDTH,
                SPRITE_HEIGHT,
                this.x,
                this.y,
                this.width,
                this.height
            );
        }
        // update frameX of object
        updateFrame() {
            if (this.frameX < this.maxFrame) {
                this.frameX++;
            } else {
                this.frameX = 0;
            }
        }
    }
```

This player class has properties such as x and y values, height and width, and a current direction. Addtionally, the draw method will draw the sprite on the screen, and the updateFrame will help with animation of the sprite.

```js
const validKeys = {
        "w": "up",
        "a": "left",
        "s": "down",
        "d": "right"
    }

let currentKeys = []
    
document.addEventListener("keydown", (event) => {
    const key = event.key;
    const validKey = validKeys[key]

    if (validKey === undefined) {
        return;
    };

    if (!currentKeys.includes(validKey)) {
        currentKeys.push(validKey) //add to currentKeys
    } 

    isMoving = true;
})

document.addEventListener("keyup", (event) => {
    const key = event.key;
    const validKey = validKeys[key]

    if (key == "e") {
        console.log(`(${lopez.x},${lopez.y})`);
        debugger;
    };

    if (validKey === undefined) {
        return;
    };

    currentKeys = currentKeys.filter((currKey) => {
            return currKey !== validKey;  //remove from currentKeys 
    }) 

    isMoving = !!currentKeys.length
})
```

This is a part of the movement script we made so that our player has the ability to move around the screen smoothly. This works by creating an empty array that will be filled with "up", "left", "right", or "down". For example, when the "w" key is being held down the array will show ["up"], if the "w" and "a" keys are being held down, the array will show ["up", "left"]. Using this array, in the game loop, we can now find what directions we are currently supposed to move in, and move our player accordingly.

# Collision Detection

```js
const canMoveUp = () => {
const futureY = player.y - LOPEZ_SPEED
    if (
        player.x + (player.width) >= this.x && //left 
        player.x <= this.x + this.width && //right
        futureY + (player.height) >= this.y && //top
        futureY <= this.y + this.height //bottom
    )
    {
        return false
    }
    return true
}
const canMoveDown = () => {
    const futureY = player.y + LOPEZ_SPEED
    if (
        player.x + (player.width) >= this.x && //left 
        player.x <= this.x + this.width && //right
        futureY + (player.height) >= this.y && //top
        futureY <= this.y + this.height //bottom
    )
    {
        return false
    }
    return true
}
const canMoveLeft = () => {
    const futureX = player.x - LOPEZ_SPEED
    if (
        futureX + (player.width) >= this.x && //left 
        futureX <= this.x + this.width && //right
        player.y + (player.height) >= this.y && //top
        player.y <= this.y + this.height //bottom
    )
    {
        return false
    }
    return true
}
const canMoveRight = () => {
    const futureX = player.x + LOPEZ_SPEED
    if (
        futureX + (player.width) >= this.x && //left 
        futureX <= this.x + this.width && //right
        player.y + (player.height) >= this.y && //top
        player.y <= this.y + this.height //bottom
    )
    {
        return false
    }
    return true
}

const moveableDirections = {
    'left': canMoveLeft(),
    'right': canMoveRight(),
    'up': canMoveUp(),
    'down': canMoveDown()
}

return moveableDirections
```

This is a method of the hitbox object that checks for a collision with the player. It finds the directional collsion by finding the future position of the player, and checking for a collision. For example, for up, we take the current y and subtract the speed to check if the player will be colliding on the next iteration of the game loop. This helps us check for collisions between the player and the hitboxes.

# Working with other people

While working on this project, we all had to find a way to control our versions of the game so there is no overlaps. To do this, we used Github branches to merge our versions together and smoothly integrate our code.

# What I want to learn in the future

I want to learn more about the debugging process in Javascript. I got to get a glimpse of it by making a debug key that uses googles debug tool and also shows the players coordinates.