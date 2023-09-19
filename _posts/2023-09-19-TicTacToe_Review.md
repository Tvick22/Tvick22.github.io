---
toc: true
comments: false
layout: post
title: Creating Tic Tac Toe
description: This post goes over the steps I took to create a game of Tic Tac Toe.
courses: { blogs: {week: 5} }
---

1. First, I created the html and styled it with DaisyUI
    - I made a top bar that displays info
    - I added 9 tiles organized into 3 rows of 3 (for each tic tac toe square)
2. Next, I started to make functions for the game
    - I made a reset function that would clear the innerText of each tile
    - I made a change spot function that adds an "X" or "O" to the tile they choose
    - I made a win check function that checks if a player has won
3. I stored the board info in an object along with the turn and a method that alternates the turn from "X" to "O" or "O" to "X"
4. I used the functions to make the page interactive, so the user can play tic tac toe.