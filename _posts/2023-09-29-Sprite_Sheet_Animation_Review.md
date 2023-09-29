---
toc: true
comments: false
layout: post
title: Sprite Sheet Animation Review
description: This post goes over the steps I took animate my sprite
type: hacks
courses: { blogs: {week: 5} }
---

# The HTML Portion
```html
    <div>
        <div class="w-full flex justify-center">
            <canvas id="spriteContainer"> <!-- Within the base div is a canvas. An HTML canvas is used only for graphics. It allows the user to access some basic functions related to the image created on the canvas (including animation) -->
                <img id="skeletonSprite" src="../../../images/SpriteSheet.png">  // change sprite here
            </canvas>
        </div>
        <div id="speedTooltip" class="tooltip tooltip-bottom w-full" data-tip="ChangeSpeed">
        <input id="speed" type="range" min="0" max="100" value="0" class="range mt-4" />
        </div>
    </div>
```

> I have a div that wraps around the sprite image. It uses CSS to make sure the sprite is centered on the page. Inside that I have the canvas and image with their unique ids.

> Under the sprite, there is a bar which gives you the option to change the speed. I used CSS to make it look like a bar, and have a tooltip that tells the user what the bar controls. The input itself has an id called 'speed' and a value property.

```js
    this.maxFrame = FRAME_LIMIT-1;
```

> Here, I fixed an error that would repeat frames 1 too many times by removing 1 from the FRAME_LIMIT variable. This fixed the blinking effect that we were experiencing.

```js
const validKeys = {
            "w": "up",
            "a": "left",
            "s": "down",
            "d": "right",
};

document.addEventListener("keypress", (event) => {
    if (!Object.keys(validKeys).includes(event.key)) {
        return;
    }
    changeAnimation(validKeys[event.key]); 
});
```

> In this area, I let the user use their WASD keys to control the animation rather than the radio inputs. The code has an event listener that checks if a key pressed was a "valid key" (W, A, S, or D) and then uses the input to change the animation (with the changeAnimation() function)

```js
SPRITE_SPEED = 100 - document.getElementById("speed").value
    // Uses `requestAnimationFrame` to synchronize the animation loop with the display's refresh rate,
    // ensuring smooth visuals.
setTimeout(() => {requestAnimationFrame(animate);}, SPRITE_SPEED);
```

> In this spot, I make the framerate of the animation change due to the SPRITE_SPEED variable. SPRITE_SPEED is a number that defines how many miliseconds of delay each frame should have. I use the setTimeout() function to add a delay to the animation.