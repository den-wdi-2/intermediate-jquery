<!---
title: Intermediate jQuery
type: lesson
duration: "1:25"
creator:
    name: Jim Clark
    city: LA
competencies: Front-end intro
--->

<!--HTML and typos just plaguing the class on this, only got halfway through by 11:30 -->

<!--Hook: Raise your hand if you have a car.  Keep your hand up if you know how to fill up the tank.  Keep your hand up if you know how to change your oil.  Keep your hand up if you know how to replace your transmission. Just like with cars, there are a lot of these stopping points in coding.  Nobdody knows everything.  Today, we're going to move up to and a little beyond the "oil changing point of jQuery".  So yeah, it might get messy.-->

<!--Make a point throughout this class to show the code that devs need on the projector, and remind them not to copy-paste from sources if they can avoid it. -->

<!--10:10 5 minutes-->

# Intermediate jQuery

### Objectives
*After this lesson, students will be able to:*
- **Describe** event bubbling, delegation and how to bind events with jQuery
- **Apply** jQuery to manipulate, add, and remove DOM elements
- **Add** event listeners for standard events - click, mouse, keydown - and custom events and respond with an action
- **Capture** data from specific events and iterate on or manipulate the data
- **Work** with timer events within the context of the browser

### Preparation
*Before this lesson, students should already be able to:*

- **Call** JavaScript/jQuery in your HTML file
- **Describe** jQuery and it's use in manipulating the DOM
- **Write** simple jQuery to manipulate the DOM

<!--10:15 15 minutes -->

## Page Setup - Codealong

#### Create Folder and Files

Welcome back to jQuery!  Since we've had a proper introduction, let's start building our own `index.html` page and `app.js` file. In Terminal:

- Navigate to your working directory where you keep your code
- Create a directory called `first_jquery`
- Navigate inside that directory
- `touch` your HTML file
- Make a `js` directory
- `touch` your JS file, and make sure it is inside your `js` directory
- Open the current directory with Sublime

#### Boilerplate

- Create your HTML boilerplate. 
- Include the jQuery library from a CDN and your `app.js` after it.  
 - **Hint**: You can Google "jQuery CDN" to find a good link.
- We'll also include the CDN of something called Bootstrap, a CSS framework that we will learn more about later, but for now, think of it as a whole bunch of CSS prewritten for us that we can use by calling it.  It's helpful now because it will make our simple demo easier on the eyes:

```html
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
```

<!--Make sure devs stop here -->

#### Starting HTML

<!--Demo this without copy-paste, and ask them to do the same -->

We are going to display a list of homes for sale in Longmont. Here's some HTML to get us started - replace the existing `<body>` tags with the following:
```html
<body class="container">

    <h1 class="jumbotron">Longmont Homes For Sale</h1>

    <table id="homes" class="table">
        <thead>
            <tr>
                <th>Address</th>
                <th>Sq. Ft.</th>
                <th>Bedrooms</th>
                <th>Baths</th>
                <th>Price</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>27374 Matterhorn Drive</td>
                <td>1,664</td>
                <td>3</td>
                <td>2</td>
                <td>$279,500</td>
                <td><button class="btn btn-xs btn-danger">Remove</button></td>
            </tr>
            <tr>
                <td>243 El Dorado</td>
                <td>4,900</td>
                <td>6</td>
                <td>6.5</td>
                <td>$990,000</td>
                <td><button class="btn btn-xs btn-danger">Remove</button></td>
            </tr>
        </tbody>
    </table>
	<br>
    <button id="addHome" class="btn btn-danger">Add Home</button>

</body>
```

#### Ensuring that the DOM is Ready

Since our script is in the `<head>`, it will be parsed before the DOM. If our code references any DOM elements, and since this is a jQuery lesson it most certainly will, we need to delay our code's execution until the DOM is built by the browser:

```js
$(document).ready(function() {
	alert("Everything is ready, let's do this");
	/* Javascript
	goes
	here */
});

// or, the shortcut version
$(function(){
	alert("Everything is ready, let's do this");
	/* Javascript
	goes
	here */	
});
```

We're all set to get started. In Sublime, right-click anywhere on `index.html` in the editor and select `Open in Browser`.

Your page should load and the alert should appear.

<!--10:30 5 minutes -->

<!--Half-mast -->

## Adding & Removing Classes - Demo

It looks like our designer styled our _Add Home_ button with Bootstrap's `btn-danger` class making it red. We know that the button should probably be a color other than red - let's make it green instead.

Change the button from red to green by removing the `btn-danger` class and adding the `btn-success` class with jQuery:

```js
$(function() {

    $('#addHome').removeClass('btn-danger').addClass('btn-success');

});
```
That's better!

## Add and Remove Classes - Independent Practice

Your turn! After you change the class to `btn-success`, add a class named "text-center" to the `<h1>` tag.

<!--10:35 10 minutes -->

## Creating and Modifying Elements - Codealong

jQuery makes creating new elements easy. Let's add an anchor tag (link) to our page that takes our users to Zillow's site.

The jQuery function isn't just for selecting elements - it can create them! Just give it a string holding the HTML:

```js
var $newLink = $( '<br><br><a id="zillowLink" href="http://www.zillow.com">Visit Zillow.com</a>' );
```

#### Adding the Element to the DOM

The `newLink` variable now holds our newly created element, however, we still need to add it to the page. One of the ways is to use the `appendTo()` method:

```js
newLink.appendTo('body');
```
`appendTo()` will insert the new elements at the end, but still inside of the specified element.

Other methods available include:

- `append()`
- `insertBefore()`
- `insertAfter()`
- `before()`
- `after()`
- `prepend()`
- `prependTo()`

We'll practice adding elements in a bit.

