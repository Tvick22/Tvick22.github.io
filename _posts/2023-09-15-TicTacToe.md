---
toc: true
comments: false
layout: post
title: Tic Tac Toe
description: Simple game of Tic Tac Toe
type: tangibles
courses: { blogs: {week: 4} }
---

<button class="btn btn-primary" onclick="resetBoard()">Reset</button>

<div id="turn" class="grid h-20 card bg-base-300 rounded-box place-items-center text-5xl mb-2 bg-accent">X</div>

<div id="board" class="grid grid-cols-3 grid-rows-3 pb-4">
    <button id="1" class="btn btn-outline btn-primary h-48 text-5xl" onClick="changeSpot(1)"></button>  
    <button id="2" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(2)"></button>  
    <button id="3" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(3)"></button>  

    <button id="4" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(4)"></button>  
    <button id="5" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(5)"></button>  
    <button id="6" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(6)"></button>  

    <button id="7" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(7)"></button>  
    <button id="8" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(8)"></button>  
    <button id="9" class="btn btn-outline btn-primary h-full text-5xl" onClick="changeSpot(9)"></button>  
</div>

<script>
const Board = {
  1: document.getElementById("1"),
  2: document.getElementById("2"),
  3: document.getElementById("3"),
  4: document.getElementById("4"),
  5: document.getElementById("5"),
  6: document.getElementById("6"),
  7: document.getElementById("7"),
  8: document.getElementById("8"),
  9: document.getElementById("9"),
  "canChange": true,
  "turn": "X",
  alternateTurn() {
    if (this.turn == "X") {
      this.turn = "O" 
      document.getElementById("turn").innerText = "O"
      return;
    }
    this.turn = "X"
    document.getElementById("turn").innerText = "X"
    return;
  }
}

function resetBoard() {
  for (const [key, spot] of Object.entries(Board)) {
    if (isNaN(key)) continue;

    spot.innerText = ""
    spot.classList.add("btn-outline")
  }
  Board.turn = "X";
  document.getElementById("turn").innerText = "X";
  Board.canChange = true;
};

function changeSpot(spot) {
  if (!Board.canChange) return;
  if (Board[spot].innerText == "") {
    Board[spot].innerText = Board.turn
    checkForWin()
    return;
  }
  return;
}

function checkForWin () {
  if (Board[1].innerText === Board.turn && Board[2].innerText === Board.turn  && Board[3].innerText === Board.turn) {
    Board[1].classList.remove("btn-outline")
    Board[2].classList.remove("btn-outline")
    Board[3].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[4].innerText === Board.turn && Board[5].innerText === Board.turn  && Board[6].innerText === Board.turn) {
    Board[4].classList.remove("btn-outline")
    Board[5].classList.remove("btn-outline")
    Board[6].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[7].innerText === Board.turn && Board[8].innerText === Board.turn  && Board[9].innerText === Board.turn) {
    Board[7].classList.remove("btn-outline")
    Board[8].classList.remove("btn-outline")
    Board[9].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[1].innerText === Board.turn && Board[4].innerText === Board.turn  && Board[7].innerText === Board.turn) {
    Board[1].classList.remove("btn-outline")
    Board[4].classList.remove("btn-outline")
    Board[7].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[2].innerText === Board.turn && Board[5].innerText === Board.turn  && Board[8].innerText === Board.turn) {
    Board[2].classList.remove("btn-outline")
    Board[5].classList.remove("btn-outline")
    Board[8].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[3].innerText === Board.turn && Board[6].innerText === Board.turn  && Board[9].innerText === Board.turn) {
    Board[3].classList.remove("btn-outline")
    Board[6].classList.remove("btn-outline")
    Board[9].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[1].innerText === Board.turn && Board[5].innerText === Board.turn  && Board[9].innerText === Board.turn) {
    Board[1].classList.remove("btn-outline")
    Board[5].classList.remove("btn-outline")
    Board[9].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  if (Board[3].innerText === Board.turn && Board[5].innerText === Board.turn  && Board[7].innerText === Board.turn) {
    Board[3].classList.remove("btn-outline")
    Board[5].classList.remove("btn-outline")
    Board[7].classList.remove("btn-outline")
    document.getElementById("turn").innerText = `${Board.turn} Wins!!`
    Board.canChange = false
    return;
  }
  for (const [key, spot] of Object.entries(Board)) {
    if (isNaN(key)) continue;
    if (spot.innerText == "") {
      Board.alternateTurn()
      return;
    }
  }
  document.getElementById("turn").innerText = `TIE`
  Board.canChange = false
}

</script>