# QR Code Ruby

In this project, we'll write a command-line program that generates QR code images. We'll be using a gem called `rqrcode` to do most of the heavy lifting for us[^how_qr_codes_work].

[^how_qr_codes_work]: If you're curious how QR codes actually work, you can [read up on them here](https://typefully.com/DanHollick/qr-codes-T7tLlNi){:target="_blank"}; but fortunately the gem encapsulates all of this logic for us.

## Explore the target

There is a solution in the file called `solution.rb`. To see how it behaves, first we must install the rqrcode gem. At a command prompt:

```
gem install rqrcode
```

Then, run the solution (`ruby solution.rb`) to explore how your program should work. (Don't peek at the solution code until you've tried some things on your own.)

You should notice a few things about the final solution:

- The program gives you four options: to generate QR codes for URLs, wifi networks, and text messages; and to exit the program.
- If you select `4`, the program ends.
- If you select `1`, `2`, or `3`, the program creates a PNG file that contains a QR code.
- Try typing in an option that the program doesn't expect (i.e., not `1`, `2`, `3`, or `4`); how does it handle it?

## Hello world

Create a file to write the program in. I called mine `qr.rb`.

Add some code to print "hello world" and ensure that you can run the program without any issues.

At a command prompt, `bin/server`. Visit `/git` and make a commit. Push your changes back to GitHub.

Keep the `/git` page open in a tab. As you work, continue to make commits and push them.

## Install the rqrcode gem

To get access to the `rqrcode` gem, at a command prompt:

```
gem install rqrcode
```

## Using the rqrcode gem

The rqrcode gem has a lot of different options[^rqrcode] for rendering QR codes — as PNG files, as `<svg>` elements, and more.

[^rqrcode]: If you're curious, you can read about them in [the gem's README file](https://github.com/whomwah/rqrcode){:target="_blank"}.

For now, we're going to render PNG images only. To do so, here's how it works:

```ruby
require "rqrcode"

# Use the RQRCode::QRCode class to encode some text
qrcode = RQRCode::QRCode.new("wikipedia qr code")

# Use the .as_png method to create a 500 pixels by 500 pixels image
png = qrcode.as_png({ :size => 500 })

# Write the image data to a file
IO.binwrite("sometext.png", png.to_s)
```

Try adding the above code to your program and run it. You should see a file pop up in your file tree called `sometext.png`.

If you open that file and scan it with your phone's camera, it should offer to search for the text we encoded. Neat!

## Encoding URLs

If you provide a fully-qualified URL as the text to be encoded (starting with `https` or `http`) then most phones will offer to take you directly to the URL when the QR code is scanned. Try updating your code with a URL instead:

```ruby
qrcode = RQRCode::QRCode.new("https://en.wikipedia.org/wiki/QR_code")
```

Try scanning the generated image with your phone. Did it work?

## Join a wifi network

If you want the QR code to automatically join a wifi network, then you must encode text in the following format:

```
WIFI:T:WPA;S:My wifi network;P:supersecretpassword;;
```


In the above example, `My wifi network` is the name of the network to be joined, and `supersecretpassword` is the password for that network. Replace them with the actual network name and password that you want to generate a QR code for.

Give it a try. Did the generated image work?

## Send a text message

If you want the QR code to pre-populate a text message, then you must encode text in the following format:

```
SMSTO:9876543210:Hi Alice! It's
```

- No spaces are allowed in the phone number.
- You can include country codes, e.g. `+19876543210`.

In the above example, when the QR code is scanned it will open the messages app with the message `Hi Alice! It's` and phone number `(987) 654-3210` pre-filled.

Give it a try. Did the generated image work?

## Suggested steps

Before reading further, you can and should attempt to write the program on your own. How can you break the program down into tiny little steps?

Once you get stuck (that might not take long), then read on for some suggestions:

### Make the program interactive

Write some code that prompts the user to enter a URL of their choice.

Then use their input to generate the QR code dynamically.

### Give your user options

Write some code that first prompts the user to select whether they want a URL, wifi network, or text message to be encoded in the QR code.

Depending on their selection, prompt them further for the information you need to generate the QR code.

Then use their input to generate the QR code dynamically.

### Stretch goal: make the program loop until exited

Optionally, write some code that will keep generating QR codes until the user chooses to exit.

The `while`, `next`, and `break` keywords might come in handy. [Read more here.](https://www.geeksforgeeks.org/ruby-break-and-next-statement/){:target="_blank"}

## To submit

Submit the URL of your GitHub repository. You can keep pushing up commits after the due date in case you add more features.