#### Check it Out

Refresh your page and there's the link!

The problem however is that the link takes us away from our page. Wouldn't it be better instead to open Zillow in another tab? We'll do that in the next section.

#### Modifying Attributes

jQuery makes it easy (that phrase never gets old) to modify the attributes of an element with the `attr()` method.

Lets use it to add a `target` attribute to our link:

```js
$('#zillowLink').attr( "target", "_blank" );
```

Nice!

We also can use the `removeAttr()` method to remove an attribute.

<!--Timer for 2 minutes -->

<!--Got to here ~11:30 -->

## Find the value of an attribute - Independent Practice

How do you think we would retrieve the value of an attribute?  Pair up, get on the web and find out, and then, `console.log` the value of the link's `href` attribute.

<!--10:45 10 minutes -->

## Adding Event Listeners - Codealong

When our shiny green _Add Home_ button is clicked, we want to add one of the homes from an array that we will preload with a few homes.

jQuery has several ways to add event listeners. We will look at a couple of them in this lesson.

Here is a straight-forward way to add an event listener to our _Add Home_ button:

```js
$('#addHome').click(function(evt){
	console.log(evt);
	console.log(this);
});
```

<!--CFU: Think-pair-share for below -->

Refresh the page and open the console to see what the `evt` argument (jQuery's _event_ object) passed in by jQuery looks like and what `this` is set to.

jQuery's _event_ object can come in handy, especially when listening to mouse events. It is this object for example that would make writing a drawing or paint application possible.

Here is an alternative syntax. This syntax is preferred because the syntax above actually calls this next version internally.

```js
$('#addHome').on('click', function() {
	console.log(this);
});
```

In all cases, note that if you don't need to use the _event_ argument, you don't have to include it.

[These docs](http://api.jquery.com/category/events/) have a complete list of event methods.

In order to stay on the topic of event listeners, we'll write the code to insert a home a bit later.

<!--10:55 5 minutes -->

#### Event Delegation - Intro

_Event delegation_ allows us to attach a single event listener to an element that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future.

This is possible courtesy of something known as _event bubbling_, implemented in all major browsers. With event bubbling, un-handled events "bubble up" the DOM until a listener for that type of event is found. If there is no listener, so be it.

Doesn't this sound like a perfect approach for our _Remove_ buttons on each home? One event listener, regardless of how many homes in our table?! One event listener for all of the current rows in our table now, and for ones that we add later?! Yes, thanks to event delegation!

We need to decide which ancestor element to use.<br>

> Note: Identify the ancestor elements of our `<tr>` tags with the button.

Any ancestor element would work, but as they say, closer is usually better.

Let's put the handler on our `<tbody>` tag.  Also, to see how it's done, we will use a named function instead of an anonymous one:

```js
$('#homes tbody').on('click', 'tr', removeHome);

function removeHome() {
    console.log(this);
}
```

<!-- Note: Discuss the differences about the way we used the `on()` method that made it perform event delegation. -->

<!--11:00 10 minutes -->

## More DOM practice - Codealong

### Removing Elements

If our users click on the _Remove_ button, we obviously want to remove that home's row from the table:

```js
function removeHome() {
	$(this).remove();
}
```

No, it can't be that easy!

#### Removing Elements "Gracefully"

Currently, the sudden disappearance of the home's row is a little harsh. jQuery has some nice built-in [effects](http://learn.jquery.com/effects/intro-to-effects/) to help us out:
<!-- Leave this up, so people aren't tempted to copy-and-paste
```js
function removeHome() {
	$(this).fadeOut(1000, function() {
		$(this).remove();
	});
}
```
-->

Much better!

## Traversing the DOM - Demo

jQuery has [several methods to traverse the DOM](https://api.jquery.com/category/traversing/). However, to complete the next exercise, we need to know about the `children()` method.

We can use the `children()` method to select direct children (vs. all descendants) of an element.

For example, if we wanted to set the color of the text of our _Address_ and _Price_ cells in the table header row blue and green respectively, we could do this:

```js
var cells = $('#homes thead tr').children();
cells.eq(0).css('color', 'blue');
cells.eq(4).css('color', 'green');
```

Note that the `children()` method can be passed in an additional selector string for further filtering.

<!--11:10 15 minutes -->

## Add New Homes - Independent Practice

Now for what would appear to be our biggest challenge. However, you've already seen everything you need to make this happen! jQuery's there for you.

First, create an array of new home data in your script:

- Create a blank array called `newHomes`
- Push a house object into it with
  - `address` propery of "123 Sesame Street", `sf` property of "1,234", `bedrooms` property of 3, `baths` property of 2, `price` property of "$280,000"
- Push another house object into it with
  - `address` propery of "345 Plaza Sesamo", `sf` property of "4,321", `bedrooms` property of 5, `baths` property of 3.5, `price` property of "$680,000"

- Use the home data to "fill" in the cells of newly created rows.
- It always helps to pseudocode (write the major coding steps in English).
- You can take a home from the beginning or end of the array - your call.

**Bonus**:

- If you have time, include a check for there being no more homes in the array to add and disable the _Add Home_ button.
- Add a button that, when clicked, restores all previously removed homes and appends them to the bottom of the table.
  - Hint: Take a look at the "Removing Elements" section in [these docs](http://learn.jquery.com/using-jquery-core/manipulating-elements/).

<!--11:25 5 minutes -->

## Conclusion

- Describe how the event delegation syntax differs from the standard event handler syntax.
- Explain how to ensure your jQuery doesn't run until after the DOM loads in the browser.

## Resources:

- [Manipulating Elements - jQuery Learning Center](http://learn.jquery.com/using-jquery-core/manipulating-elements/)
