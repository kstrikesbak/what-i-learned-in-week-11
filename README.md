# **WHAT I LEARNED IN  WEEK 11** 
___

    It's Week 11. Time is flying 
    Tell JK I'm still Rowling. - Kejal

## `CodeWars`

### Welcome!
```javascript 
function greet(language) {
  let database = {english: 'Welcome',
czech: 'Vitejte',
danish: 'Velkomst',
dutch: 'Welkom',
estonian: 'Tere tulemast',
finnish: 'Tervetuloa',
flemish: 'Welgekomen',
french: 'Bienvenue',
german: 'Willkommen',
irish: 'Failte',
italian: 'Benvenuto',
latvian: 'Gaidits',
lithuanian: 'Laukiamas',
polish: 'Witamy',
spanish: 'Bienvenido',
swedish: 'Valkommen',
welsh: 'Croeso'};
  if (database[language] === undefined) {
    return database.english;
  } else {
    return database[language];
  }
}
```

### The office I boredom score
```javascript

```

## `object-stuff`

```javascript
function getFirstName(person) {
  return person.firstName
}

function getLastName(person) {
  return person.lastName
}

function getFullName(person) {
  return person.firstName + ' ' + person.lastName
}

function setFirstName(person, name) {
  return person.firstName = name
}

function setAge(person, age) {
  return person.age = age
}

function giveBirthday(person) {
  if (person.age === undefined) {
    return person.age = 1
  } else {
    person.age = person.age + 1
  }
}

function marry(person1, person2) {
  person1.married = true
  person2.married = true
  person1.spouseName = person2.firstName + ' ' + person2.lastName
  person2.spouseName = person1.firstName + ' ' + person1.lastName
}

function divorce(person1, person2) {
  person1.married = false
  person2.married = false
  delete person1.spouseName
  delete person2.spouseName
}
```



## `just-how-we-roll`
```javascript
/**********
 * DATA *
 **********/

const sixes = [];
const doubleSixes = [];
const twelves = [];
const twenties = [];


/*************************
 * RANDOM ROLL GENERATOR *
 *************************/


function getRandomNumber(max) {
    const rand = Math.random();
    const range = rand * max;
    const result = Math.ceil(range);
    
    return result;
}



/*******************
 * YOUR CODE BELOW *
 *******************/
let newD6 = document.querySelector('#d6-roll');
newD6.src = 'images/start/d6.png';
let newD12 = document.querySelector('#d12-roll');
newD12.src = 'images/start/d12.jpeg';
let newD20 = document.querySelector('#d20-roll');
newD20.src = 'images/start/d20.jpg';
let newD6Double = document.querySelector('#double-d6-roll-1');
newD6Double.src = 'images/start/d6.png';
let newD6Double2 = document.querySelector('#double-d6-roll-2');
newD6Double2.src = 'images/start/d6.png';

function changeD6RollPic (){
    let roll = getRandomNumber(6)
    // const newD6 = document.querySelector('#d6-roll')
    newD6.src = `./images/d6/${roll}.png`
    sixes.push(roll)
    document.querySelector('#d6-rolls-mean').innerText = mean(sixes).toFixed(2)
    document.querySelector('#d6-rolls-median').innerText = median(sixes).toFixed(2)
    document.querySelector('#d6-rolls-mode').innerText = mode(sixes)

    
}
// changeD6RollPic()

function changeDoubleD6RollPics (){
    let roll = getRandomNumber(6)
    let rollAgain = getRandomNumber(6)
    document.querySelector('#double-d6-roll-1').src=`./images/d6/${roll}.png`
    document.querySelector('#double-d6-roll-2').src=`./images/d6/${rollAgain}.png`
    doubleSixes.push(roll+rollAgain)
    document.querySelector('#double-d6-rolls-mean').innerText = mean(doubleSixes).toFixed(2)
    document.querySelector('#double-d6-rolls-median').innerText = median(doubleSixes).toFixed(2)
    document.querySelector('#d6-rolls-mode').innerText = mode(doubleSixes)
}

function changeD12RollPic (){
    let roll = getRandomNumber(12)
    document.querySelector('#d12-roll').src=`./images/numbers/${roll}.png`
    twelves.push(roll)
    document.querySelector('#d12-rolls-mean').innerText = mean(twelves).toFixed(2)
    document.querySelector('#d12-rolls-median').innerText = median(twelves).toFixed(2)
    document.querySelector('#d12-rolls-mode').innerText = mode(twelves)
}

function changeD20RollPic () {
    let roll = getRandomNumber(20)
    document.querySelector('#d20-roll').src=`./images/numbers/${roll}.png`
    twenties.push(roll)
    document.querySelector('#d20-rolls-mean').innerText = mean(twenties).toFixed(2)
    document.querySelector('#d20-rolls-median').innerText = median(twenties).toFixed(2)
    document.querySelector('#d20-rolls-mode').innerText = mode(twenties)
}


/*******************
 * EVENT LISTENERS *
 *******************/

const singleD6 = document.querySelector('#d6-roll')
singleD6.addEventListener('click',changeD6RollPic)
const doubleD6First = document.querySelector('#double-d6-roll-1')
doubleD6First.addEventListener('click',changeDoubleD6RollPics)
const doubleD6Second = document.querySelector('#double-d6-roll-2')
doubleD6Second.addEventListener('click',changeDoubleD6RollPics)
const d12 = document.querySelector('#d12-roll')
d12.addEventListener('click', changeD12RollPic)
const d20 = document.querySelector('#d20-roll')
d20.addEventListener('click', changeD20RollPic)



/****************
 * MATH SECTION *
 ****************/
function mean (arr) {
    let sum = 0 
    for (let i = 0 ; i < arr.length ; i++) {
        sum += arr[i]
    }
    return sum / arr.length
    
}

function median (arr) {
    let median = 0;
    arr.sort();
    if (arr.length % 2 === 0){
        median = (arr[arr.length / 2 -1] + arr[arr.length / 2]) / 2;
    } else {
    median = arr[(arr.length - 1) / 2];
}
return median;
}

function mode (rolls) {
    const counts = {};
    let highestCount = 0 ;
    let mode = 0 ;
    for (const currentRoll of rolls) {
        if (currentRoll in counts) {
            counts[currentRoll]++;
        } else {
            counts[currentRoll]=1;
        }
        
        if (counts[currentRoll]>highestCount) {
            highestCount = counts[currentRoll];
            mode = currentRoll;
        }
    }
    return mode
}


const reset1 = document.querySelector('#reset-button')
reset1.addEventListener('click',resetPage)
function resetPage() {
document.location.reload(true);
}
```
## `BS-Paint`

