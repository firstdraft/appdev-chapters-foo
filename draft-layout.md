## A better Application Layout file

To generate an application layout file that includes links to Bootstrap, Font Awesome, and some boilerplate markup for a nav bar and alert messages, run the command

```bash
rails g draft:layout
```

It will warn you that it is going to overwrite your existing `app/views/layouts/application.html.erb` -- say yes if you are sure that's okay. Copy out any important stuff if necessary, to be re-pasted back in.

As with all generators, I recommend making a git commit before you generate, and then compare the diff at `/git`. What files did it add? What are they doing?
