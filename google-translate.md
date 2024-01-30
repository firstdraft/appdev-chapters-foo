# Google Cloud Translate

 - [Google Cloud Translation](https://cloud.google.com/translate)

If you want to use Google's Ruby gem in one of your own projects, then add the gem to your Gemfile:

```ruby
# /Gemfile
gem "google-cloud-translate", "2.3.0"
```

Then `bundle install` and restart your web server.

Next, we have to create environment variables containing our Google Translate credentials. You can either sign up for your own or use the ones we've provided on Canvas. The two variables you need to create are `TRANSLATE_PROJECT` and `TRANSLATE_CREDENTIALS`.

You now have access to the `Google::Cloud::Translate` class. To use it (you can launch a `rails console` in a new Terminal tab and give the following a try, if you like:

```ruby
require "google/cloud/translate"

gt_client = Google::Cloud::Translate.new({ :version => :v2 })

translation = gt_client.translate("Hello, world!", { :to => "es" })
```

Amazing!

To list all available languages,

```ruby
languages = gt_client.languages("en") # The argument determines what language to list the other language names in
languages.size #=> 104
languages[0].code #=> "af"
languages[0].name #=> "Afrikaans"
```

You can use this list to, for example, create dropdowns allowing the user to select which languages to translate from/to.

Read more at the gem docs:

[Ruby gem documentation](https://googleapis.dev/ruby/google-cloud-translate/latest/index.html#Using_the_legacy_v2_client)
