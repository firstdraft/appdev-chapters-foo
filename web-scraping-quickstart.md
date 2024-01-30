# Web Scraping

Add this to your `Gemfile` and run `bundle install` in the Terminal.

```ruby
gem "http"
```

You can follow along in the `rails console`.

### Step 1

Choose a URL with the data you want on it. For this example, let’s pick `chapters.firstdraft.com`.

```ruby
url = "https://chapters.firstdraft.com/chapters/753"
```
    
### Step 2

Make a request to that URL and save the result in a variable.

```ruby
webpage = HTTP.get(url)
```

The result of our request is a `Response` object.
There is a LOT of data that the browser can return when we request a page. For web scraping purposes, we only care about the visible content of the page. To get that, we use the `body` method.

```ruby
p webpage.body.to_s
```

This should return something like:

```shell
=> "<!DOCTYPE html>\n<html>\n  <head>\n    <title>README.md | firstdraft Chapters</title>\n    <meta name=\"csrf-param\" content=\"authenticity_token\" />..."
```  

Now we have a big String that has all the HTML elements on the page. But as we know from reading from an API, searching through a String is a pain! It’d be a lot nicer if we could convert it to an Array or a Hash or some other Ruby structure so we could search through it easier.

### Step 3

Similar to parsing the JSON of an API, we next need to parse the page’s HTML.

```ruby
parsed_page = Nokogiri::HTML(webpage.body.to_s)

p parsed_page
```

[Nokogiri](https://github.com/sparklemotion/nokogiri) is a gem that all Rails apps have and can parse HTML into a structured Ruby object. Now we have the page data in a structured format! It’s not an Array or a Hash, but it is a Ruby object that has methods we can use to better search through HTML, which is all that matters.

Next, how do we select the specific parts of the page to get the data from?

### Step 4

We need to use CSS selectors to pick which elements we want to grab from the page.

Let’s say I want to select all the links in a list on the Chapters homepage.

```ruby
# This selects all <a> element that are inside an <li> element 
links = parsed_page.css("li a")
```

If you need to you can further filter page content with multiple uses of the `.css` method.

```ruby
# This selects all <a> element that are inside a <div> element 
div_links = parsed_page.css("div").css("a")
```

For more details about how to figure out the selector you want to use, see the [CSS Resources](#css-resources) section at the bottom.

The `.css` method will return a list of HTML elements that match whatever selector we gave it as an argument.

### Step 5

Since we selected a list of elements, we can now loop through all of them and grab only the visible text of the element with the `text` method.

```ruby
links.each do |link|
  p link.text
end
```

If we run the whole code we should get the text of the links we wanted:

```bash
"The One Reference"
"Nouns, verbs, and grammar"
"A few program notes"
"String"
"Getting strings from users"
 ...
```

## CSS Resources

- [CSS Diner](https://flukeout.github.io/) is a fun and helpful game that teaches you CSS Selectors.
- [Selector Gadget](https://selectorgadget.com/) is a Chrome extension that makes it almost too easy to find the exact selector you need to scrape a webpage. Watch the video in the link to see you that works.

Happy hacking!
