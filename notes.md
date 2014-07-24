# Codeschool Javascript Path: Try Jquery

## Chapter 1: Introduction to jQuery

Listening for document ready

    jQuery(document).ready(function(){
        <code>
    });

Will only run this code once the DOM is "ready".

**Used in Lesson:**

[Devdocs: .text()][1]

Example: 

    //changing the text inside of the < span > tag:
    
    jQuery(document).ready(function() {
        $("span").text("$the ");
    });

#### 1.8. Include the jQuery Library
    <script src="jquery.min.js"></script>

#### 1.9. Include a Custom javascript File
    <script src="application.js"></script>
    
    
#### 1.10 Modifying Multiple Elements
    

 >1. First we find all elements we want to change on the page (e.g. < h2 >)
 >2. Then we call the `.text()` method on them passing in a string.

    
#### 1.11 ID Selector

    $("#id-name")

#### 1.12 Class Selector

    $(".class-name")
* * *
* * *

### Chapter 2: Traversing and Searching the DOM
* * *
### 2.1 Searching the DOM

#### 2.2 Descendant Selector

    //selecting (e.g.) all `<li>` items under parent `#destinations`

    $("#destinations li");

#### 2.3 Selecting Direct Children
    
    //selecting (e.g.) all direct children `<li>` under parent `#destinations`

    $("#destinations > li");
    
#### 2.4 Selecting Multiple Elements
    //selecting multiple elements
    
    $(".promo, #france");

