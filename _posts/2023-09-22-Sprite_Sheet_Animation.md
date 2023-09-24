---
toc: true
comments: false
layout: post
title: Sprite Sheet
description: Sprite Sheet Animation - control with WASD
type: tangibles
courses: { blogs: { week: 5 } }
---

<body>
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
</body>


<script>
    // start on page load
    window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        const sprite = document.getElementById("sprite")
        const SPRITE_WIDTH = 64;  // matches sprite pixel width
        const SPRITE_HEIGHT = 64; // matches sprite pixel height
        const SCALE_FACTOR = 1.5;  // control size of sprite on canvas
        const FRAME_LIMIT = 9;  // number of frames per row, this code assume each row is same
        let SPRITE_SPEED = 100 // delay between each frame (miliseconds)

        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;
        canvas.x = 100
        class Dog {
            constructor() {
                this.image = document.getElementById("skeletonSprite");
                this.spriteWidth = SPRITE_WIDTH;
                this.spriteHeight = SPRITE_HEIGHT;
                this.width = this.spriteWidth;
                this.height = this.spriteHeight;
                this.x = 0;
                this.y = 0;
                this.scale = SCALE_FACTOR;
                this.minFrame = 0;
                this.maxFrame = FRAME_LIMIT-1;
                this.frameX = 0;
                this.frameY = 0;
            }

            // draw dog object
            draw(context) {
                context.drawImage(
                    this.image,
                    this.frameX * this.spriteWidth,
                    this.frameY * this.spriteHeight,
                    this.spriteWidth,
                    this.spriteHeight,
                    this.x,
                    this.y,
                    this.width * this.scale,
                    this.height * this.scale
                );
            }

            // update frameX of object
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }

        // dog object
        const dog = new Dog();

        // update frameY of dog object, action from idle, bark, walk radio control
        function changeAnimation(input) {
            switch (input) {
                    case 'up':
                        dog.frameY = 0;
                        break;
                    case 'left':
                        dog.frameY = 1;
                        break;
                    case 'down':
                        dog.frameY = 2;
                        break;
                    case 'right':
                        dog.frameY = 3;
                        break;
                    default:
                        break;
                }
        }

        const validKeys = {
            "w": "up",
            "a": "left",
            "s": "down",
            "d": "right",
        }
        document.addEventListener("keypress", (event) => {
            if (!Object.keys(validKeys).includes(event.key)) {
                return;
            }
            changeAnimation(validKeys[event.key])   
        })

        // Animation recursive control function
        function animate(timeStamp) {
            // Clears the canvas to remove the previous frame.
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            // Draws the current frame of the sprite.
            dog.draw(ctx);
            // Updates the `frameX` property to prepare for the next frame in the sprite sheet.
            dog.update();
            SPRITE_SPEED = 100 - document.getElementById("speed").value
            // Uses `requestAnimationFrame` to synchronize the animation loop with the display's refresh rate,
            // ensuring smooth visuals.
            setTimeout(() => {requestAnimationFrame(animate);}, SPRITE_SPEED);
            
        }

        // run 1st animate
        animate();
    });
</script>