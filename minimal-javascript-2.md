# JavaScript: The Slimmest Guide

There's an old meme about JavaScript:

![](/assets/minimal-js-2-definitive-vs-good.png)

_JavaScript: The Definitive Guide_ is 1096 pages long, and (from the same publisher) _JavaScript: The Good Parts_ is 176 pages long.[^joke]

[^joke]: The joke, back in the day, was about the large amount of cruft in the language that no one liked. Fortunately, the situation is much improved nowadays.

The _JavaScript: The Slimmest Guide_ on this page is even smaller than _JavaScript: The Good Parts_. This is the tiniest introduction that I could come up with to get you ready to do what we want to do: make our Rails apps snappy, such that every click doesn't require a full page reload.

## Ruby → JavaScript translations

The good news is that Ruby and JavaScript are quite similar! Basics like numbers, strings, arrays, math operators (`+`, `-`, `*`, `\`, `%`, `**`), and the `receiver.message` syntax for calling methods on objects are the same.

There are differences, however. Go through the following Ruby statements and the roughly equivalent translations[^rosetta_stone] into JavaScript. Experiment with them as you read.

[^rosetta_stone]: I find that a ["rosetta stone"](https://blog.britishmuseum.org/everything-you-ever-wanted-to-know-about-the-rosetta-stone/){:target="_blank"} approach is very helpful when learning a new programming language.

### Setup

- [Some starter code for this project is here.](https://github.com/appdev-projects/minimal-js)
- `bin/server`
- The homepage has some starter HTML. Find it in `app/views/misc/home.html.erb`.
- To experiment with the JavaScript expressions below:
    - You can open the JavaScript Console from Chrome's View > Developer menu. There, you have a REPL, much like `irb` or `rails console`, where you can type any JavaScript expression and execute it immediately.
    - For longer programs, you can write JavaScript within the `<script>` element on the page and then refresh it to execute.

### Note on semicolons

Unlike Ruby, but like many languages (like CSS), JavaScript uses semicolons to separate lines/expressions:

Ruby:

```ruby
p "howdy"
p "world"
```

JavaScript:

```js
console.log("howdy");
console.log("world");
```

Nowadays, JavaScript can automatically insert semicolons in most cases. So the following will also work:

```js
console.log("howdy")
console.log("world")
```

But this doesn't work in _all_ cases — just 99% of them. For now, in order to avoid confusing issues, my rule of thumb is to put a semicolon at the end of every line that doesn't end in a curly bracket.

With that out of the way, let's see and experiment with some Ruby expressions and their JavaScript equivalents. Wherever feasible, try typing out the JavaScript into a `<script>` tag or into the JavaScript console, rather than copy-pasting. Develop some muscle memory.

### Translations

#### Simple debugging output

Ruby:

```ruby
p "howdy!"
```

JavaScript:

```js
console.log("howdy!");
```

#### String interpolation

Ruby:

```ruby
"Your lucky number is #{7 * 6}"
# => "Your lucky number is 42"
```

JavaScript:

```js
`Your lucky number is ${7 * 6}`
// => Your lucky number is 42
```

Use backticks instead of double-quotes to create the string, and then use `${}` to interpolate instead of `#{}`.

#### Creating local variables

Ruby:

```ruby
name = "Alice"

p "howdy, #{name}!"

name = "Bob"

p "hi, #{name}!"
```

JavaScript:

```js
let name = "Alice";

console.log(`howdy ${name}!`);

name = "Bob";

console.log(`hi ${name}!`);
```

Difference: use `let` when creating the variable for the first time.

#### Declaring constants

Ruby:

```ruby
PI = 3.14
```

JavaScript:

```js
const pi = 3.14;
```

Difference: In Ruby, constants are `ALL_CAPS`. In JavaScript, the are lowercase like variables, but we use the `const` keyword to create them instead of `let`.

In Ruby, we use constants over variables when we want to indicate to people reading the code that "this value will never change". However, Ruby itself allows you to update constants if you want:

```ruby
PI = 3.14
PI = 3
# => works fine
```

So there's no real functional difference between constants and variables in Ruby.

However, in JavaScript, attempting to replace the value in a constant will result in an error:

```js
const pi = 3.14;
pi = 3;
// Uncaught TypeError: Assignment to constant variable.
```

#### Multi-word variable/method naming

Ruby:

```ruby
a_really_long_variable_name = 42
```

JavaScript:

```js
let aReallyLongVariableName = 42;
```

Difference: In Ruby we prefer to snake_case when we want to indicate word separation within a single identifier. JavaScript prefers [lowerCamelCase](https://en.wikipedia.org/wiki/Camel_case).

Both languages support either style; it's just a matter of community preference/taste.

#### Defining and calling methods

Ruby:

```ruby
def greet
  p "howdy!"
end

greet
```

JavaScript:

```js
function greet() {
  console.log("howdy!");
}

greet();
```
    
Difference: In JavaScript, if you don't include the parentheses (even if there are no arguments), the function will not be executed; it will be referenced as an object (so that you can e.g. pass it as an argument to a method that takes a function as an input).

#### Methods that accept arguments

Ruby:

```ruby
def greet(name)
  p "howdy, #{name}!"
end

greet("Alice")
```

JavaScript:

```js
function greet(name) {
  console.log(`howdy, ${name}!`);
}

greet("Alice");
```

#### Increment a value

Ruby:

```ruby
x = 5
x += 1
# x is now 6
```

JavaScript:

```js
let x = 5;
x++
# x is now 6
```

#### For loops

Ruby:

```ruby
for i in 2...6
  p i * i
end
```

JavaScript:

```js
for (let i = 2; i < 6; i++) {
  console.log(i * i);
}
```

#### Arrays

Ruby:

```ruby
fruits = ["apples", "oranges", "bananas"]
p fruits[1]
p fruits.length
```

JavaScript:

```js
let fruits = ["apples", "oranges", "bananas"];
console.log(fruits[1]);
console.log(fruits.length);
```

#### Methods that accept blocks of code

Ruby:

```ruby
fruits = ["apples", "oranges", "cherries"]

fruits.each do |fruit|
  p "I love #{fruit}!"
end
```

JavaScript:

```js
let fruits = ["apples", "oranges", "cherries"];

fruits.forEach(function(fruit) {
  console.log(`I love ${fruit}!`);
});
```

Difference: In Ruby we use `do` to start a block and `end` to close it. In JavaScript, we use `function() {` to start a block and `}` to close it. In JavaScript, these are called "anonymous functions" rather than "blocks".

If the method provides values for block variables, in Ruby we name them within optional "pipes" `| |` after the `do`. In JavaScript, we name them within the parentheses `( )` (which are not optional) after `function`.

In JavaScript, when you provide an anonymous function as an argument to another function, they are referred to as "callback functions". Just as we use blocks a lot in Ruby, we use callbacks _a ton_ in JavaScript.

#### Random numbers

For a random decimal greater than or equal to `0` and less than `1`:

Ruby:

```ruby
win_probability = rand
```

JavaScript:

```js
let win_probability = Math.random();
```

For a random integer:

Ruby:

```ruby
dice_roll = rand(6)
```

JavaScript:

```js
let dice_roll = Math.floor(Math.random() * 6);
```

`Math.floor()` rounds a number down, so the above code will return an integer between 0 and 5.

#### Conditionals

Ruby:

```ruby
MOVES = ["rock", "paper", "scissors"]

computer_move = MOVES.sample

p "The computer played #{computer_move}."

if computer_move == "rock"
  p "You tied."
elsif computer_move == "paper"
  p "You lost."
else
  p "You won."
end
```

JavaScript:

```js
const moves = ["rock", "paper", "scissors"];

let random_index = Math.floor(Math.random() * 3);

let computer_move = moves[random_index];

console.log(`The computer played ${computer_move}.`);

if (computer_move === "rock") {
  console.log("You tied.");
} else if (computer_move === "paper") {
  console.log("You lost.");
} else {
  console.log("You won.");
}
```

Note: The comparisons use triple `===,` not double `==`.

Beware: There's also a JS double `==` (non-strict equivalence) operator. In most cases, you should use `===`.

The other comparison operators work as you would expect in Ruby (`!=`, `<`, `<=`, `>`, `>=`).

### Challenge

Try writing fizz buzz in JavaScript:

For the numbers 1 through 100, print "fizz" if the number is a multiple of 3, "buzz" if the number is a multiple of 5, and "fizzbuzz" if the number is a multiple of both.

Your output in the JavaScript console should look something like this:

```
1
2
fizz
4
buzz
fizz
7
8
fizz
buzz
11
fizz
13
14
fizzbuzz
16
17
fizz
19
buzz

// etc ...

89
fizzbuzz
91
92
fizz
94
buzz
fizz
97
98
fizz
buzz
```

If you can do this challenge, you're in great shape!

## Manipulating HTML elements

JavaScript is okay, as far as languages go, but we were perfectly happy with Ruby. The only reason we're interested in JavaScript is that it has a unique ability: the browser can execute it directly, and that means we can use it to modify HTML elements in our pages _without needing to refresh the page_. This is the key to making our apps feel like _apps_ and not pages.

Let's see how this works. Visit the homepage of our app, which contains the following code at the moment:

```html
<h1>Cities</h1>

<ul id="cities">
  <li id="aus" class="south">Austin</li>
  <li id="bos" class="east">Boston</li>
  <li id="ord" class="midwest">Chicago</li>
  <li id="lax" class="west">Los Angeles</li>
  <li id="jfk" class="east">New York</li>
  <li id="sfo" class="west">San Francisco</li>
</ul>
```

In Chrome, open the JavaScript Console from the View > Developer menu. There, you have a REPL, much like `irb` or `rails console`, where you can type any JavaScript expression. (There's also great autocomplete functionality in the Chrome dev tools, so you can use <kbd>tab</kbd> often.)

Importantly, there is an object available, `document`, that represents the page itself:

```js
document
```

### Query by tag

Type the following into the JavaScript Console:

```js
let items = document.getElementsByTagName("li")

items
```

We've created a variable, `items`, and stored an array of all the `li` elements on the page within it. Neat!

As you were typing, you might have noticed the autocomplete showing you other methods that were available — `getElementsByClassName`, `getElementByID`, etc. These are all ways that we can query [the DOM (Document Object Model)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) and find HTML elements; exactly the way we did when we were writing CSS selectors.

### Query by id

Let's assign the list item representing Chicago to a variable `chi`:

```js
let chi = document.getElementById("ord");
```

Now that we have an element in the variable `chi`, we can retrieve its text with the `innerText` property:

```js
chi.innerText;
```

### Manipulate DOM

Crucially, we can _modify_ the element:

 -  `chi.style.backgroundColor = "green"` (sets a CSS property value for the element)
 -  `chi.remove()` (removes the element from the DOM)

Poof! Let's put it back in the DOM, but at the end of the list:

```js
list = document.getElementById("cities_list");

list.append(chi)
```

### Query by class

Let's add a blue border around the cities in the east:

```js
eastItems = document.getElementsByClassName("east");

eastItems.style.border = "thin blue solid";
```

Oops! This errors out with `Uncaught TypeError: Cannot set properties of undefined (setting 'border')`. That is because `eastItems` currently contains an _array_ of elements, not an individual element; and an array doesn't respond to `style`.

So, we'll have to get the elements out one by one and then set the property:

```js
eastItems[0].style.border = "thin blue solid";

eastItems[1].style.border = "thin blue solid";
```

That would be quite tedious if there were a hundred items, so let's use a loop instead:

```js
for (let i = 0; i < eastItems.length; i++) {
  eastItems[i].style.border = "thin red solid";
}
```

### Add new elements

We can also [create new elements](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) and add them to the DOM. Let's construct an item for Denver and then insert it at the beginning of our list:

```js
let den = document.createElement("li")

let den_text = document.createTextNode("Denver")

den.append(den_text)

den.style.backgroundColor = "orange"

den.className = "west"

den.id = "den"

list.prepend(den)
```

Great! So: with JavaScript, we can manipulate the DOM _after_ the page renders. This opens up a world of possibilities.

## jQuery

Nowadays, plain vanilla JavaScript is pretty nice to use; but before, say, 2015, it was quite a different story. The language itself was missing lots of features that we Rubyists take for granted, there were many cross-browser inconsistencies, and life was hard.

Sound familiar? It was the same story with CSS; with CSS, developers came together to share their solutions to rough edges and cross-browser inconsistencies with frameworks like Bootstrap. In the JavaScript world, the go-to library to paper over JavaScript's inconsistencies was jQuery.

Nowadays, jQuery isn't absolutely essential to survival, the way it was for many years. Many developers, especially the developers of libraries like Bootstrap, have started to remove it and just use vanilla JavaScript, which does have some benefits in terms of performance/the amount of data users have to download.

However, I still use jQuery on almost every project. I recommend that you start out with it too, because as beginners, we're not interested in grappling with the harder, "purer" way of doing things right now. We just want to get productive quickly.

So: let's experiment with jQuery. [Here's a convenient CDN](https://code.jquery.com/){:target="_blank} we can use to pull it in. Add the following line to your HTML document:

```html
<script src="https://code.jquery.com/jquery-3.6.1.min.js"></script>
```

And refresh the page.

### The jQuery function

jQuery is an incredibly useful library, and gives us access to a massive ecosystem of plugins; but basically, the way we use it starts out in just one way: by calling the `jQuery()` function[^official_docs].

[^official_docs]: Let me point out right away the [the official jQuery documentation](https://api.jquery.com/jquery/){:target="_blank} is quite good, so you should refer to it often.

The `jQuery()` function is sort of like the `document.getElementsByTag()`, `document.getElementsByClassName()`, `document.getElementByID()`, etc, functions that we met earlier — but all wrapped into one. You pass in any CSS selector (as a string) as an argument, and `jQuery()` will return an array of matching elements. Try this in the JS console:

```js
jQuery("li");

jQuery(".west");

jQuery("#ord");
```

Since we're going to be using the `jQuery()` function _a lot_, they conveniently aliased it as `$()`, to save us a bunch of typing. So the above could also be shortened to:

```js
$("li");

$(".west");

$("#best");
```

Once we've queried the DOM for the elements we're interested in, jQuery provides many methods for manipulating them. Let's try putting an element in a variable:

```js
let chi = $("#ord");
```

Since we obtained `chi` from the jQuery function, it is now a jQuery object, which means it has different methods from the objects returned by the vanilla `getElementById()`, etc, methods.

You can get its inner text with the `text()` function:

```js
chi.text();
```

Note that if you tried `chi.text`, it would return the function itself; not the actual text. In JavaScript, you have to execute the function explicitly by adding the parentheses, even if there are no arguments. (I forget to do this approximately 82 times per day.)

### DOM manipulation with jQuery

Let's do what we did before in vanilla JS: set Chicago's `background-color` to `green`:

```js
chi.css("background-color", "green");
```

Any CSS property/value pair can be set with the `css()` function.

And, just as before, we can remove it:

```js
chi.remove();
```

And add it back to the end of the list:

```js
list = $("#cities_list");

list.append(chi);
```

Let's add a border to the cities in the east:

```js
$(".east").css("border", "thin blue solid");
```

Ah ha! Notice that we didn't have to write the loop ourselves this time; jQuery takes care of it for us.

### Adding elements

To create a new element, we can pass a string containing the HTML directly to the `$()` function, which is much more convenient than using `createElement` and then adding content and attributes one by one:

```js
let den = $('<li id="den" class="west">Denver</li>');
```

Much better. Remember to use single quotes to create the string, or alternatively to [escape the inner double quotes](https://bobbyhadz.com/blog/javascript-escape-quotes-in-string){:target="_blank"}.

Now, we can add the new item to the list:

```js
list.append(den);
```

### jQuery bonuses

Sometimes we want to hide an element, but not remove it entirely from the DOM. For that, jQuery provides the convenient `hide()` method:

```js
chi.hide();
```

Poof! Let's bring it back:

```js
chi.show();
```

Or, if we're not sure what state it's in (visible or invisible) to start with, we can toggle:

```js
chi.toggle();

chi.toggle();

chi.toggle();
```

That's pretty abrupt, though. How about something a little smoother?

```js
chi.hide();

chi.fadeIn();

chi.fadeOut();

chi.fadeToggle();

chi.fadeToggle();

chi.fadeToggle();
```

Or even smoooooother:

```js
chi.fadeToggle(5000);
```

### Using callbacks

As I mentioned earlier, JavaScript is callback-heavy. Here's a simple example:

In the smoooooother example above, we had the element take 5 seconds to fade. What if we want to remove the element after it's faded out?

Try this:

```js
chi.fadeToggle(5000);
chi.remove();
```

You'll see that the element is removed _before_ the fade completes (when we reload the page, we barely even see the element at all before it is removed). 

What if we wanted to have something happen after the element faded out, but not until then? No problem! `fadeToggle` (like most jQuery methods) accepts a callback that it will run once it completes:

```js
chi.fadeToggle(5000, function() {
  alert("All done!");
});
```

So now we can remove at the right time:

```js
chi.fadeToggle(5000, function() {
  chi.remove();
});
```

Slightly more idiomatic would be to use the `this` keyword (which is _sorta_ like Ruby's `self`) so that our callback is not dependent on variable names defined outside of it:

```js
chi.fadeToggle(5000, function() {
  this.remove();
});
```

### Event handlers with on()

Another common thing we'll do is bind **event handlers** to elements. Try the following:

Add the following to the HTML:

```html
<div id="bye">Click me</div>
```

Now let's add a "click handler" to our new div that will toggle the western cities:

```js
$("body").on("click", "#bye", function() {
  $(".west").slideToggle();
});
```

This is saying: "Within `<body>`, find elements with an id of `bye`, and when they are clicked run the following callback." Now, whenever the div is clicked, elements with class `west` will slide up and down. Nice!

As you can see, we can use [the `on` method](https://api.jquery.com/on/){:target="_blank} to react to `"click"`s to any element; we're no longer constrained to users only clicking `<a>`s or `<button>`s.

Examples of events that apply to only certain kinds of elements are `"change"` (for `<select>`s), `"keydown"` (for `<input>`s), and `"submit"` (for forms).

### Frequently used jQuery methods

If you look at the left sidebar of [the jQuery docs](https://api.jquery.com/){:target="_blank}, you'll see they nicely organize methods by category:

 - [Effects](https://api.jquery.com/category/effects/){:target="_blank}
 - DOM [Manipulation](https://api.jquery.com/category/manipulation/){:target="_blank}
    -  [Insertion Around](https://api.jquery.com/category/manipulation/dom-insertion-around/){:target="_blank}
    -  [Insertion Inside](https://api.jquery.com/category/manipulation/dom-insertion-inside/){:target="_blank}
    -  [Insertion Outside](https://api.jquery.com/category/manipulation/dom-insertion-outside/){:target="_blank}
    -  [Removal](https://api.jquery.com/category/manipulation/dom-removal/){:target="_blank}
    -  [Replacement](https://api.jquery.com/category/manipulation/dom-replacement/){:target="_blank}
 - [CSS](https://api.jquery.com/category/css/){:target="_blank}

It's worth looking through the docs for what you need; but usually, you can Google "jQuery how to ＿＿＿＿" and have pretty good success. E.g., "jquery how to add an element as the last child".

Here are the jQuery methods that I wind up using most frequently. Read about and experiment with them. If you need to, refresh the page to reset the state of the elements:

 - [hide()](https://api.jquery.com/hide/){:target="_blank}
 - [show()](https://api.jquery.com/show/){:target="_blank}
 - [toggle()](https://api.jquery.com/toggle/){:target="_blank}
 - [slideUp()](https://api.jquery.com/slideUp/){:target="_blank}
 - [slideDown()](https://api.jquery.com/slideDown/){:target="_blank}
 - [fadeToggle()](https://api.jquery.com/fadeToggle/){:target="_blank}
 - [remove()](https://api.jquery.com/remove/){:target="_blank}
 - [append()](https://api.jquery.com/append/){:target="_blank}
 - [prepend()](https://api.jquery.com/prepend/){:target="_blank}
 - [before()](https://api.jquery.com/before/){:target="_blank}
 - [after()](https://api.jquery.com/after/){:target="_blank}
 - [replaceWith()](https://api.jquery.com/replaceWith/){:target="_blank}
 - [html()](https://api.jquery.com/html/){:target="_blank}
 - [addClass()](https://api.jquery.com/addClass/){:target="_blank}
 - [removeClass()](https://api.jquery.com/removeClass/){:target="_blank}
 - [val()](https://api.jquery.com/val/){:target="_blank}
 - [trigger()](https://api.jquery.com/trigger/){:target="_blank} (particularly useful with `"reset"` to clear all of the inp in a form)
 - [focus()](https://api.jquery.com/focus/){:target="_blank}
 - [submit()](https://api.jquery.com/submit/){:target="_blank}

## $(document).ready

Note that if you're using, for example, the Google Maps JS library, or any JS library that acts upon one of your HTML elements: you need to wait until the element that you want to call the method on has been loaded before it will work.

Unlike CSS, JavaScript runs _asynchronously_ in the browser, so there's no guarantee that just because the `<script>` tag appears in the document after the element that the element will have been fully loaded in time for the code within the `<script>` to affect it.

To solve this problem, jQuery adds a `.ready` method[^ready_read_more] to the `$(document)` object that we can, you guessed it, provide a callback to. If we put all our code that binds event handlers to elements within this callback, it will execute only after the document has been fully loaded.

[^ready_read_more]: [Read more about `$(document).ready` here](https://learn.jquery.com/using-jquery-core/document-ready/){:target="_blank"}, if you're interested.

For example, to attach click handlers reliably, instead of this:

```html
<script>
  $("#zebra").on("click", ".giraffe", function() {
    console.log("clicked!");
  });
</script>
```

We should do something like the following:

```html
<script>
  $(document).ready(function() {
    $("#zebra").on("click", ".giraffe", function() {
      console.log("clicked!");
    });
  });
</script>
```



## Conclusion

And that, from the perspective of a Rails developer who wants to improve the UX of their web application, is all we _need_ to know about JavaScript — for the moment[^polyglot].

[^polyglot]: Sidenote: Compare your experience learning JavaScript for the first time to when you learned Ruby for the first time. How did it feel this time around to learn about variables, string interpolation, arrays, arguments, etc?

    _So_ much better, right? This was, for me, one of the best things about learning Ruby.

    After learning (the friendly, welcoming) Ruby and building some pragmatic, real-world applications in Rails, and through that getting a pretty good understanding of programming _concepts_ (variables, conditionals, loops, objects, methods, arguments, etc) — my second[^second_lang] language was _so much easier_, and the third was even easier still.

    Conversely, every language has some distinctive characteristics about it that will change the way you _think_ and make you better at your previous languages. Welcome to being a polyglot programmer 🙌🏾 

    This has hiring implications. _Really_ good developers can get up to speed on a new language pretty quickly (especially if it's a friendly language like Ruby). If there are other developers on the team to answer questions about the codebase/framework while they are working on small introductory tasks, then it shouldn't be a dealbreaker that a strong developer has 0 years of experience in a stack, if they say they're willing to learn.

Now, we're ready to revamp the interactions in our UI. When someone clicks on a link or submits a form, in many cases (usually after an action that CRUDs some records in some table(s)) we end up redirecting them to the same URL that they were on before; but they wind up at the top of the page, losing their scroll position. Annoying!

Let's see if we can use our new JavaScript skills to improve this experience — with a technique called **A**synchronous **J**avaScript **A**nd **X**ML — Ajax[^ajaj]. That's coming up next. 

[^ajaj]: No one really uses XML for it anymore, but Ajax sounds much better than "Ajaj" (for JSON) or "Ajah" (for HTML), so we stuck with it 😉
