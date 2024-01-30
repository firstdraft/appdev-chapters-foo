# Turbolinks

Rails, by default, includes a library called Turbolinks[^turbolinks_read_more] that actually has been doing some Ajax for us all along without us even knowing it. When users click on links, Turbolinks has been only replacing the `<body>` of the document, to make the application feel a bit snappier.

## turbolinks:load

This, however, can mess with our jQuery, which is listening for `$(document).ready` (which only fires when a full page reload occurs) to initialize event handlers when users navigate to different pages. To solve this, we can use the `turbolinks:load` event instead:

[^turbolinks_read_more]: [Read more about Turbolinks here](https://github.com/turbolinks/turbolinks#installing-javascript-behavior){:target="_blank"}, if you're interested.

```js

$(document).on('turbolinks:load', function() {
  console.log("It works on each visit!")
})
```

## JS libraries acting funny?

If you pull in a 3rd-party JavaScript library (say, for example, Google Maps), and you notice some weird behavior, especially things that are resolved when you do a full page refresh: the issue is probably related to Turbolinks.

Try the `turbolinks:load` fix above. Or sometimes you have to do some other things, [as we did to fix the Bootstrap modal in Photogram Industrial](https://www.honeybadger.io/blog/turbolinks/){:target="_blank"}.

A common strategy is to [just remove Turbolinks](https://stackoverflow.com/questions/38649550/rails-how-to-disable-turbolinks-in-rails-5){:target="_blank"}; or when you're first creating your app with `rails new`, use the `--skip-turbolinks` option to never include it in the first place. Since we're about to add real Ajax to our application anyway, having the automatic sort-of-but-not-really-Ajax of Turbolinks becomes less helpful.