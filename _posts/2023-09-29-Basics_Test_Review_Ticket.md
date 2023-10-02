---
toc: true
comments: false
layout: post
title: Basics Test Review Ticket
description: Review of what I did for the Basics Test
type: tangibles
courses: { blogs: {week: 6} }
---

# HTML

```html
<div class="container">
    <div class="wrappertop">
        <p class="paragraph">p</p>
        <button class="greenButton" onclick="flipText()">button</button>
        <div class="floatingDivTop">div</div>
    </div>
    <div class="wrapperbtm">
        <div class="floatingDivBtm">div</div>
        <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ">
            <div class="link">a</div>
        </a>
        <a href="https://nighthawkcoders.github.io/teacher/basics/html">
            <div class="link">a</div>
        </a>
        <p class="paragraph">p</p>
    </div>
</div>
```
>- This is my HTML layout that follows the wireframe, and adds a few extra elements.

>- I have a div that wraps everything with the container class.

>- I have 2 other divs that act as wrappers for the button, paragraph, and a tags.

>- I have a paragraph and button on the top wrapper.

>- I have 2 links and a paragraph in the bottom wrapper.

>- Additionally, I added a 'floatingDiv' that labels the divs just like the picture showed.

```css
    .greenButton {
        position: relative;
        border: 3px solid #59ff00;
        background-color: #ffff;
        color: #59ff00;
        font-size: 24px;
        font-weight: bold;
        width: 33%;
        z-index: 10;
    }
    .greenButton:hover {
        position: relative;
        border: 3px outset #59ff00;
        background-color: #ffff;
        color: #59ff00;
        font-size: 24px;
        font-weight: bold;
        width: 33%;
        z-index: 10;
    }
    .greenButton:active {
        position: relative;
        border: 3px inset #59ff00;
        background-color: #ffff;
        color: #59ff00;
        font-size: 24px;
        font-weight: bold;
        width: 33%;
        z-index: 10;
    }
```

>- This is the CSS I made to edit the button
>- When you hover over it, the border is outset. When you click it, the border is inset. When you dont interact with it, the border is solid.

```js
    let factCount = 0;

    function flipText () {
        const paragraph = document.getElementsByClassName("paragraph")[0]
        if (factCount == animalFacts.length) {
            factCount = 0;
        }
        const randomFact = animalFacts[factCount]
        paragraph.innerText = randomFact;
        factCount++
        return;
    }
```

>- This function gets called when the button gets pressed.

>- animalFacts is an array of strings that contain random animal facts ChatGPT found for me

>- The function iterates to the next fact everytime it is called, and displays it on the paragraph. If the factCount (iterator) is equal to the length of animal facts, then it is on the last fact, and will be set back to 0. This enables it to infinitely loop through the array.

# Data Types

```js
const Trevor = {
    "name": "Trevor",
    "lastName": "Vick",
    "age": 16,
    "birthYear": 2007,
    "foodStorage": {
        "bananas": 5,
        "apples": 3,
        "waffles": 15,
        "mangos": 4,
        "pancakes": 14
    },
    "currentClasses": ["AP World History", "Math 3A", "Computer Science and Software Engineering", "Chemistry 1", "Spanish 4"],
    "interests": ["Hockey", "Lacrosse", "Programming"],
    "favoriteFoods": ["Pizza", "CheeseBurger", "Orange Chicken", "Filet Mignon"],
}
```

>- Here is part of the object I created with the required criteria along with apsects such as: a foodStorage that could represent how much stuff I have using a key value store, a birthyear that could be used to update my "age" attribute, and 3 arrays of simple information about me.

```js
updateAge () {
        const currYear = new Date().getFullYear();
        this.age = currYear-this.birthYear
        return this.age
    }
```

>- This is the first method I made for the Trevor Object. It uses Date().getFullYear() to grab the current year and subtract my birthyear to update my current age.

```js
changeClass (newClass, period) {
        if (!this.currentClasses[period-1]) {
            return console.warn(`Period ${period} does not exist (Accepts 1-5)`);
        }
        this.currentClasses[period-1] = newClass;
        return this.currentClasses;
    }
addInterest(newInterest) {
    const lowerCaseInterests = this.interests.map((interest) =>  interest.toLowerCase())
    if (lowerCaseInterests.includes(newInterest.toLowerCase())) {
        return console.warn("Interest already exists");
    }

    this.interests.push(newInterest);

    return this.interests;
}
```

>- These 2 methods of the Trevor Object let you add to the different arrays. changeClass() takes a new class and period to place the new class in a specific location of the Array based off of the period. addInterest() takes a new interest as a parameter and checks if the interest is already in the array, and then if it isn't, it adds it to the end of the array with .push().

```js
countAllFood() {
        const quantities = Object.values(this.foodStorage)
        let finalCount = 0;
        quantities.map((num) => {
            finalCount += num
        })
        return finalCount
    }
```

>- This method of the Trevor Object counts the total of all of the food in the foodStorage object. It starts by getting an array of just the quantities of each food object, and then uses .map() to iterate each food object and add it to the finalCount. Finally, it returns the final count of all the quantities added up.

>- Array.map() iterates through each object in the array, and performs a callback function on each object. In this case, I used (num) =>- {finalCount+= num} as my callback so it adds each number in the array to the finalCount.

# DOM

```js
let canFlip = true

function flipLinks () {
    if (!canFlip) {
        console.warn("Cannot Flip Yet")
        return;
    }
    canFlip = false;

    const href1 = document.getElementById("link1").getAttribute("href");
    const href2 = document.getElementById("link2").getAttribute("href");

    document.getElementById("link1").setAttribute("href", href2);
    document.getElementById("link2").setAttribute("href", href1);
    document.getElementById("paragraph").classList.add("switch")
    document.getElementById("paragraph").innerText = "switched!";
    
    setTimeout(() => {
        document.getElementById("paragraph").innerText = "p";
        document.getElementById("paragraph").classList.remove("switch")
        canFlip = true
        return;
    }, 1000)
    }
```

>- This is the function I used to flip the links and display "switched!" in the top p tag. I added a small color change animation to the paragraph as well when it is switched and a 1 second cooldown to the action.
>- The function works by checking if the canFlip varaible is true, then it sets it to false while it is working. It changes the links by grabing the href attribute of each one, and re-assigning them to the other other one. Next, it adds the switch class to the paragraph, so the CSS can change the color of it, and then it changes the text to say "switched!". After this it uses setTimeout() to add a 1000 milisecond delay to the action. After 1000 miliseconds, the callback function changes the paragraph back to normal, and sets canFlip back to true.

# Javascript

```js
function compareNumbers (a, b) {
    if (isNaN(a) || isNaN(b)) {
        return new Error("A and B must both be Numbers")
    }
    if (a > b) {
        return "a is greater";
    }

    if (b > a) {
        return "b is greater";
    }
    if (b == a) {
        return "both are equal";
    }
}
```

>- This function I made takes 2 numbers (a and b), checks if they are numbers, and performs a check to see which one is greater, or if the two are equal. I use isNaN() to check if the given parameters are numbers that can both be compared. Next, I compare each number using seperate if statements.

# Js Debugging

>- Work and explanation is shown [HERE]({{site.baseurl}}/basics/js-debug)

>- See *What I changed* Tab