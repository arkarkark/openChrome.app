# openChrome.app

Opens URLs in various chrome profiles/users based on pattern matching.

If you install [SwiftDefaultApps](https://github.com/Lord-Kamina/SwiftDefaultApps/releases) you can set this app as your default URL opener.

## ~/.openchromerc

You must set up a ~/.openchromerc file. It's a JSON format file like this:

```json
{
  "rules": [
    {"run": ["/usr/local/bin/transmission-remote", "btserver:8347", "--add", "%(url)s"], "pattern": "^magnet:"},
    {"email": "user-faceboook@example.com", "pattern": "(facebook.com/|fb.me/)"},
    {"email": "user@work.example.com",      "pattern": "(work.example.com|(docs|drive).google.com/)"},
    {"email": "user@example.com"}
  ]
}
```

If the url being opened matches the first rule's pattern, it will be opened in the chrome profile that is logged in to the `user-facebooke@example.com` Google account. etc...
The last rule is a catch all for all urls that don't match.

If you have profiles that are not logged into a Google account then you can use `"profile": "Profile 1"` rather than `"email": "..."` in a rule entry.

You can also specify `profileDirectory` and `chromeBinary` in the `~/.openchromerc` configuration object.

If you want to run a shell command rather than open Chrome then use `run` rather than `email`.

## The script

You might be able to use [openChrome http://facebook.com/](Contents/Resources/Scripts/openChrome) from the command line on a unix/linux system. Indeed this is a good script to run if you are having configuration problems. You probably forgot a comma at the end of a line or have one extra (grrr... JSON).

## History

I use at least three chrome user profiles, one for personal stuff, one for facebook (to keep the tracking down and to make it easy to switch to) and one for my work stuff. Oftentimes links from Slack or Adium open up in the last profile I was using which is usually the wrong one. Setting this script as my system URL opener makes sure the URLs open in the right chrome profile most of the time.

This all came about because of https://crbug.com/549275
I also used help from here:
http://superuser.com/questions/373701/create-bash-script-to-open-url-in-mac-os-x
http://apple.stackexchange.com/questions/32386/how-to-register-an-applescript-as-a-potential...
