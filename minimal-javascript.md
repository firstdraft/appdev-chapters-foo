# Minimal JavaScript for Rails Developers

## History

Oh, JavaScript:

 - whipped together at Netscape in 1995, back during the great Browser Wars
 - named "Java"Script to piggy-back on popularity of Java (despite having nothing to do with Java)
 - and, through some historical accident, won the battle to become the third standard language of the web, along with HTML (for structure) and CSS (for style).

As the only scripting language that browsers run natively, it has by default become one of the most widely used general-purpose programming languages; maybe _the_ most.

However, like CSS, it can't undo mistakes in the design of the language[^ten_days] very often; in order to maintain backwards compatibility.

Thankfully, also like CSS, JavaScript has made tremendous strides in the last 5-10 years in paving over the warts of the past with new features and getting them adopted across _most_ browsers so that it's quite nice to use nowadays.

[^ten_days]: The initial design of JavaScript was done in just 10 days. This was (sometimes painfully) obvious in the early days.

## The very basics

For the very basics of JavaScript, I recommend this Scrimba course: [Introduction to JavaScript](https://scrimba.com/learn/introtojavascript){:target="_blank"}. You should be able to watch it on 1.5x or 2x speed. Or, if you want to go even deeper first, then [Scrimba's JavaScript Bootcamp](https://scrimba.com/learn/javascript){:target="_blank"} is good and will cover concepts that we'll need in the future when we get to React. Go ahead, I'll wait.

---

---

---

Welcome back! What did you think of your first encounter with JavaScript?

### This ain't your first rodeo

First of all, compare your experience learning JavaScript for the first time to when you learned Ruby for the first time. How did it feel this time around to learn about variables, string interpolation, arrays, arguments, `split`, etc?

_So_ much better, right? This was, for me, one of the best things about learning Ruby.

After learning (the friendly, welcoming) Ruby and building some pragmatic, real-world applications in Rails, and through that getting a pretty good understanding of programming _concepts_ (variables, conditionals, loops, objects, methods, arguments, etc) — my second[^second_lang] language was _so much easier_, and the third was even easier still.

Conversely, every language has some distinctive characteristics about it that will change the way you _think_ and make you better at your previous languages. Welcome to being a polyglot programmer 🙌🏾 

[^second_lang]: This has hiring implications. _Really_ good developers can get up to speed on a new language pretty quickly (especially if it's a nice language like Ruby). If there are other developers on the team to answer questions about the codebase/framework while they are working on small introductory tasks, then it shouldn't be a dealbreaker that a strong developer has 0 years of experience in whatever stack you happen to be using, if they say they're willing to learn.

    Conversely, if a developer pigeonholes themselves as _just_ a Rails developer or _just_ a Node developer or _just_ a React developer, then that's a red flag; they probably aren't very strong. (My opinion.)

## A review of Ruby blocks

I'm going to give you another brief introduction to JavaScript in a moment, with a specific focus on what we're going to need for our objective: making our web apps interactive and _slick_.

But first, it will be helpful to make sure you understand the following exploration of Ruby Blocks. Read it carefully and [experiment with the concepts in a Ruby workspace](https://github.com/appdev-projects/base-ruby/generate){:target="blank"}; ask lots of questions. Ruby Blocks are directly analogous to JavaScript Callbacks, which we'll be using extensively soon.

### Defining methods that accept blocks

What if I wanted you to define a method called `benchmark` such that:

- I could send it some arbitrary code within a block.
- It would print some explanatory text and dashes.
- Then it would run the code I sent.
- Then it would print the amount of time that it took to execute the code I sent.
 
So, if I called the method like this:

```ruby
benchmark do
  puts "howdy!"
end
```

When run, the output of the program should look something like this:

```
==================================================
Starting benchmark.
--------------------------------------------------
howdy!
--------------------------------------------------
It took 4.6191e-05 seconds to run your code.
==================================================
```

Here's a more realistic example:

```ruby
sample_data = Array.new(10_000_000) { rand(100) }

# Benchmarking .each
benchmark do
  sample_data.each do |datum|
    datum * 2
  end
end

# Benchmarking while
benchmark do
  counter = 0

  while counter < sample_data.length
    sample_data[counter] * 2
    
    counter += 1
  end
end

# Benchmarking for
benchmark do
  for datum in sample_data do
    datum * 2 
  end
end
```

If we define the `benchmark` method properly, the output should look something like[^each_speed]:

[^each_speed]: As we can see, the three looping constructs perform quite similarly. Many students coming to Ruby from other languages ask whether `.each` is slower than `while`; the answer is no.

```
==================================================
Starting benchmark.
--------------------------------------------------
--------------------------------------------------
It took 0.344827695 seconds to run your code.
==================================================
==================================================
Starting benchmark.
--------------------------------------------------
--------------------------------------------------
It took 0.342456005 seconds to run your code.
==================================================
==================================================
Starting benchmark.
--------------------------------------------------
--------------------------------------------------
It took 0.340229314 seconds to run your code.
==================================================
```

Can you define the `benchmark` method? Go ahead, give it a try. I'll wait.

(It might be helpful to review [the `about_blocks.rb` Ruby Koan](https://github.com/appdev-projects/ruby-koans/blob/9a498bdc3f78cb1b13f7ba97235c5f6c2377f60d/about_blocks.rb){:target="_blank"}.)

```ruby
# Define the benchmark method here.

benchmark do
  puts "howdy!"
end
```

---

---

---

What we need to do here is define a method that is capable of receiving not just an argument, which we're used to doing with parentheses, but a **block**.

In Ruby, we actually don't have to do anything at all to our method in order to allow it to receive a block; if a block is provided by the user of the method, it will automatically be captured and we (the method authors) can invoke it with `yield`:

```ruby
def benchmark
  puts "=" * 50
  puts "Starting benchmark."
  puts "-" * 50

  start_time = Time.now
  
  yield

  end_time = Time.now

  elapsed_time = end_time - start_time

  puts "-" * 50
  puts "It took #{elapsed_time} seconds to run your code."
  puts "=" * 50
end

benchmark do
  puts "howdy!"
end
```

However, we can also define methods that [receive and name blocks explicitly](https://github.com/appdev-projects/ruby-koans/blob/9a498bdc3f78cb1b13f7ba97235c5f6c2377f60d/about_blocks.rb#L85){:target="_blank"} by treating the block like the last argument but prefixing it with an ampersand (`&`):

```ruby
def benchmark(&code_to_be_benchmarked)
  puts "=" * 50
  puts "Starting benchmark."
  puts "-" * 50

  start_time = Time.now
  
  code_to_be_benchmarked.call

  end_time = Time.now

  elapsed_time = end_time - start_time

  puts "-" * 50
  puts "It took #{elapsed_time} seconds to run your code."
  puts "=" * 50
end
```

The `.call` method is used to actually execute the code that is stored in the block, whenever and wherever we're ready to.

### Defining methods that accept blocks and arguments

Okay, what about if we want the method to accept both a block _and_ arguments?

For example, what if I wanted to provide a descriptive label for each benchmark, to make the output easier to understand?

```ruby
sample_data = Array.new(10_000_000) { rand(100) }

# Benchmarking .each
benchmark(".each") do
  sample_data.each do |datum|
    datum * 2
  end
end

# Benchmarking while
benchmark("while") do
  counter = 0

  while counter < sample_data.length
    sample_data[counter] * 2
    
    counter += 1
  end
end

# Benchmarking for
benchmark("for") do
  for datum in sample_data do
    datum * 2 
  end
end
```

And the output should be:

```
==================================================
Starting benchmark: '.each'
--------------------------------------------------
--------------------------------------------------
It took 0.339939834 seconds to run '.each'.
==================================================
==================================================
Starting benchmark: 'while'
--------------------------------------------------
--------------------------------------------------
It took 0.346698033 seconds to run 'while'.
==================================================
==================================================
Starting benchmark: 'for'
--------------------------------------------------
--------------------------------------------------
It took 0.380493103 seconds to run 'for'.
==================================================
```

Try upgrading the `benchmark` method to allow it to accept a label.

---

---

---

In order to allow our method to receive arguments as well, we need to move our block over and make sure it comes last:

```ruby
def benchmark(label, &code_to_be_benchmarked)
  puts "=" * 50
  puts "Starting benchmark: '#{label}'"
  puts "-" * 50

  start_time = Time.now
  
  code_to_be_benchmarked.call

  end_time = Time.now

  elapsed_time = end_time - start_time

  puts "-" * 50
  puts "It took #{elapsed_time} seconds to run '#{label}'."
  puts "=" * 50
end
```

Any other arguments can be passed in first and used as usual!

### Sending block variables back to the caller

This is a somewhat contrived example, but let's say for argument's sake that the caller of the `benchmark` method needs to know the time at which the measurement started. For example:

```ruby
benchmark("howdy") do |started_at|
  puts "howdy #{started_at}!"
end
```

Should produce this:

```
==================================================
Starting benchmark: 'howdy'
--------------------------------------------------
howdy 2022-04-26 17:58:41 +0000!
--------------------------------------------------
It took 3.116e-05 seconds to run 'howdy'.
==================================================
```

A bit contrived, but the point is: _What if the user of the method needs some information within their block that only the method can provide?_ That sounds like a job for a block variable!

Here's what the caller of the method would really like to do — make up a name for a block variable, say `edge`, and then use it within the block:

How do we as the authors of methods send information back to the caller of the method through block variables? How would you write the method now? Give it a try.

---

---

---

To send values back through block variables, we provide them as arguments to `call()` when we execute the block:

```ruby
def benchmark(label, &code_to_be_benchmarked)
  puts "=" * 50
  puts "Starting benchmark: '#{label}'"
  puts "-" * 50

  start_time = Time.now
  
  code_to_be_benchmarked.call(start_time)

  end_time = Time.now

  elapsed_time = end_time - start_time

  puts "-" * 50
  puts "It took #{elapsed_time} seconds to run '#{label}'."
  puts "=" * 50
end
```

The key bit: `code_to_be_benchmarked.call(start_time)`. This is where we're sending information that then becomes `started_at` or whatever name the caller makes up for the block variable.

And that's about all there is to know about Ruby blocks[^benchmark_library].

[^benchmark_library]: There is [an official Ruby benchmark library](https://github.com/ruby/benchmark){:target="_blank"}, as well as a whole bunch of third party options (like [Skylight.io for Rails apps](https://www.skylight.io/){:target="_blank"}), in case you ever want to do more in-depth measurements.

### Callbacks

Why have I spent all this time reviewing Ruby blocks during a lesson on JavaScript?  

Ruby blocks are an example of a general concept in computer programming known as **callbacks**. [From Wikipedia](https://en.wikipedia.org/wiki/Callback_(computer_programming)){:target="_blank"}:

> In computer programming, a callback, also known as a "call-after"[1] function, is any executable code that is passed as an argument to other code; that other code is expected to call back (execute) the argument at a given time.

Callbacks are extremely common — we've seen and used them many times before, and not just every time we used a Ruby block with `do`/`end`. Think about it:

 - From the name, it's obvious that [ActiveRecord Callbacks](https://guides.rubyonrails.org/active_record_callbacks.html){:target="_blank} are callbacks.
 - [The `dependent: destroy` option](https://guides.rubyonrails.org/association_basics.html#options-for-belongs-to-dependent){:target="_blank} and [the `counter_cache: true` option](https://guides.rubyonrails.org/association_basics.html#options-for-belongs-to){:target="_blank} are ready-made ActiveRecord callbacks.
 - [ActiveRecord validations](https://guides.rubyonrails.org/active_record_validations.html){:target="_blank} are a form of callbacks.
 - [`before_action` and `after_action` filters](https://guides.rubyonrails.org/action_controller_overview.html#filters){:target="_blank} in controllers are callbacks
 - Even controller actions themselves (code that we write in advance and give to `routes.rb` to run later when a user visits a URL) are callbacks! Most of our work all along has been writing callbacks, if you squint.

That said, JavaScript, and particularly the sort of JavaScript that we're going to be writing (to make our pages interactive) is _really_ callback-heavy.

That's because a lot of what we're going to want to do is attach **event handlers** to elements in our HTML that will wait for the user to perform some interaction (for example, click on something, or drag-and-drop something), and then it is supposed to spring to life and run the _callback_ we give it (`.call()` the block, in Ruby terms).

Okay, with that review of blocks under our belt, let's now, finally, take a look at JavaScript — from a Rails developer's perspective.

## JavaScript for Rails Developers

### Ruby -> JavaScript translations

First, go through the following Ruby statements and the roughly equivalent translation[^rosetta_stone] into JavaScript and see if they all make sense to you. If not, experiment with them. To experiment, create an HTML file, write your code within a `<script>` tag, open the file in Chrome, and look at the output in [the JavaScript console](https://developer.chrome.com/docs/devtools/console/javascript/){:target="_blank}.

If you don't have a [code editor](https://code.visualstudio.com/download) installed on your computer, you can use the same base-ruby Gitpod workspace that you were using to experiment with Ruby above. Follow these steps:

 - Create a Ruby file called `my_app.rb`.
 - Inside this Ruby file, add one line:

    ```ruby
    require 'sinatra'
    ```
 - Run your program with `ruby my_app.rb`.
 - Voilà! We've created a web app using [the framework Sinatra](https://www.devdungeon.com/content/ruby-sinatra-tutorial). Sinatra is a very lightweight framework, compared to Rails. It doesn't include ActiveRecord and a million other things that Rails does, but for simple request/responses, it's very elegant.
 - One thing that Sinatra shares with Rails is the convention that you can put static assets in `public/` and they will be automatically served. Create a folder called `public/` and a file within called `hello.html`.
 - Visit `/hello.html` in your applicatin preview. Click on the "Remote Explorer" icon in the left sidebar to open your preview, if you don't have it open already.
 - Now we can write our JavaScript within a `<script>` element and see the output in our Chrome Dev Tools Console.

[^rosetta_stone]: I find that a ["rosetta stone"](https://blog.britishmuseum.org/everything-you-ever-wanted-to-know-about-the-rosetta-stone/){:target="_blank} approach is very helpful when learning a new programming language.

Let's get started translating our Ruby knowledge into JavaScript.

#### Semicolon rule of thumb

Rule of thumb: put a semicolon at the end of every line that doesn't end in a curly.

#### Simple output

Ruby:

```ruby
p "howdy!"
```

JavaScript:

```js
console.log("howdy!");
```

#### Declaring local variables

Ruby:

```ruby
name = "Raghu"

p "howdy, #{name}!"
```

JavaScript:

```js
let name = "Raghu";

console.log(`howdy ${name}!`);
```

#### Defining and calling methods

Ruby:

```ruby
def greet
  puts "howdy!"
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
    
Note: in JavaScript, if you don't include the parentheses (even if there are no arguments), the function will not be executed; it will be referenced as an object (so that you can e.g. pass it as an argument to a method that takes a function as an input).

#### Methods that accept arguments

Ruby:

```ruby
def greet(name)
  puts "howdy, #{name}!"
end

greet("Raghu")
```

JavaScript:

```js
function greet(name) {
  console.log(`howdy, ${name}!`);
}

greet("Raghu");
```

#### Conditionals

Ruby:

```ruby
city = "Mumbai"

if city == "Chicago"
  puts "You live in the best city ever!"
elsif city == "Berlin"
  puts "You live in a great city!"
else
  puts "You live in a nice city."
end
```

JavaScript:

```js
let city = "Mumbai";

if (city === "Chicago") {
  console.log("You live in the best city ever!");
} else if (city === "Berlin") {
  console.log("You live in a great city!");
} else {
  console.log("You live in a nice city.");
}
```

Note: That was a triple ===, not a double ==. It's not the same as the Ruby triple ===.

Beware: There's also a JS double == (non-strict equivalence) operator. Look it up.

#### For loops

Ruby:

```ruby
for i in 2...6
  puts i * i
end
```

JavaScript:

```js
for (let i = 2; i < 6; i++) {
  console.log(i * i);
}
```

#### Methods that accept blocks of code

Ruby:

```ruby
def announce(&instructions)
  puts "********** DEAR PASSENGER **********"
  instructions.call
  puts "********** THANK YOU FOR FLYING ONE-WAY AIR **********"
end

announce do
  puts "Your flight is boarding in 5 minutes."
end
```

JavaScript:

```js
function announce(instructions) {
  console.log("********** DEAR PASSENGER **********");
  instructions();
  console.log("********** THANK YOU FOR FLYING ONE-WAY AIR **********");
}

announce(function() {
  console.log("Your flight is boarding in 5 minutes.");
});
```

#### Methods that accept arguments and blocks

Ruby:

```ruby
def announce(salutation, valediction, &instructions)
  puts "********** #{salutation} **********"
  instructions.call
  puts "********** #{valediction} **********"
end

announce("DEAR PASSENGER", "THANK YOU FOR FLYING ONE-WAY AIR") do
  puts "Your flight is boarding in 5 minutes."
end
```

JavaScript:

```js
function announce(salutation, valediction, instructions) {
  console.log(`********** ${salutation} **********`);
  instructions();
  console.log(`********** ${valediction} **********`);
}

announce("DEAR PASSENGER", "THANK YOU FOR FLYING ONE-WAY AIR", function() {
  console.log("Your flight is boarding in 5 minutes.");
});
```

#### Providing block variables

Ruby:

```ruby
def announce(&instructions)
  puts "********** DEAR PASSENGER **********"
  instructions.call("*")
  puts "********** THANK YOU FOR FLYING ONE-WAY AIR **********"
end

announce do |accent_character|
  puts "#{accent_character} Your flight is boarding in 5 minutes. #{accent_character}"
end
```

JavaScript:

```js
function announce(instructions) {
  console.log("********** DEAR PASSENGER **********");
  instructions("*");
  console.log("********** THANK YOU FOR FLYING ONE-WAY AIR **********");
}

announce(function(accentCharacter) {
  console.log(`${accentCharacter} Your flight is boarding in 5 minutes ${accentCharacter}`);
});
```

#### Methods with arguments, blocks, and block variables

Ruby:

```ruby
def announce(salutation, valediction, &instructions)
  puts "********** #{salutation} **********"
  instructions.call("*")
  puts "********** #{valediction} **********"
end

announce("DEAR PASSENGER", "THANK YOU FOR FLYING ONE-WAY AIR") do |accent_character|
  puts "#{accent_character} Your flight is boarding in 5 minutes. #{accent_character}"
end
```

JavaScript:

```js
function announce(salutation, valediction, instructions) {
  console.log("********** " + salutation + " **********");
  instructions("*");
  console.log("********** " + valediction + " **********");
}

announce("DEAR PASSENGER", "THANK YOU FOR FLYING ONE-WAY AIR", function(accentCharacter) {
  console.log(accentCharacter + " Your flight is boarding in 5 minutes. " + accentCharacter);
});
```

#### Arrays

Ruby:


```ruby
fruits = ["apples", "oranges", "bananas"]
puts fruits[1]
puts fruits.length
```

JavaScript:

```js
let fruits = ["apples", "oranges", "bananas"];
console.log(fruits[1]);
console.log(fruits.length);
```

#### Challenge

Translate the following Ruby into Javascript:

```ruby
def for_each_in(array, &instructions)
  for i in 0...array.length
    instructions.call(array[i])
  end
end

fruits = ["apples", "oranges", "bananas", "pears"]
for_each_in(fruits) do |f|
  puts "I like #{f}."
end
```

If you can do it, you're in great shape for what we want to do — adding interactivity to our apps with **A**synchronous **J**avaScript **A**nd **X**ML — Ajax[^ajaj]!

[^ajaj]: No one really uses XML for it anymore, but Ajax sounds much better than "Ajaj" (for JSON) or "Ajah" (for HTML), so we stuck with it 😉

## Manipulating HTML elements

JavaScript is okay, as far as languages go, but we were perfectly happy with Ruby. The only reason we're interested in JavaScript is that it has a unique ability: it can run inside the browser, and that means we can use it to modify HTML elements in our pages _without needing to refresh the page_. This is the key to making our apps feel like _apps_ and not pages.

Let's see how this works. In Chrome, open the JavaScript Console from the View > Developer menu. There, you have a REPL, much like `irb`, where you can type any JavaScript expression. (There's also great autocomplete functionality in the Chrome dev tools, so use <kbd>tab</kbd> often.)

Importantly, there is an object available, `document`, that represents the page itself:

```js
document
```

Let's try working with it:

```js
let headings = document.getElementsByTagName("h1");
```

We've created a variable, `headings`, and stored an array of all the `h1` elements on the page within it. Neat!

As you were typing, you might have noticed the autocomplete showing you other methods that were available — `getElementsByClassName`, `getElementByID`, etc. These are all ways that we can query the DOM (Document Object Model) and find HTML elements; exactly the way we did when we were writing CSS selectors.

Let's keep going and get just one heading out of the array:

```js
let h = headings[0];
```

Now that we have one element in the variable `h`, we can do things like:

 -  `h.innerText` (will return the text content of the element)
 -  `h.classList.add("display-1")` (adds a CSS class to the element)
 -  `h.remove()` (removes the element from the DOM)
 -  and a whole bunch more. Neat!

## jQuery

Nowadays, plain vanilla JavaScript is pretty nice to use; but before, say, 2015, it was quite a different story. The language itself was missing lots of features that we Rubyists take for granted, there were lots of cross-browser inconsistencies, and life was hard.

Sound familiar? It was the same story with CSS; with CSS, developers came together to share their solutions to rough edges and cross-browser inconsistencies with frameworks like Bootstrap. In the JavaScript world, the go-to library to make up for JavaScript's shortcomings was jQuery.

Nowadays, jQuery isn't absolutely essential to survival, the way it was for many years. Many developers have started to drop it and just use vanilla JavaScript, which does have some benefits in terms of performance/the amount of data users have to download.

However, I still use jQuery on almost every project and I recommend that start out with it too, because I'm not interested in dealing with the 1% of cases where there are still rough edges. Let's create a new HTML file and start to experiment with jQuery. [Here's a convenient CDN](https://code.jquery.com/){:target="_blank} we can use to pull it in:

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
```

### Add some elements

Let's get some HTML elements in our page to work with. (You can add the standard HTML boilerplate around it if you want to.)

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>

<h1>Cities</h1>

<ul id="cities_list">
  <li class="northeast">New York</li>
  <li class="west">Los Angeles</li>
  <li id="best" class="midwest">Chicago</li>
  <li class="south">Houston</li>
  <li class="west">Phoenix</li>
</ul>
```

### The jQuery function

jQuery is an incredibly useful library, and gives us access to a massive ecosystem of plugins; but basically, the way we use it starts out in just one way: by calling the `jQuery()` function[^official_docs].

[^official_docs]: Let me point out right away the [the official jQuery documentation](https://api.jquery.com/jquery/){:target="_blank} is quite good, so you should refer to it often.

The `jQuery()` function is sort of like the `document.getElementsByTag()`, `document.getElementsByClassName()`, `document.getElementByID()`, etc, functions that we met earlier — but all wrapped into one. You pass in any CSS selector (as a string) as an argument, and `jQuery()` will return an array of matching elements. Try this in the JS console:

```js
jQuery("li");
jQuery(".west");
jQuery("#best");
```

Since we're going to be using the `jQuery()` function _a lot_, they conveniently aliased it as `$()`, to save us a bunch of typing. So the above could also be shortened to:

```js
$("li");
$(".west");
$("#best");
```

### DOM manipulation with jQuery

Once we've queried the DOM for the elements we're interested in, jQuery provides many methods for manipulating them. Let's try putting an element in a variable:

```js
let x = $("#best");
```

Now, we can manipulate it:

```js
x.hide();
```

Poof! Let's bring it back:

```js
x.show();
```

Or, if we're not sure what state it's in (visible or invisible) to start with, we can toggle:

```js
x.toggle();
x.toggle();
x.toggle();
```

That's pretty abrupt, though. How about something a little smoother?

```js
x.hide();
x.fadeIn();
x.fadeOut();
x.fadeToggle();
```

Or even smoooooother:

```js
x.fadeToggle(5000);
```

### Creating elements with jQuery

You can also programmatically create elements using jQuery. Pass a string containing HTML directly to `$()`:

```js
let another_city = $("<li class='northeast'>Philadelphia</li>");
```

Then, you can add it to the DOM:

```
list = $("#cities_list");

list.append(another_city);
```

### Using callbacks

As I mentioned earlier, JavaScript is callback-heavy. Here's a simple example:

In the smoooooother example above, we had the element take 5 seconds to fade. What if we wanted to have something happen after the element faded out, but not until then?

No problem! `fadeToggle` (like most jQuery methods) accepts a callback that it will run once it completes:

```js
x.fadeToggle(5000, function() {
  alert("All done!");
});
```

Another common thing we'll do is bind **event handlers** to elements. Try the following:

```js
x.on("click", function() {
  $(".west").slideToggle();
});
```

Now, whenever `x` is clicked, elements with class `west` will slide up and down. Nice!

As you can see, we can use [the `on` method](https://api.jquery.com/on/){:target="_blank} to react to `"click"`s to any element; we're no longer constrained to users only clicking `<a>`s or `<button>`s. `"mouseover"` is another event that applies to almost any element.

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
 - [trigger()](https://api.jquery.com/trigger/){:target="_blank} (particularly useful with `"reset"` to clear all of the inputs in a form)
 - [focus()](https://api.jquery.com/focus/){:target="_blank}
 - [submit()](https://api.jquery.com/submit/){:target="_blank}

## jQuery plugins

Even if we just stopped here, you've already gained a lot of power, because jQuery has a whole ecosystem of plugins built around it. A lot of JavaScript library authors architected their projects as: "locate the element on your page with `$()`, call my function on it, and _poof_, it will turn into a chart/datepicker/calendar/carousel/etc".

For example, [here's a nice datepicker library](https://getdatepicker.com/5-4/Usage/){:target="blank"} that plays well with Bootstrap. There are _many_ other jQuery plugins out there that follow the same pattern.

You now also have full access to all of the goodies in Bootstrap, like [the Popover component](https://getbootstrap.com/docs/4.6/components/popovers/#example-enable-popovers-everywhere){:target="blank"}, which requires that you initialize it using jQuery (it doesn't automatically initialize for performance reasons).

## $(document).ready

Note that, if you use libraries like [the datepicker](https://getdatepicker.com/5-4/Usage/){:target="blank"} above, Google Maps, or any JS library that acts upon one of your HTML elements: you need to wait until the element that you want to call the method on has been loaded before it will work. Unlike CSS, JavaScript runs _asynchronously_ in the browser, so there's no guarantee that just because the `<script>` tag appears in the document after the element that the element will have been fully loaded in time.

To solve this problem, jQuery adds a `.ready` method[^ready_read_more] to the `$(document)` object that we can, you guessed it, provide a callback to. If we put all our code that binds event handlers to elements within this callback, it will execute only after the document has been fully loaded.

[^ready_read_more]: [Read more about `$(document).ready` here](https://learn.jquery.com/using-jquery-core/document-ready/){:target="_blank"}, if you're interested.

For example, to use the datepicker library referenced above, rather than just this:

```html
<script>
  $('#datetimepicker1').datetimepicker();
</script>
```

We should do something like the following:

```html
<script>
  $(document).ready(function() {
    $('#datetimepicker1').datetimepicker();
  });
</script>
```

## Turbolinks

### turbolinks:load

Rails, by default, includes a library called Turbolinks[^turbolinks_read_more] that actually has been doing some Ajax for us all along without us even knowing it. When users click on links, Turbolinks has been only replacing the `<body>` of the document, to make the application feel a bit snappier.

This, however, can mess with our jQuery, which is listening for `$(document).ready` (which only fires when a full page reload occurs) to initialize event handlers when users navigate to different pages. To solve this, we can use the `turbolinks:load` event instead:

[^turbolinks_read_more]: [Read more about Turbolinks here](https://github.com/turbolinks/turbolinks#installing-javascript-behavior){:target="_blank"}, if you're interested.

```js
$(document).on('turbolinks:load', function() {
  console.log("It works on each visit!")
})
```

### If your JavaScript libraries are acting funny, it's probably Turbolinks

If you pull in a 3rd-party JavaScript library (say, for example, Google Maps), and you notice some weird behavior, especially things that are resolved when you do a full page refresh: the issue is probably related to Turbolinks.

Try the `turbolinks:load` fix above. Or sometimes you have to do some other things, [as we did to fix the Bootstrap modal in Photogram Industrial](https://www.honeybadger.io/blog/turbolinks/){:target="_blank"}.

A common strategy is to [just remove Turbolinks](https://stackoverflow.com/questions/38649550/rails-how-to-disable-turbolinks-in-rails-5){:target="_blank"}; or when you're first creating your app with `rails new`, use the `--skip-turbolinks` option to never include it in the first place. Since we're about to add real Ajax to our application anyway, having the automatic sort-of-but-not-really-Ajax of Turbolinks becomes less helpful.

## Conclusion

And that, from the perspective of a Rails developer who wants to improve the UX of their web application, is all we _need_ to know about JavaScript — for the moment.

Now, we're ready to revamp the interactions in our UI. When someone clicks on a link or submits a form, in many cases (usually after an action that CRUDs some records in some table(s)) we end up redirecting them to the same URL that they were on before; but they wind up at the top of the page, losing their scroll position. Annoying!

Let's see if we can use our new JavaScript skills to improve this experience — with a technique called Ajax. We're going to:

 1. Change the default behavior of links and forms.
   
    When the user clicks on a link/form, we're going to keep them where they are instead of sending them to a different URL.
    
    We'll still make the same GET/PATCH/POST/DELETE request as before, to the same route and with the same parameters; but it will be in the background, using JavaScript.
 2. In the action triggered by the request, instead of responding with a `.html.erb` template or redirecting as usual, we'll **respond with a `.js.erb` template containing some jQuery**.
 3. The jQuery will run in the user's browser and update just the part of the page that needs it (sliding in the comment, updating the like count, etc).

Voilá! Ajax! That's coming up next.
