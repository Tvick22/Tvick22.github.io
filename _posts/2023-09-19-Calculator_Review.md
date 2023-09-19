---
toc: true
comments: false
layout: post
title: Creating the Calculator
description: This post goes over the steps I took to modify the Calculator.
type: hacks
courses: { blogs: {week: 5} }
---

1. First I started changing the calculator by changing the style of the page
    - I styled the buttons and output area using DaisyUI
2. Next I added the square root function by adding a new operation that takes the first number and brings it to the power of (1/second number)
3. I also removed a line of code that was causing the operation to repeat twice
4. I also made sure the operation doesn't repeat more than one time when you press the = sign
    - On top of this I made it so you can continue to use an operation and it almost acts as an equal button.
    - I also fixed other errors that I found in the operation function and equal function
5. Then I added keybinds to make the calculator easier to use (1-9, and operations)
6. I also found an error that made the first number appear as a float, but be processed as an Integer because of the parseInt function instead of parseFloat