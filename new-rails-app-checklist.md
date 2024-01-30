# New Rails App Checklist

## Domain

Get a domain. I recommend using a registrar that allows for [using the root domain on Heroku](https://devcenter.heroku.com/articles/custom-domains#configuring-dns-for-root-domains){:target="_blank"} (i.e. if you want to you can use `https://yourdomain.com` rather than `https://www.yourdomain.com`). Not all registrars allow the type of DNS record we need for this (for example, Google Domains doesn't).

## rails new

Create your rails app. You can:

 - Use [the vanilla-rails template repository](https://github.com/appdev-projects/vanilla-rails/generate){:target="_blank"}.
 - Run `rails new` yourself; if so, I recommend the `--database=postgresql` flag. E.g.:

    ```
    rails new my-fancy-app --database=postgresql
    ```

## RuboCop

Use [RuboCop](https://github.com/rubocop/rubocop){:target="_blank"} to enforce style consistency in the project.

`gem install rubocop`/`gem update rubocop` to get access to the `rubocop` command line program.

Add to Gemfile:

```ruby
gem "rubocop-performance"
gem "rubocop-rails"
```

 - You can then do `rubocop -A` to automatically fix many style violations that come out of the box with `rails new`.
 - `rubocop --auto-gen-config` will generate a todo file with all of the remaining warnings.

