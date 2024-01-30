# Sharing a Gitpod Snapshot

It's often helpful to share a snapshot of the state of your entire Gitpod workspace with someone else.

### Take the snapshot

From the hamburger menu in the top-left corner of your IDE, select `Gitpod: Share Workspace Snapshot`:

![](/assets/gitpod-snapshot-file-menu.png)

### Copy the snapshot URL

It will take a moment to create the snapshot. Then a dialog will pop up in the bottom-right corner that will give you the URL to copy and share:

![](/assets/gitpod-snapshot-copy-url.png)

#### The correct URL looks like this

The URL that you share should look something like this:

```
https://gitpod.io#snapshot/5a47e40d-e279-44e5-96bc-ae33cd48f151
```

Note the `#snapshot` fragment of the URL. That means you have the right one.

#### Not this

The URL should _not_ look something like this:

```
https://ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io/
```

That is the URL of your own IDE, which no one else can access.

#### Or this

The URL should _not_ look something like this:

```
https://3000-ac1bde40-34e8-421d-a102-6425971fb9db.ws-eu38.gitpod.io
```

Note the `3000-` at the start. That is the URL of the live preview of your app.

### Snapshots are completely independent

When someone clicks on the snapshot URL, they will get their own private copy of your workspace in the state that it was in when you took the snapshot.

Any changes they make to their copy will not affect your workspace. Similarly, any changes you make to your workspace won't affect their snapshot. So you can keep trying to resolve the problem on your own, or work on the next task, without interfering with their snapshot.