```javascript
const brush = document.querySelector('.current-brush')
const classes = brush.classList;
document.querySelector('#reset').addEventListener('click', resetEverything)
function resetEverything() {
    document.location.reload(true);
}
document.querySelector('.color-1').addEventListener('click', changeBrush)
function changeBrush() {
    classes.replace(classes[1] , 'color-1')
}
document.querySelector('.color-2').addEventListener('click', changeBrush1)
function changeBrush1() {
    classes.replace(classes[1], 'color-2')
}
document.querySelector('.color-3').addEventListener('click', changeBrush2)
function changeBrush2() {
    classes.replace(classes[1], 'color-3')
}
document.querySelector('.color-4').addEventListener('click', changeBrush3)
function changeBrush3() {
    classes.replace(classes[1], 'color-4')
}
document.querySelector('.color-5').addEventListener('click', changeBrush4)
function changeBrush4() {
    classes.replace(classes[1], 'color-5')
}
document.querySelector('.color-6').addEventListener('click', changeBrush5)
function changeBrush5() {
    classes.replace(classes[1], 'color-6')
}

const allSquares = document.querySelectorAll('.square')
let newSquares = Array.from(allSquares)
const squareClass =newSquares.classList
for (let i = 0; i < newSquares.length; i++) {
    newSquares[i].addEventListener("click", function(event) {
        newSquares[i].classList.replace(newSquares[i].classList[1], classes[1])
})
}
```
## `Transmogrify`
```javascript
const biggify = function(num) {
  return num + 9000
}

const nasafy = function(num) {
  let newArr = []
  for (let i=num; i>0; i--) {
    newArr.push(i)
  }
  newArr.push('Blast off!')
  return newArr

}

const reversify = function(str) {
  let newStr = ''
  for (let i = str.length-1 ; i>-1; i--) {
    newStr += str[i]
  }
  return newStr
}

const titleify = function(str) {
  let newStr = ''
  for (let i = 0 ; i<str.length; i++) {
    if (i===0) {
      newStr += str[i].toUpperCase()
    }
    else if (str[i]!==' ') {
      newStr +=str[i].toLowerCase()
    } else {
      newStr += ' ' + str[i+1].toUpperCase()
      i++
    }
  }
  return newStr
}

const crazify = function(str) {
  let newStr = ''
  let count = 0 
  for (let i = 0 ; i<str.length; i++) {
    if (str[i] === ' ' ) {
      newStr += ' '
    }
    else if (count % 2 === 0) {
      newStr += str[i].toLowerCase()
      count++
    } else  {
      newStr +=str[i].toUpperCase()
      count++
    }
  }
  return newStr 
}
```
## `all-about-that-text`

```javascript
const biggifyButton = document.querySelector('.biggify');
const nasafyButton = document.querySelector('.nasafy');
const crazifyButton = document.querySelector('.crazify');
const reversifyButton = document.querySelector('.reversify');
const titleifyButton = document.querySelector('.titleify');


const userInput = document.querySelector('.user-input');
const newLi = document.createElement('li');
const answer = document.querySelector('.result');


const buttonOne = function () {
    newLi.innerText = biggify((userInput.value)*1);
    answer.append(newLi);
}
const buttonTwo = function () {
    newLi.innerText = nasafy((userInput.value));
    answer.append(newLi);
}
const buttonThree = function () {
    newLi.innerText = crazify((userInput.value));
    answer.append(newLi);
}
const buttonFour = function () {
    newLi.innerText = reversify((userInput.value));
    answer.append(newLi);
}
const buttonFive = function () {
    newLi.innerText = titleify((userInput.value));
    answer.append(newLi);
}

biggifyButton.addEventListener('click', buttonOne);
nasafyButton.addEventListener('click', buttonTwo);
crazifyButton.addEventListener('click', buttonThree);
reversifyButton.addEventListener('click', buttonFour);
titleifyButton.addEventListener('click', buttonFive);
```
