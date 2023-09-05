---
toc: true
comments: false
layout: post
title: Creating the Snake Game
description: This post goes over the steps I took to modify the Snake Game.
type: tangibles
courses: { blogs: {week: 2} }
---

## How I modified the Snake Game
- Custom snake colors
    - Alternating body color + Head color
    ```
    // Paint snake
            headDot(snake[0].x, snake[0].y);
            for(let i = 1; i < snake.length; i++){
                if (i % 2 !== 0) {
                    activeDotA(snake[i].x, snake[i].y);
                    continue;
                }
                activeDotB(snake[i].x, snake[i].y)
            }
    ```
- Custom background color
- Custom apple color