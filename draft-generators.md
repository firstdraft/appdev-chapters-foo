# draft:resource generator

## Installation

Make sure this line is in your `Gemfile`:

```ruby
# /Gemfile

gem "draft_generators", :git => "https://github.com/firstdraft/draft_generators"
```

Then, at a Terminal prompt:

```bash
bundle install
```

Or make sure it is up to date with:

```bash
bundle update draft_generators
```

If you are starting with our [base-rails repository](https://github.com/appdev-projects/base-rails), then you've already got the gem included.

## Generating a resource

To generate a complete, database-backed web resource:

```bash
rails generate draft:resource <MODEL_NAME_SINGULAR> <COLUMN_1_NAME>:<COLUMN_1_DATATYPE> <COLUMN_2_NAME>:<COLUMN_2_DATATYPE> # etc
```

For example,

```bash
rails generate draft:resource photo image:string caption:text owner_id:integer
```

- The model name must be singular.
- Separate column names and datatypes with colons (NO SPACES).
- Separate name:datatype pairs with spaces (NO COMMAS).

In other words, the format of the command is exactly the same as when you were [generating only a model and table](https://chapters-foo.ourplatform.com/chapters/770#the-quick-way-to-create-a-table){:target="_blank"}, but `draft:model` is replaced with `draft:resource`.

> Note: `rails g` is short for `rails generate`, like  `c` is for `console` and `s` is for `server`.

As usual, we have to run the command `rails db:migrate` at a Terminal prompt to execute the migrations that were written for us by the generator, to actually create the new table.

### What just happened?

Whoa, what just happened? Well, let's look at the output from the command:

```bash
create  app/controllers/photos_controller.rb
invoke  active_record
create    db/migrate/20200602191145_create_photos.rb
create    app/models/photo.rb
create  app/views/photos
create  app/views/photos/index.html.erb
create  app/views/photos/show.html.erb
  route  RESTful routes
insert  config/routes.rb
```

 - A model and a migration for the table.
 - A controller named after the table.
 - Some view templates related to the table.
 - Some routes related to the table.

If you look at the routes, controller, and views, you'll see that it has essentially added in all of the standard CRUD boilerplate for us — automatically! Try navigating to `/photos`, or whatever your table is called, and you'll see that you have a fully-functional interface to CRUD records. Awesome!

This makes sense because, as you might have noticed by now, the Golden Five RCAVs relating to letting users Create, Read, Update, and Delete records through their browser are basically the same for every table; only the form inputs vary, really, based on the different columns in the tables.

And since we're going to need most of the Golden Five for most of our tables, why not automate the boilerplate? Then we can just delete the stuff that we don't want, and modify what's left to match our needs.

Whew! What a time saver. However, it only saves time if you are comfortable with all of the code that it is writing for you — otherwise the code is intimidating and you are scared to change it. Then, rather than saving you time, the generators slow you down; relative to you writing code by hand that you understand 💯. So choose your approach wisely. When in doubt, pick a URL that you want the user to be able to visit, connect the RCAV dots yourself, and make it happen.

## What if I made a mistake when I generated a resource?

### Go back to an earlier git commit

You've been making lots of git commits, right? If so, you can [jump back to an earlier commit and try again](https://chapters-foo.ourplatform.com/chapters/839#jumping-back-in-time).

Alternatively....

### If you've already run rails db:migrate

**If you haven't run `rails db:migrate` yet, then you can proceed to `rails destroy draft:resource`, below.**

If you made a mistake when generating your `draft:resource` AND **you've _already_ run `rails db:migrate`**, then first you have to run the command:

```bash
rails db:rollback
```

to get the database back into the state that it was in before. The command looks at the most recent migration and reverses it.

### rails destroy draft:resource

Anything that you can `rails generate`, you can also `rails destroy`; the latter command will undo whatever the former one does. So, for example, you can:

```bash
rails destroy draft:resource photo
```

This will remove all the files that `rails generate draft:resource photo ...` had previously added. You can then correct your error and re-generate from scratch.

## With great power...

With great power comes great responsibility. If you use a generator to automate writing a bunch of code, then you _own_ that code. It's just as if you typed it yourself, really quickly. From that point forward, it's completely on you to modify the code to fit your needs.

The generated code will _never_ be exactly what you need directly out-of-the-box. You still have to remember all of your basics, and write additional RCAVs as needed. Some of the automatically generated RCAVs might be security holes that you definitely don't want, so you should delete them.

If you decide, as you certainly will at some point in the future, to [add a new column](https://chapters-foo.ourplatform.com/chapters/770#adding-or-removing-columns-from-your-table), then you'll have to go in and edit all of the relevant files (forms, processing actions) by hand. Or create new RCAVs entirely.

I wrote the generators for you to speed you up, serve as a starting point for you, and be an example for you to learn from. But **you can't be afraid to change the generated code**. Strive to understand every line that it wrote for you, so that you can modify it, delete it, and otherwise customize it to your own needs.
