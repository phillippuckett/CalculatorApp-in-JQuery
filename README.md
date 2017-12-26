# jQuery Calculator
Following along with Josh Simon's 'Simple jQuery Calculator', searchable at ```https://codepen.io/simonja2/pen/QbGYbR```, 
I was able to create a fully functional algebraic calculator, using nothing more than jQuery, html, and css. 
It's a simple project, but having been out of the game for so long I needed some help getting back into the swing of things, thus the selected project. 
The following commentary will serve to break down Mr. Simon's code, for the purpose of instructing any person viewing this project, and looking to create an identical calculator.

Let's get started by moving into the 'index.html' file:
I could have coded everything into my html document, however I'm not a fan of overloading a single page with code, and try to keep things as clean/simple as possible. With that in mind I created a separate JS and CSS file for my project; linking the two files to my index.html page, proceeding to source the jQuery CDN, and then adding DIV's for styling purposes.

Moving on to the app.js file - where I utilized jQuery:
The bane of jQuery is the selector function (selector). Basically selectors in jQuery serve to manipulate html elements by using strings, and look like this ```$()```;
If you have questions about it, feel free to visit ```http://api.jquery.com```. 

Let's starts with our first selector,
```
    $(document).ready(function () {

    };
```
adding a number of variables that serve to give the input field some nice default placeholder zeroes (much like one would see when operating a calculator in reallife):
```
    $(document).ready(function () {
        var result = 0;
	    var prevEntry = 0;
	    var operation = null;
	    var currentEntry = '0';
	    updateScreen(result);
    };
```
Once we've established our default variables, we can go ahead and begin configuring the following: 
```C```, ```CE```, ```back```, ```+/-```, ```.```, ```%```, ```sqrt```, ```1/x```, ```pi```, and ```=```;
```
	$('.button').on('click', function (evt) {
		var buttonPressed = $(this).html();
		console.log(buttonPressed);

		if (buttonPressed === "C") {
			result = 0;
			currentEntry = '0';
		} else if (buttonPressed === "CE") {
			currentEntry = '0';
		} else if (buttonPressed === "back") {
			//currentEntry = currentEntry.substring(0, currentEntry.length-1);
		} else if (buttonPressed === "+/-") {
			currentEntry *= -1;
		} else if (buttonPressed === '.') {
			currentEntry += '.';
		} else if (isNumber(buttonPressed)) {
			if (currentEntry === '0') currentEntry = buttonPressed;
			else currentEntry = currentEntry + buttonPressed;
		} else if (isOperator(buttonPressed)) {
			prevEntry = parseFloat(currentEntry);
			operation = buttonPressed;
			currentEntry = '';
		} else if (buttonPressed === '%') {
			currentEntry = currentEntry / 100;
		} else if (buttonPressed === 'sqrt') {
			currentEntry = Math.sqrt(currentEntry);
		} else if (buttonPressed === '1/x') {
			currentEntry = 1 / currentEntry;
		} else if (buttonPressed === 'pi') {
			currentEntry = Math.PI;
		} else if (buttonPressed === '=') {
			currentEntry = operate(prevEntry, currentEntry, operation);
			operation = null;
		}

		updateScreen(currentEntry);
	});
```
 Now we are ready to add in our number buttons:
```
    updateScreen = function (displayValue) {
        var displayValue = displayValue.toString();
        $('.screen').html(displayValue.substring(0, 10));
    };

    isNumber = function (value) {
	    return !isNaN(value);
    };
```
and last but not least, our elementary arithmetic:
```
    isOperator = function (value) {
	    return value === '/' || value === '*' || value === '+' || value === '-';
    };

    operate = function (a, b, operation) {
	    a = parseFloat(a);
	    b = parseFloat(b);
	    console.log(a, b, operation);
	    if (operation === '+') return a + b;
	    if (operation === '-') return a - b;
	    if (operation === '*') return a * b;
	    if (operation === '/') return a / b;
    };
```
Once the last few steps are completed one should be able to start a live-server or local-server and being  plugging away numbers all day long - to their hearts content.