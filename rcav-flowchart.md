# RCAV Flowchart

Our apps are nothing more than a collection of URLs that we decide to allow users to access:

 - `mydomain.com/products`
 - `mydomain.com/photos/193`
 - `mydomain.com/signin`

So remember: everything always starts with a **route** between an *address* we want users to be able to visit and a *Ruby method* that will be responsible for generating a response to the user's browser.

In order to support a URL in your app such as `https://3000-your-gitpod-workspace.gitpod.io/home`, there are a lot of dots to connect!

![](/assets/rcav-chart.png)

 1. A user visits an address in our app; in this case, we chose `/home`.
 2. If we want to allow users to visit that address, we have to add a **route** for it in `config/routes.rb`.
 
    The complete route looks like this:
    
    ```ruby
    get("/home", { :controller => "pages", :action => "home" })
    ```
    
    Here's what's going on:

    A route is defined using the `get()` method, which has two arguments. The first argument is a `String` that contains the address we want to support; in this case, `"/home"`.
    
    The second argument to `get()` is a `Hash` that tells Rails what to do when someone visits the address. The `Hash` has two keys: `:controller` and `:action`.
 
    "Controllers" contain the logic of how to respond to requests (they're just Ruby classes).
    
    "Actions" are the actual logic that gets executed by Rails when a user visits an address (they're just Ruby methods).
    
    The key `:controller` must go to the name of a Ruby class; in this case, we chose `"pages"`.
    
    The key `:action` must go to the name of a Ruby method that we want Rails to execute when a user visits `/home`; in this case, we chose `"home"`. This name is **not required to match the route**.
  
 3. Rails finds a match for the controller name we specified in the `app/controllers` folder. Files that contain controllers must always end in `_controller.rb`, and begin with what we said in the route would be the name of the controller; in this case, `pages_controller.rb`.
  
    Rails finds the Ruby class in the file. The name of the class must be `CamelCased` and always end in `...Controller < ApplicationController`. In this case, `PagesController < ApplicationController`.
    
    Rails finds the method we specified as the action and executes it; in this case, we defined a method called `home`.
    
    We can write as much or as little Ruby as necessary within the action to satisfy the request — reading from APIs, doing math, whatever.
  
4. Once we've computed the final values that should be displayed to the user, we tell Rails the name of an **HTML view template** to use to format the output. To do so, we use the `render()` method. The complete `render()` method looks like this:
    
    ```ruby
    render({ :template => "page_templates/home.html.erb"})
    ```

    Here's what's going on:

    `render()` takes one argument, a `Hash`. The Hash must have a key, `:template`, with a String value. The string specifies the location of an Embedded Ruby HTML template to use to format the output. The first part of the string specifies the name of a folder, in this case `pages_templates` and the second part of the string specifies the name of a file, in this case `home.html.erb`.
  
    We have to create a folder within `app/views` that matches the name that we specified in the `render()` statement.
  
    We have to create a file within that folder that matches the name that we specified in the `render()` statement.

    Finally, if we've connected all the dots correctly, Rails will embed the variables in the `.html.erb` template, produce a final plain `.html` file, and send it back to the user's browser. Hurray!
 
If you _didn't_ connect the dots correctly, you will usually see a very descriptive error message; try to read and understand it.

Some things to keep in mind:

 - Capitalization (all file, folder, method, variable, and symbol names should be `snake_case`; only class names are `CamelCase`).
 - Spelling/pluralization matters (by convention, controller names are usually plural, but don't have to be).
 - Location (controller files must be in `app/controllers/`).
 - **READ THE ERROR MESSAGE!** It usually tells you exactly what is going wrong, and where. It will at least give you a strong hint.

---
