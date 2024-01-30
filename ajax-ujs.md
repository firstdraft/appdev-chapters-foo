# Ajax with Rails UJS


 1. Change the default behavior of links and forms.
   
    When the user clicks on a link/form, we're going to keep them where they are instead of sending them to a different URL.
    
    We'll still make the same GET/PATCH/POST/DELETE request as before, to the same route and with the same parameters; but it will be in the background, using JavaScript.
 2. In the action triggered by the request, instead of responding with a `.html.erb` template or redirecting as usual, we'll **respond with a `.js.erb` template containing some jQuery**.
 3. The jQuery will run in the user's browser and update just the part of the page that needs it (sliding in the comment, updating the like count, etc).