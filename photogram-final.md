# Photogram Final

Here is your target:

[https://photogram-final.matchthetarget.com/](https://photogram-final.matchthetarget.com/){:target="_blank"}

Explore it and see what's different relative to previous Photogram targets.

## Hints

The starting point of this project is a blank Rails application. You need to create all the tables and models yourself!

We domain modeled this application in first two weeks of class, and used the same database structure in photogram-gui and photogram-signin; here's the Entity Relationship Diagram (ERD):

![](/assets/photogram-final-erd.png)

_All tables will automatically get the usual `id`, `created_at`, and `updated_at` columns._

If you add these columns _exactly_, then you can run the `rails sample_data` Rake task to add example data to your database tables like with the homeworks.

You can use the `model` generator to add your tables, or you can use [the `draft:resource`](https://chapters-foo.ourplatform.com/chapters/773) to add the tables _and_ give yourself a big head start on routes, controllers, actions, and view templates.

You can use [firstdraft](http://firstdraft.com/)'s Co-Pilot to help write the commands to generate the tables and avoid typos.

You should also consider adding [association accessor methods](https://association-accessors.firstdraft.com/) to your models to make your job easier. [Validations to protect data integrity](https://chapters-foo.ourplatform.com/chapters/845) are helpful as well.

### Important notes on generating:

 - Remember that if you use [the `draft:account` generator](https://chapters-foo.ourplatform.com/chapters/888) for user accounts, you do not need to specify `email` and `password_digest` columns; they are automatically added, like `id`, `created_at`, and `updated_at`. I.e.:

    ```
    # Don't do this
    rails generate draft:account user email:string password_digest:string

    # Do this instead
    rails generate draft:account user
    ```

    You still have to specify any other columns that you want in the table, besides `email` and `password_digest`.

 - When creating the follow requests table, the model name should be `FollowRequest`, as you can see in the ERD above. If you generate a model named `Followrequest` (note the lack of a capital `R`), **then the sample data task we wrote for you will not work.**

    In order to generate a model named `FollowRequest`, you need to use the snakecased version, `follow_request`, at the command line. If you use `followrequest`, then you'll get a model named `Followrequest`.
 
    So: When you run the generator, make sure to the snakecased version of `FollowRequest`: `follow_request`. For example, `rails generate model follow_request ...`.

## More notes

### Image Uploads

In the target, users add images by uploading files instead of entering image URLs into a text field. **Until you setup real image uploads in your project, all image related tests will fail.** Please see the chapter on [images uploads](https://chapters-foo.ourplatform.com/chapters/790) for more information.

### Follow Requests

When a `FollowRequest` is created you need to check if the recipient of the request is a private User. If they are private, the `status` column of the `FollowRequest` should be set to `"pending"`. If they are _not_ private the `status` should be set to `"accepted"`.

If a user has a private account, all `"pending"` received `FollowRequest`s should appear on their details page with the option to accept. Accepting should change the `status` from `"pending"` to `"accepted"`, while rejecting should set the `status` to `"rejected"`.

### Feed 

Clicking the **Feed** link should show all of the photos from every person that the user is following. For example, if I am following Jelani, I should see all of Jelani's posted photos. 

### Discovery

Clicking the **Discovery** link should show all of the photos liked by the people the user is following. For example, if I am following Jelani and he has liked seven different photos, all of those photos should be visible in my discovery section. 
