# Sending emails and text messages

## Example of how to send an email with the Mailgun gem

Mailgun has written a class called `Mailgun::Client` which has an amazing method called `.send_message`, so you can do something like this:

```ruby
mg_client.send_message(mg_sending_domain, email_info)
```

And it will do all the heavy lifting to interact with the Mailgun API and deliver an email!

Some setup is required first to get the instance of `Mailgun::Client` ready:

### Add the gem

#### In a Ruby program

At a command prompt:

```
gem install mailgun-ruby
```

In your program:

```ruby
require "mailgun-ruby"
```

#### In a Rails app

In your `Gemfile`, add:

```ruby
gem "mailgun-ruby"
```

Then, at a Terminal prompt:

```bash
bundle install
```

### Usage

```ruby
# Get your credentials from your Mailgun dashboard, or from Canvas if you're using mine
mg_api_key = "your-api-key"
mg_sending_domain = "your-sending-domain"

# Create an instance of the Mailgun Client and authenticate with your API key
mg_client = Mailgun::Client.new(mg_api_key)

# Craft your email as a Hash literal with these four keys
email_info =  { 
  :from => "umbrella@appdevproject.com",
  :to => "put-your-own-email-address-here@example.com",  # Put your own email address here if you want to see it in action
  :subject => "Take an umbrella today!",
  :text => "It's going to rain today, take an umbrella with you!"
}

# Send your email!
mg_client.send_message(mg_sending_domain, email_info)
```

Voilà! Check your email.

 - **Important:** before you push your code to GitHub, please be sure to [store your Mailgun credentials securely](https://chapters.firstdraft.com/chapters/792){:target="_blank"}, and replace the strings containing your API credentials with something like `ENV.fetch("MAILGUN_API_KEY")`.

## Example of how to send an SMS with the Twilio gem

Twilio has written a class called  `Twilio::REST::Client` class which has a bunch of amazing telephony-related methods, including:

```ruby
twilio_client.api.account.messages.create(sms_info)
```

Which will do all the heavy lifting to interact with the Twilio API and deliver a text message!

Some setup is required first to get the instance of `Twilio::REST::Client` ready:

### Add the gem

#### In a Ruby program

At a command prompt:

```
gem install twilio-ruby
```

In your program:

```ruby
require "twilio-ruby"
```

#### In a Rails app

In your `Gemfile`, add:

```ruby
gem "twilio-ruby"
```

Then, at a Terminal prompt:

```bash
bundle install
```

### Usage

```ruby
# Get your credentials from your Twilio dashboard, or from Canvas if you're using mine
twilio_sid = "your-account-sid"
twilio_token = "your-auth-token"
twilio_sending_number = "your-sending-number"

# Create an instance of the Twilio Client and authenticate with your API key
twilio_client = Twilio::REST::Client.new(twilio_sid, twilio_token)

# Craft your SMS as a Hash literal with three keys
sms_info = {
  :from => twilio_sending_number,
  :to => "+19876543210", # Put your own phone number here if you want to see it in action
  :body => "It's going to rain today — take an umbrella!"
}

# Send your SMS!
twilio_client.api.account.messages.create(sms_info)
```

Voilà! Check your phone.

 - Sign up for your own Twilio account — [if use this referral link you'll $10 in credit](https://www.twilio.com/referral/86ykDX), and so will our class account.
 - [Twilio Ruby Quickstarts](https://www.twilio.com/docs/quickstart/ruby)
 - **Important:** before you push your code to GitHub, please be sure to [store your Twilio credentials securely](https://chapters.firstdraft.com/chapters/792){:target="_blank"}, and replace the strings containing your API credentials with something like `ENV.fetch("TWILIO_ACCOUNT_SID")`.

---

Have fun!