#### 2.5 The First and Odd Pseudo Selectors
    //selecting only (e.g.) FIRST item in unordered list
    $("#destination li:first);
    
    //selecting only (e.g.) LAST item in unordered list
    $("#destination li:last);

If we have `<ul>` like this, index starts at 0:

    <ul id="destinations">
        <li>#0 Rome</li>
        <li>#1 Paris</li>
        <li>#2 London</li>
    </ul>

`:odd` selector selects middle item:

    $("#destinations li:odd"); // #1 Paris

#### 2.6 The :even Selector
`:even` selector selects first and last items:

    $("#destinations li:even"); // #0 Rome, #2 London

* * *

#### 2.7 Traversing the DOM
#### 2.8 Using find()
[Devdocs: .find()][2]

    $("#destinations li");

Filtering by traversing:

    $("#destinations").find("li");
    //  |----> selection |----> traversal
    
#### 2.9 Using first()
[Devdocs: .first()][3]

    $("li").first();
// Using traversal or filtering, select the first vacation li element from the list.
$("#vacations li").first()

#### 2.10 Using last()
[Devdocs: .last()][4]

    $("li").last();

#### 2.11 Using prev(), 2.12 Traversing Up, 2.13 Traversing Down

**Walking the DOM:**

[Devdocs: .next()][5]

>Get the immediately following sibling of each element in the set of matched elements. If a selector is provided, it retrieves the next sibling only if it matches that selector.

[Devdocs: .prev()][6]

 >Get the immediately preceding sibling of each element in the set of matched elements, optionally filtered by a selector.

[Devdocs: parent()][7]

> Get the parent of each element in the current set of matched elements, optionally filtered by a selector.

    <div id="tours-wrapper">
      <h1>Guided Tours</h1>
      <ul id="tours">
        <li class="usa">
          <h2>New York, New York</h2>
          <span class="details">$1,899 for 7 nights</span>
          <ul class="vote"><li><a href="#">↑</a></li><li><a href="#">↓</a></li></ul>
        </li>
        <li class="europe">
          <h2>Paris, France</h2>
          <span class="details">$2,499 for 7 nights</span>
          <ul class="vote"><li><a href="#">↑</a></li><li><a href="#">↓</a></li></ul>
        </li>
        <yes><li class="europe sale">
          <h2 class="featured">Madrid, Spain</h2>
          <span class="details">$1,577 for 5 nights</span>
        </li></yes>
        <li class="asia">
          <h2>Tokyo, Japan</h2>
          <span class="details">$1,999 for 5 nights</span>
          <ul class="vote"><li><a href="#">↑</a></li><li><a href="#">↓</a></li></ul>
        </li>
      </ul>
       
      <ul class="sorting">
        <li><a href="#">America</a></li>
        <li><a href="#">Europe</a></li>
        <li><a href="#">Asia</a></li>
      </ul>
    </div>
<br>

    $(".featured").parent()

Traversing **Down**:

[Devdocs: children()][8]
    

> Get the children of each element in the set of matched elements, optionally filtered by a selector.

<br>

    $('#tours > li')
    
    //is same as:
  
    $('#tours').children('li')

* * *
* * *
## Chapter 3: Working with the DOM

### 3.1 Manipulating the DOM
####3.2 Creating a DOM Node

    var exampleNode = $("<span>bla bla bla</span>");


####3.3 Adding to the DOM I
[Devdocs: .before()][9]    

 > Insert content, specified by the parameter, before each element in the set of matched elements.

    $(".book").before(iAmContentInSomeVar);

####3.4 Adding to the DOM II
[Devdocs: .append()][10]

>  Insert content, specified by the parameter, to the end of each element in the set of matched elements.
    
    $(".book").append(iAmContentInSomeVar);

####3.5 Removing From the DOM
[Devdocs: .remove()][11]
> Remove the set of matched elements from the DOM.
    
    $("button").remove();

***
### 3.6 Acting on Interaction
#### 3.7 Click Interaction
#### 3.8 Acting on Click

[Devdocs: .ready()][12]
>Specify a function to execute when the DOM is fully loaded.

[Devdocs: .on()][13]

> Attach an event handler function for one or more events to the selected elements.

[Devdocs: .click()][14]

> Bind an event handler to the "click" JavaScript event, or trigger that event on an element.

Appending some tag/Removing `<button>` from the DOM on click:

    $(document).ready(function() {
      $('button').on('click', function() {
        // run this function on click
        var tagTag = $('<div>Tag</div>');
        $('.someClass').append(tagTag);
        $('button').remove();
      });
    });

#### 3.9 On Page Load

> Wrapping all of our code with:

    $(document).ready(function() { 
        // our code block
    });
> ... will ensure that it won't run until the DOM has loaded.

***
### 3.10 Refactor Using Traversing
#### 3.11 Removing the Clicked Button

When we click on one of the buttons, it removes all buttons on the page. Instead, let's just remove the one button that was clicked by using `$(this)`.

    $(document).ready(function(){
    $("button").on("click", function(){
     /* | */     var message = $("<span>Call 1-555-jquery-air to book this tour</span>");
     /* | */     $(".usa").append(message);
     /* | */     // $("button").remove(); 
     /* |-----> */  $(this).remove();
        });
    });

#### 3.12 Relative Traversing I
[Devdocs: after()][15]
>  Insert content, specified by the parameter, after each element in the set of matched elements.

We want message to be added after the button we click on. Instead of appending the message to the .usa list, add it after the button that was clicked.

    $(document).ready(function(){
      $("button").on("click", function(){
        var message = $("<span>Call 1-555-jquery-air to book this tour</span>);
        $(this).after(message);
        $(this).remove();
        });
    });
#### 3.13 Relative Traversing II
#### 3.14 Relative Traversing III
[Devdocs: .closest()][16]
> For each element in the set, get the first element that matches the selector by testing the element itself and traversing up through its ancestors in the DOM tree.

(exercise example)

*Rather than clicking on the button to show the price, we've decided to allow travelers to click on the entire `<li>` element. Change the call to on to only target .tour elements. After that change, $(this) in the event handler will reference the clicked `<li>`. Let's update our code to still append the message at the bottom and use find to locate the button and remove it.*

    $(document).ready(function(){
  $(".tour").on("click", function(){
    var message = $("<span>Call 1-555-jquery-air to book this tour</span>");
    $(this).append(message);
    $(this).find("button").remove();
     });
    });



***
### 3.15 Traversing and Filtering
####  3.16 Fetching Data From the DOM I
[Devdocs: .data()][17]
>The HTML <data> Element links a given content with a machine-readable translation. If the content is time- or date-related, the <time> must be used.

####  3.17 Fetching Data From the DOM II
####  3.18 Refactoring
**Exercise:**
*We want to show this discount to the user in the message we show after the 'Book Now' button is clicked. Go ahead and change the content of message to Call 1-555-jquery-air for a $<discount> discount., and swap out <discount> for the discount price.*

**HTML:**

    <br>
    <div id="tours">
      <h1>Guided Tours</h1>
      <ul>
        <li class="usa tour" data-discount="299">
          <h2>New York, New York</h2>
          <span class="details">$1,899 for 7 nights</span>
          <button class="book">Book Now</button>
        </li>
        <li class="europe tour" data-discount="176">
          <h2>Paris, France</h2>
          <span class="details">$2,299 for 7 nights</span>
          <button class="book">Book Now</button>
        </li>
        <li class="asia tour" data-discount="349">
          <h2>Tokyo, Japan</h2>
          <span class="details">$3,799 for 7 nights</span>
          <button class="book">Book Now</button>
        </li>
      </ul>
    </div>
<br>
**JS:**

    $(document).ready(function(){
  $("button").on("click", function(){
    var discount = $(this).closest(".tour").data("discount");
    var message = $("<span>Call 1-555-jquery-air for a $" + discount + "discount.</span>");
    $(this).closest(".tour").append(message);
    $(this).remove();
        });
    });
    

####  3.19 Better On Handlers
If we want to only target (e.g.)`<button>` elements within a certain tag/class/ID we need to refactor the on handler.

FROM:

      $("#someID").on("click", function(){...

TO:
    
      $("#someID").on("click", 'button', function(){...

Now we are ONLY targeting `<button>` that is inside `#someID`.

####  3.20 New Filter I
####  3.21 New Filter II

[Devdocs: addClass()][18]
> Adds the specified class(es) to each of the set of matched elements.

[Devdocs: .filter()][19]

> Reduce the set of matched elements to those that match the selector or pass the function's test.

Example: *When we click on the button with class .on-sale within #filters -> find all tours that are on-sale*

    $(document).ready(function(){
  $("#filters").on("click", ".on-sale", function(){
    	$('.tour').filter('.on-sale').addClass('highlight');
        });
    });
    
####  3.22 New Filter III
[Devdocs: .removeClass()][20]

> Remove a single class, multiple classes, or all classes from each element in the set of matched elements.

In last example if we want to remove `.highlight` class immediately after clicking a filter so we are only highlighting the correct elements we need to add:

    $(document).ready(function(){ 
  $("#filters").on("click", ".on-sale", function(){
    $(".highligh").removeClass("highlight");
    $(".tour").filter(".featured").addClass("highlight");
        });
    });

***
***
## 4.Listening to DOM Events

### 4.1 On DOM Load

#### 4.2 On Load I
#### 4.3 On Load II
#### 4.4 Slide Effect I
[Devdocs: .slideDown()][21]
> .slideDown() will display the matched element with a sliding motion

    $(document).ready(function() { 
    $("#tour").on("click", "button", function() { 
    
        /* .slideDown() will display the matched element with a sliding motion */
  
        $(".photos").slideDown("slow", function() {});
        });
    });




#### 4.5 Slide Effect II

[Devdocs: .slideToggle()][22]
>  Display or hide the matched elements with a sliding motion.

    $(document).ready(function() { 
    $("#tour").on("click", "button", function() { 
    $(".photos").slideToggle();
        });
    });

### 4.6 Expanding on on()
#### 4.7 Mouseover I
[Devdocs: .mouseenter()][23]

> Bind an event handler to be fired when the mouse enters an element, or trigger that handler on an element.
    
    $(document).ready(function() {
    $("#tour").on("click", "button", function() { 
    $(".photos").slideToggle(); 
        });
    
        $("#tour").on("mouseenter", "li", function () { 
        console.log("testiram"); 
        });
    });


#### 4.8 Mouseover II
*In our new mouseenter event handler, call slideToggle on the span tag within the picture description. You'll need to traverse down from the current element, the li, and find the span tag.*

    $(document).ready(function() {
  $("#tour").on("click", "button", function() {
    $(".photos").slideToggle();
    });
  $(".photos").on("mouseenter", "li", function() {
    //traversing from the current element li to span that tag below li
    $(this).find("span").slideToggle();
        });
    });

#### 4.9 Mouseleave
[Devdocs: .mouseleave()][24]

    $(document).ready(function() {
      $("#tour").on("click", "button", function() {
        $(".photos").slideToggle();
      });
      $(".photos").on("mouseenter", "li", function() {
        $(this).find("span").slideToggle();
      });
      $(".photos").on("mouseleave", "li", function() {
        $(this).find("span").slideToggle();
      });
    });

>Bind an event handler to be fired when the mouse leaves an element, or trigger that handler on an element.
#### 4.10 Named Functions

> Refactoring functions above:

    function showPhotos() {
    $(this).find("span").slideToggle();
    }

    $(document).ready(function() {
    $("#tour").on("click", "button", function() {
    $(".photos").slideToggle();
    });
  
    $(".photos").on("mouseenter", "li", showPhotos);
    $(".photos").on("mouseleave", "li", showPhotos);
    });



* * *
###4.11 Keyboard Events
[Devdocs: .val()][25]
>Get the current value of the first element in the set of matched elements or set the value of every matched element.

#### 4.12 Keyup Event

[Devdocs: .keyup()][26]
>Bind an event handler to the "keyup" JavaScript event, or trigger that event on an element.

#### 4.13 Keyup Event Handler I
>Within our event handler, update the number of nights in the #nights-count element to whatever the traveler entered in the #nights form field.

    $(document).ready(function() {
    $("#nights").on("keyup", function() {
        $("#nights-count").text($(this).val());
        });
    });



#### 4.14 Keyup Event Handler II
> Example: Set the content of the #total element to the number the traveler has entered into the form field multiplied by the daily price.



    $(document).ready(function() {
        $("#nights").on("keyup", function() {
        var nights = +$(this).val();
        var dailyPrice = +$(this).closest(".tour").data("daily-price");
         $("#total").text(nights * dailyPrice);
         $("#nights-count").text($(this).val());
         });
    });
#### 4.15 Another Event Handler

[Devdocs: .focus()][27]
>Description: Bind an event handler to the "focus" JavaScript event, or trigger that event on an element.

<br>
> Example: Let's write another event handler for the form field that will be run when the focus event is triggered. When this occurs, set the number of #nights to 7.

    $("#nights").on("focus", function() {
      $(this).val(7);
    });



* * *
### 4.16 Link Layover
#### 4.17 Link Events I
#### 4.18 Link Events II

> When this link is clicked, show the photos for the clicked tour by traversing to it using closest and find then sliding it down by using slideToggle.

    $(document).ready(function() {
  $(".see-photos").on("click", function() {
	console.log("kliknuto na link");
    $(this).closest(".tour").find(".photos").slideToggle();
    });
    });

<br>

    <div id="all-tours" class="links">
      <h1>Guided Tours</h1>
      <ul>
        <li class="tour usa" data-discount="199">
          <h2>New York, New York</h2>
          <span class="details">$1,899 for 7 nights</span>
          <button class="book">Book Now</button>
          <a href="#" class="see-photos">See Photos</a>
          <ul class="photos">
            <li>
              <img src="/assets/photos/paris1.jpg">
              <span>Arc de Triomphe</span>
            </li>
            <li>
              <img src="/assets/photos/paris2.jpg">
              <span>The Eiffel Tower</span>
            </li>
            <li>
              <img src="/assets/photos/paris3.jpg">
              <span>Notre Dame de Paris</span>
            </li>
          </ul>
        </li>
        <li class="tour france" data-discount="99">
          <h2>Paris, France</h2>
          <span class="details">$1,499 for 5 nights</span>
          <button class="book">Book Now</button>
          <a href="#" class="see-photos">See Photos</a>
          <ul class="photos">
            <li>
              <img src="/assets/photos/paris1.jpg">
              <span>Arc de Triomphe</span>
            </li>
            <li>
              <img src="/assets/photos/paris2.jpg">
              <span>The Eiffel Tower</span>
            </li>
            <li>
              <img src="/assets/photos/paris3.jpg">
              <span>Notre Dame de Paris</span>
            </li>
          </ul>
        </li>
        <li class="tour uk" data-discount="149">
          <h2>London, UK</h2>
          <span class="details">$2,199 for 5 nights</span>
          <button class="book">Book Now</button>
          <a href="#" class="see-photos">See Photos</a>
          <ul class="photos">
            <li>
              <img src="/assets/photos/paris1.jpg">
              <span>Arc de Triomphe</span>
            </li>
            <li>
              <img src="/assets/photos/paris2.jpg">
              <span>The Eiffel Tower</span>
            </li>
            <li>
              <img src="/assets/photos/paris3.jpg">
              <span>Notre Dame de Paris</span>
            </li>
          </ul>
        </li>
      </ul>
    </div>       



#### 4.19 Event Parameter I
#### 4.20 Event Parameter II
[Devdocs: event.stopPropagation()][28]
[Devdocs: event.preventDefault()][29]

> Example: Change event handler method to take in a link event and prevent the other event handler from being called + preventing the browser doesn't jump to the top of the page when the link is clicked as well.



    $(document).ready(function() {
  $(".see-photos").on("click", function(event) {
    event.stopPropagation();
    event.preventDefault();
    $(this).closest(".tour").find(".photos").slideToggle();
  });
  $(".tour").on("click", function() {
    alert("This should not be called");
    });
    });

* * *
* * *

## 5. Styling
###5.1 Taming CSS
#### 5.2 CSS I
#### 5.3 CSS II
#### 5.4 Show Photo
#### 5.5 Refactoring to CSS
* * *
###5.6 Animation
#### 5.7 Animate I
#### 5.8 Animate II
#### 5.9 Animation Speed
#### 5.10 Animate III
* * *

  [1]: http://devdocs.io/jquery/text
  [2]: http://devdocs.io/jquery/find
  [3]: http://devdocs.io/jquery/first
  [4]: http://devdocs.io/jquery/last
  [5]: http://devdocs.io/jquery/next
  [6]: http://devdocs.io/jquery/prev
  [7]: http://devdocs.io/jquery/parent
  [8]: http://devdocs.io/jquery/children
  [9]: http://devdocs.io/jquery/before
  [10]: http://devdocs.io/jquery/append
  [11]: http://devdocs.io/jquery/remove
  [12]: http://devdocs.io/jquery/ready
  [13]: http://devdocs.io/jquery/on
  [14]: http://devdocs.io/jquery/click
  [15]: http://devdocs.io/jquery/after
  [16]: http://devdocs.io/jquery/closest
  [17]: http://devdocs.io/html/data
  [18]: http://devdocs.io/jquery/addclass
  [19]: http://devdocs.io/jquery/filter
  [20]: http://devdocs.io/jquery/removeclass
  [21]: http://devdocs.io/jquery/slidedown
  [22]: http://devdocs.io/jquery/slidetoggle
  [23]: http://devdocs.io/jquery/mouseenter
  [24]: http://devdocs.io/jquery/mouseleave
  [25]: http://devdocs.io/jquery/val
  [26]: http://devdocs.io/jquery/keyup
  [27]: http://devdocs.io/jquery/focus
  [28]: http://devdocs.io/jquery/event.stoppropagation
  [29]: http://devdocs.io/jquery/event.preventdefault