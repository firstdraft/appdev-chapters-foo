# Forcing Chrome to "Hard" Refresh

Sometimes, when we update a CSS stylesheet, our page appears not to change. This is especially frequent when we're working on static HTML files in the `public/` folder.

The cause is usually Chrome's aggressive "caching", i.e. re-using static assets that it has already downloaded (for performance reasons). If we refresh an HTML page that we've updated, Chrome won't necessarily also refresh all `<link>`ed CSS files — unless we ask it to by "hard" refreshing.

To do so:

 1. Open the Dev Tools...
    - from the `View > Developer` menu
    - or right-click on any element and `Inspect`
    - or press <kbd>F12</kbd>
    - or <kbd>Ctrl</kbd>`+`<kbd>Shift</kbd>`+`<kbd>J</kbd> (on Windows) or <kbd>Option</kbd>`+`<kbd>Command</kbd>`+`<kbd>J</kbd> (on Mac)
 2. **Right-click** on the refresh button.
 3. Select "Empty cache and hard reload".

Open Dev Tools:

![](/assets/hard-refresh-dev-tools-2.png)

With Dev Tools open, "hard" refresh:

![](/assets/hard-refresh-right-click-refresh-2.png)

Your HTML document should now have the latest CSS and any other linked assets (like images or javascripts).
