# draft:account generator

## A special sort of table: user accounts

When each row in a table is going to hold a _person_, i.e. it's going to need a column for `email`, `password_digest`, etc; then you probably shouldn't use the `draft:resource` generator. This is because you _do not_ want to generate the standard RCAVs (`index`, `show`, etc) with the standard forms to add a new record, update a record, delete a record, etc.

Instead, you need routes, actions, and templates for signing up, signing in, editing profile, cancelling an account, etc. The RCAVs that the `draft:resource` generator writes for you require so much modification to transform into those pages that it is easier to just start from scratch with the `model` generator.

Fortunately, however, there is another generator that will give you a nice head start towards the boilerplate required for most sign-in/sign-out RCAVs: `draft:account`. Let's say you want a model called `user` with columns `first_name`, `last_name`, and `company_id`:

```
rails generate draft:account user first_name:string last_name:string company_id:integer
```

You **should not include `email`, `password`, `password_confirmation`, or `password_digest`** in the command. `email` and `password_digest` string columns will automatically be added to the table for you.

Explore the generated code. It added:

 - A `User` model file.
 - A migration which will issue the SQL transaction to create the table and columns in the database once we `rails db:migrate`.
 - Routes, actions, and views for:
    - signing up
    - signing in
    - editing profile
    - signing out
    - deleting account

### @current_user

In addition, `ApplicationController`, the `draft:account` generator wrote a method called `load_current_user`:

```ruby
# app/controllers/application_controller.rb

def load_current_user
  the_id = session.fetch(:user_id)

  @current_user = User.where({ :id => the_id }).at(0)
end
```

You can call this method from within any action to easily define an instance variable called `@current_user` which would use the cookie created by the sign-in/sign-up actions to look up the record in the `User` table that represents whoever is signed in.

Furthermore, it wrote a line:

```ruby
# app/controllers/application_controller.rb

before_action(:load_current_user)
```

This line automatically calls the `load_current_user` method before any action is called! That means that `@current_user` is automatically defined within every action and view template. If someone is signed in, it is a `User`; if not, it is `nil`. From there on out, it's up to you to use `@current_user` to personalize the action/view.

### Forcing sign in

The `draft:account` also writes another method within `ApplicationController`:

```ruby
# app/controllers/application_controller.rb

def force_user_sign_in
  if @current_user == nil
    redirect_to("/user_sign_in", { :notice => "You have to sign in first." })
  end
end
```

This method, if called, will redirect the user to the sign in page if they are not already signed in. This is a very common pattern in applications, and saves us the trouble of having to do a million `if @current_user != nil ...` all over the place before we can use `@current_user` safely (assuming we need a `User`).

To call this method before _every_ action, add this line to `ApplicationController`:

```ruby
# app/controllers/application_controller.rb

# Below load_current_user

before_action(:force_user_sign_in)
```

The generator writes this line, but starts it out commented; uncomment it if you want to opt-in to forcing users to sign in.

However, you need to allow them to visit the sign-in/sign-up pages while being signed-out; to do that, in `UserAuthenticationController`, uncomment the following line:

```ruby
# app/controllers/user_authentication_controller.rb

skip_before_action(:force_user_sign_in, { :only => [:sign_up_form, :create, :sign_in_form, :create_cookie] 
```

Now you're all set; a person will have to sign in before they can visit any other action in the application, and you can confidently use `@current_user` knowing that it will actually be a `User` and not `nil`.

## Making Changes

That's it! You now have a solid sign-in/sign-out system to work from.

There's no magic to this generator; all it did was automate the tedium of building the many RCAVs required for sign-up/sign-in/sign-out. Since the RCAVs for authentication are so boilerplate, in the real world we often automate them (or use a gem like Devise).

From here on out, it's up to you to use `@current_user` to make the app do what it needs to do.
