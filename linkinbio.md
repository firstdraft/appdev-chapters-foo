# Link in bio

Some social media apps, in particular Instagram, do not allow you to include links to other pages in posts. The only place you can include a URL is in your bio, and you can only include one. This soon led to a trend of people promoting something with a post, but including "Link in bio!" in the caption. They would then update the solitary link in their bio to the latest thing they wanted to promote.

Soon, a bunch of services cropped up that allow people to manage multiple links in a single, mobile-friendly page; and include a link to that page in their bio. The most popular of these is [Linktree](https://techcrunch.com/2020/10/26/linktree-raises-10-7m-for-its-lightweight-link-centric-user-profiles/){:target="_blank"}, but there are many others.

Linktree has many users, from media companies to celebrities to, most likely, some of your friends — and maybe even you? Here are some examples:

HBO's Instagram bio:

![](/assets/linkinbio-hbo-profile.jpg){:width="480"}

And HBO's list of links:

![](/assets/linkinbio-hbo-linktree.jpg){:width="480"}

Katy Perry's Instagram bio:

![](/assets/linkinbio-katyperry-profile.jpg){:width="480"}

And Katy Perry's list of links:

![](/assets/linkinbio-katyperry-linktree.jpg){:width="480"}

---

In this project, we're going to build our own mobile-friendly list of links that we can include in our social media profiles or anywhere else that we like. [Here's mine](https://rag.hu){:target="_blank"}:

![](/assets/linkinbio-raghu-final.png)

There are several benefits to writing our own rather than using a service like Linktree:

- We can use our own custom domain name for it; rather than `linktree.com/raghubetina`, notice that my URL is simply `rag.hu`.
- We don't have to pay. Linktree has a free tier with limited design options, but if you want access to the fun themes, analytics, or to remove the Linktree branding, you have to subscribe to their $5/mo or $9/mo plan.
- We have all the power of CSS at our fingerprints to customize the design. Linktree, like all "no code" tools, limits you to a set of pre-defined constraints that you have to work within. Not so if you're writing the code yourself.
    
    For example, if you [click through to mine](https://rag.hu/){:target="_blank"}, you'll notice a lot of touches that aren't available options even on the paid Linktree plans: an animated background, a "frosted glass" effect on the links, etc.
- It's just plain fun!

Let's get started.

## Getting started

- We're going to start our projects a little differently this time. Rather than clicking the "Load [assignment] in a new window" button in Canvas, which usually will automatically create your copy of the repository on your organization, you will manually create your own blank Rails app (the same steps you can follow any time you want to build your own, non-assigned projects):
    - Visit our [appdev-projects/base-rails](https://github.com/appdev-projects/base-rails) repository and click the "Use this template" button. Then select "Create new repository" from the dropdown.
    - On the next screen, leave the "Owner" dropdown alone.
    - For "Repository name", enter "**your-username**.github.io". Substitute your own, real username for **your-username**.
        - So, for example, my repo name is "raghubetina.github.io".

            ![](/assets/linkinbio-repo-name.png)

        - Make sure to include the ".github.io" part in the repo name. E.g.:
        - Click "Create new repository from template".

### Enable GitHub Pages deployment

Next, we'll tweak some settings of our repository to allow for superfast, free hosting using GitHub Pages.

In the Settings of the repository, find Pages in the left sidebar and switch the folder to `docs/`. Then Save:

![](/assets/linkinbio-gh-pages-settings.png)

### Create Gitpod workspace

- Create a new Gitpod workspace based on your brand new repository:
    - In a new tab's address bar, type "gitpod.io/#". Then copy-paste the URL of your new repository after that. The URL should look something like `gitpod.io/#https://github.com/your-username/your-username.github.io`
    - Press <kbd>return</kbd> to visit that URL and Gitpod will automatically start creating a new workspace for you.
- Once you're in to your new workspace, `bin/server` at a terminal tab as usual to start up your web server.
- Open your app preview in a new tab.
- Create a file called `index.html` in the `docs/` folder. Add "hello, world" and make sure that it shows up when you refresh your app preview.

## First things first — the content

To start with, we need content. You'll probably want to gather:

- A profile picture for the top of the page. This doesn't have to be an image of you; it can be anything. [Unsplash](https://unsplash.com/){:target="_blank"} is a great resource for high quality stock images if you don't want to use an image of yourself.
- The URLs of your social media profiles. I used my GitHub, LinkedIn, Instagram, and Twitter pages.
- A list of links you want to share. I used a handful of essays and short stories that I find myself sharing with people often. [Here are some examples that you can peruse for inspiration](https://clickydrip.com/linktree-examples/){:target="_blank"}.
- A thumbnail image for each link. I used a few strategies to find an image for each link:
    - [Search Google images](https://images.google.com/){:target="_blank"} and look for one hosted on wikimedia.org.
    - Searched [Unsplash](https://unsplash.com/){:target="_blank"} for a relevant image.
    - [Generate an image with AI](https://dezgo.com/){:target="_blank"}.

I downloaded the image and then uploaded it to my Gitpod workspace by drag-and-dropping it into the `docs/` folder.

If you want to, you can use fake placeholder images and links for everything, but I encourage you to gather real content. It'll be more fun, you'll end up with a page that you can actually use on your social media profiles, and you'll have a good piece for your portfolio.

## Basic HTML Structure

Let's add our images, copy, and links. I wrapped each block of content in a `<div>` for now, to create some separation. I also gave each `<div>` a `class=""` attribute; since we haven't written any CSS yet, they don't do anything, but they help me remember what each `<div>` represents. Something like this:

```html
<div class="banner">
  <img src="profile-pic.jpg" alt="Raghu Betina headshot">
</div>

<div class="name">
  Raghu Betina
</div>

<div class="social-icons">
  <a href="https://github.com/raghubetina" target="_blank">
    GitHub
  </a>

  <a href="https://www.linkedin.com/in/raghubetina/" target="_blank">
    LinkedIn
  </a>

  <a href="https://www.instagram.com/raghubetina/" target="_blank">
    Instagram
  </a>

  <a href="https://twitter.com/raghubetina" target="_blank">
    Twitter
  </a>
</div>

<div class="link">
  <img
    src="https://www.ycombinator.com/assets/ycdc/yc-og-image-0cfa80cac837d64d9b4f0705950000b66906ac032791376bd721f246fafcc7b4.png">

  <a target="_blank" href="http://paulgraham.com/startupideas.html">How to Get Startup Ideas
    — Paul Graham</a>
</div>

<div class="link">
  <img src="/thumbnails/typography.jpg">

  <a target="_blank"
    href="https://practicaltypography.com/typography-in-ten-minutes.html">Typography in ten minutes — Matthew
    Butterick</a>
</div>

<div class="link">
  <img
    src="https://media.newyorker.com/photos/59096d451c7a8e33fb38e4ca/16:9/w_1280,c_limit/071210_r16884_p646.jpg">

  <a target="_blank" href="https://www.newyorker.com/magazine/2007/12/10/the-checklist/">A
    Life-Saving Checklist — The New Yorker</a>
</div>

<!-- Etc, for as many links as you want -->
```

Of course, I also have [the standard HTML boilerplate](https://chapters-foo.ourplatform.com/chapters/771#housekeeping){:target="_blank"} (`<html>`, `<head>`, `<body`, etc) in order to make it a valid document.

Two things to notice:

- I'm using the `target="_blank"` attribute on any links that I want to open in a new tab.
- For images that I am serving from my own `docs/` folder:
    - I created a subfolder called `thumbnails` to help keep things organized, and moved the images there.
    - When referencing the URL of the image in a `src=""` attribute, I start with a leading slash — e.g.:

        ```html
        <img src="/thumbnails/typography.jpg">
        ```

        I do _not_ include `/docs` in the URL.

At this stage, your page technically serves its purpose — a collection of links people can click on — but it probably looks terrible, [like this](https://rag.hu/01-content){:target="_blank"}.

## HTML Validator

If at any point your HTML breaks, or you suspect you e.g. forgot a closing tag but can't find it, [the W3C HTML Validator](https://validator.w3.org/#validate_by_input){:target="_blank"} might come in handy. Paste in your entire HTML document and click "Check", and it will give you a list of feedback. Some of them are yellow warnings and can be safely ignored for now, but any critical mistakes (like missing closing tags or quotation marks) will show up as red errors.

For example, if you run your HTML through the validator right now (try it), it will display a bunch of errors because we don't have `alt=""` attributes on our `<img>`s. These are important to include for accessibility reasons, and just in case the image breaks for some reason (i.e. the URL changes). We should add [descriptive alternative text](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#accessibility_concerns){:target="_blank"} for each image.

## View Source

You should try to type out your page yourself — avoid copy-pasting. Making mistakes, fixing them, and developing your own muscle memory is important.

That said, _after_ you've attempted it yourself, you can View Source (Windows: <kbd>Ctrl</kbd>+<kbd>U</kbd> or Mac: <kbd>Command</kbd>+<kbd>Option</kbd>+<kbd>U</kbd>) on any of my example intermediate pages to see my code.

## Sizing images

Now, let's start to make the page look better. Let's add a `<style>` element inside the `<head>` of the document so that we can begin applying CSS. We won't use an external stylesheet for now, since we're only planning to apply this CSS to a single page. Maybe we can start by giving the `body` some breathing room with top and bottom padding:

```html
<style>
  body {
    padding-top: 40px;
    padding-bottom: 40px;
  }
</style>
```

Let's start by sizing the profile picture. We need to give it a class so that we can apply CSS rules to it — let's call it `banner-image`:

```html
<div class="banner">
  <img src="profile-pic.jpg" alt="Raghu Betina headshot" class="banner-image">
</div>
```

Then, let's make the banner image 128 pixels by 128 pixels:

```css
<style>
  .banner-image {
    width: 128px;
    height: 128px;
  }
</style>
```

Unless your original image was exactly square, this probably will look squished when you check out the results. To solve this problem, we can use [the `object-fit` property](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit){:target="_blank"}:

```css
.banner-image {
  width: 128px;
  height: 128px;
  object-fit: cover;
}
```

It's quite common to see circular profile pictures. If you want to, set a large `border-radius` to achieve that:

```css
.banner-image {
  width: 128px;
  height: 128px;
  object-fit: cover;
  border-radius: 128px;
}
```

I didn't use one on my profile picture, but you should feel free to get creative with [borders](https://developer.mozilla.org/en-US/docs/Web/CSS/border){:target="_blank"}, as well.

Similarly, let's size all of the thumbnail images as 48px by 48px:

```css
.thumbnail {
  width: 48px;
  height: 48px;
  border-radius: 48px;
  object-fit: cover;
}
```

Don't forget to add the class to the relevant `<img>` elements. Now, your page should look [something like this](https://rag.hu/02-size-images){:target="_blank"} — much better.

## Basic colors

Let's add some color to make it easier to see how much space each element is occupying. We'll, at a minimum, need a color for the background of the entire page and for each link.

You can come up with your own palette, or you can use [Happy Hues](https://www.happyhues.co/){:target="_blank"}, a nice set of curated color palettes.

I used [this palette](https://www.happyhues.co/palettes/10){:target="_blank"}. I used the background color, headline color, button color, and button text color like this:

```css
body {
  background-color: #004643;
}

.name {
  color: #fffffe;
}

.social-icons a {
  color: #fffffe;
  text-decoration: none;
}

.link {
  background-color: #f9bc60;
}

.link a {
  color: #001e1d;
  text-decoration: none;
}
```

As you can see, I also removed the underlines from links with `text-decoration: none`.

Notice that I used the [descendant combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_combinator){:target="_blank"}:

```css
.link a {
  /* ... */
}
```

This selector targets only `<a>` elements that are descendants of elements with class `link`. This is a handy alternative to adding a new class to all of the elements I'm interested in targeting.[^css_diner]

[^css_diner]: If you want to become a pro at writing CSS selectors, I recommend an interactive tutorial/game called [CSS Diner](https://flukeout.github.io/){:target="_blank"}. If you make it through all 32 levels, you'll be better than most front-end developers at writing advanced CSS selectors. In addition to making it easier to style your own pages, knowing how to write advanced selectors will pay dividends if you're interested in doing any web scraping.

My page now [looks like this](https://rag.hu/03-basic-colors){:target="_blank"}.

## Layout

Now, for the interesting part — laying out the elements where we want them on the page.

### Overall page layout

Since this is a relatively simple, single-column layout, we could stay in the normal flow mode and achieve most of the positioning that we want with `margin` and `padding`.

But let's use `display: flex` instead. It will make it much easier to do things like vertically center the text within each link's box.

First, I'll wrap all of our content — the `div.banner`, the `div.name`, the `div.social-icons`, and all of the `div.links` — within a new parent `<div>` with a class called `items`. This will make it easier for me to position and size everything uniformly. Then I will switch the layout mode of the new `div.items` from the default normal flow to `flex`:

```css
.items {
  display: flex;
}
```

If you try that and refresh your page, you'll see that all of the elements are now horizontally side-by-side. This is because the default `flex-direction` is `row`. Let's switch the `flex-direction` to `column` to lay them out vertically again:

```css
.items {
  display: flex;
  flex-direction: column;
}
```

If you refresh, you'll see the layout is vertical again. When we're using `display: flex` mode, we can use the `gap` property to provide some breathing room between each child element, rather than having to add `margin`:

```css
.items {
  display: flex;
  flex-direction: column;
  gap: 30px;
}
```

On laptop screens, the buttons are running all the way to the edge of the screen, which isn't very attractive. Let's set a `max-width` of around 640px (you choose a value that looks good to you):

```css
.items {
  display: flex;
  flex-direction: column;
  gap: 30px;
  max-width: 640px;
}
```

### Layout for each link

Within each link, it would be nice if:

- The thumbnail and text were vertically centered within the box.
- The text was horizontally centered in the space remaining next to the thumbnail.

`display: flex` to the rescue!

#### Vertically centering with align-items

We can vertically center child elements with the `align-items` property:

```css
.link {
  background-color: #f9bc60;
  display: flex;
  align-items: center;
}
```

If you refresh, the thumbnails should be lined up nicely with the link text.

#### flex-grow

Next, let's center the text of each link. I'm going to expand the existing rule that we have for `.link a`. Can we simply add `text-align: center` and call it a day?

```css
.link a {
  color: #001e1d;
  text-decoration: none;
  text-align: center;
}
```

If you refresh, you'll see that didn't work. Why?

To make it easier to see things while I am working on layouts, I often use the following hack:

```css
* {
  border: thin red solid;
}
```

This puts a thin red border around every element. Your page should now look something like this:

![](/assets/linkinbio-before-flex-grow.png)

We can see that the `<a>` elements are only just wide enough to fit their content, so centering within them isn't doing anything. Instead, we want the `<a>` element to occupy all of the available space to the right of the thumbnail.

To achieve, this we can use [the `flex-grow` property](https://css-tricks.com/almanac/properties/f/flex-grow/){:target="_blank"}:

```css
.link a {
  color: #001e1d;
  text-decoration: none;
  text-align: center;
  flex-grow: 1;
}
```

Now the `<a>` element grows to fill any available space, while the `<img>` element stays the same size (it still has the default value for `flex-grow`, which is `0`). And our text should be nicely centered since we already added the `text-align`.

#### justify-content

Now let's take care of centering the profile picture and name, as well as putting some breathing room between the social links.

Flexbox has [a wonderful property called `justify-content`](https://css-tricks.com/almanac/properties/j/justify-content/){:target="_blank"} that will help with all of these things:

```css
.name {
  color: #fffffe;
  display: flex;
  justify-content: center;
}

.banner {
  display: flex;
  justify-content: center;
}

.social-icons {
  display: flex;
  justify-content: space-around;
}
```

You could also use the same technique to center the `div.items` within the `<body>`:

```css
body {
  display: flex;
  justify-content: center;
}
```

But then we again need to tell the child elements to grow to take up all available space with `flex-grow`:

```css
.items {
  display: flex;
  flex-direction: column;
  gap: 30px;
  max-width: 640px;
  flex-grow: 1;
}
```

Our page layout should now look solid!

![](/assets/linkinbio-finished-layout.png)

Let's add a little bit of padding inside our `div.link`s:

```css
.link {
  background-color: #f9bc60;
  display: flex;
  align-items: center;
  padding: 5px;
}
```

It should now be safe to remove the `* { border: thin red solid; }` hack, unless you want to continue playing with layout, padding, etc.

Our page now looks [something like this](https://rag.hu/04-layout){:target="_blank"}.

## Deploy!

We've made a lot of progress, and our list of links is functional and looking pretty solid! We can and will spend more time fine-tuning, but this seems like a great time to deploy our app to industrial-grade hosting so that we can actually link to it in our bios!

Sadly, after over a decade, [Heroku's free tier was eliminated](https://techcrunch.com/2022/08/25/heroku-announces-plans-to-eliminate-free-plans-blaming-fraud-and-abuse/) as of November 28th, 2022. There are some silver linings --- they have launched [a new discount through GitHub Student](https://www.heroku.com/github-students), and they created [a couple of new, less expensive plans](https://blog.heroku.com/new-low-cost-plans) (Eco, Basic, Mini).

For full-stack, dynamic, interactive, database-backed apps, I plan to still use Heroku. However, Heroku is no longer a good choice for hosting static HTML websites. There are several other free and fast options for that (e.g. [Netlify](https://www.netlify.com/) and [Vercel](https://vercel.com/)).

Today, I want to show you GitHub's offering for hosting static websites: GitHub Pages. We will deploy our Link In Bio via GitHub Pages. This will have several benefits:

-   It's free.
-   It is tightly integrated with GitHub repositories (obviously), so all we need to do to deploy is what we do anyway --- make a commit and push to GitHub .
-   It doesn't have any of Heroku's old free tier's restrictions.
    -   It will be up 24/7/365.
    -   It automatically includes SSL for custom domains (important if you're using a top-level domain that requires http**s**, like .dev).
-   GitHub Pages sites are automatically assigned a subdomain under `.github.io`. This carries some developer cred.
-   Or you can easily use your own domain.

Here's what to do to get your first GitHub Pages site going:

- Visit `/git`.
- Make a commit and then push the changes you've made so far to your GitHub repository.
- That's it! In a few minutes, your site should be live at `https://your-username.github.io`!
- Eventually, consider adding some other pages to your site besides just `index.html` --- a list of projects that you've built, for example.
- If you want to use a custom domain name like `yourname.com` rather than something like `your-username.github.io`, then you'll first have to purchase a domain.
    - I recommend [Porkbun](https://porkbun.com/){:target="_blank"}, or, for more exotic top-level domains, [Gandi.net](https://www.gandi.net/en){:target="_blank"}. 
    - [Here is a guide to adding your own domain to your Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Let me know if you get stuck.

You can create as many GitHub Pages sites as you want --- one per repo. [Read more about GitHub Pages here.](https://docs.github.com/en/pages/quickstart)

## This is the end of the required portion

This is the end of the required portion of this assignment. In Canvas, submit the URL of your deployed app (something.github.io, not your GitPod preview). If you are willing to share your creation, please also include "Add me to the showcase" in the submission text area.

## Make it your own

Now that we have the basics up and running, it's time for you to get creative and make it your own! You can continue to make changes, commit, and push them to deploy. We aren't grading for anything particular, so just have fun with it.

Here are a bunch of resources for you to explore:

### Fun design resources

The following are a collection of neat tools that will help you create interesting backgrounds, generate gradients and shadows, find font pairings, etc.

Glance at each one and pick one or two to integrate into your design. If you want to bounce ideas on things you can integrate, chat with an instructor.

Once you've picked something to add, try to figure out how to integrate it on your own; ask lots of questions when you get stuck.

#### Icons

To use Font Awesome icons (for example, for your LinkedIn/GitHub/Twitter/etc links), first include this in the `<head>` of your document:

```html
<!-- Connect Font Awesome -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/js/all.min.js"></script>
```

Then peruse [the icon list](https://fontawesome.com/search?m=free){:target="_blank"} and copy-paste the code examples into your HTML.

#### Fonts

- [The Ultimate Collection of Google Font Pairings (Displayed Beautifully with Classic Art)](https://heyreliable.com/ultimate-google-font-pairings/){:target="_blank"}
- Reading: [Typography in Ten Minutes](https://practicaltypography.com/typography-in-ten-minutes.html){:target="_blank"}

#### Images

- [Unsplash](https://unsplash.com/){:target="_blank"}: Search engine for free stock images.
- [Dezgo](https://dezgo.com/){:target="_blank"}: AI image generation.
- [Image Optimizer](http://www.imageoptimizer.net/){:target="_blank"}: Reduce your images' filesize in case they're taking too long to load.
- [Clippy](https://bennettfeely.com/clippy/){:target="_blank"}: Create geometric masks for your images.
  
#### Color palettes

- [Happy Hues](https://www.happyhues.co/){:target="_blank"}

#### Shadow generators

- [CSSMatic's Box Shadow Generator](https://www.cssmatic.com/box-shadow){:target="_blank"}

#### Gradient generators

- [Vivid Gradient Generator](https://learnui.design/tools/gradient-generator.html){:target="_blank"}
- [Easing Gradients](https://larsenwork.com/easing-gradients/){:target="_blank"}

#### Patterns

- [CSS Background Patterns](https://www.magicpattern.design/tools/css-backgrounds){:target="_blank"}
- [Repper](https://repper.app/){:target="_blank"}
- [Pocoloco](https://pocoloco.io/){:target="_blank"}

#### Generative art

- [Silk](http://weavesilk.com/){:target="_blank"}
- [Haikei](https://app.haikei.app/){:target="_blank"}
- [Tabbied](https://tabbied.com/select-artwork){:target="_blank"}
- [Broider](https://maxbittker.github.io/broider/)

#### Filters

- [https://css-tricks.com/almanac/properties/b/backdrop-filter/](https://css-tricks.com/almanac/properties/b/backdrop-filter/){:target="_blank"}
- [https://css-tricks.com/almanac/properties/f/filter/](https://css-tricks.com/almanac/properties/f/filter/){:target="_blank"}

---

### Always be committing

Be sure to make lots of git commits along the way as you work! Have fun ☺️
