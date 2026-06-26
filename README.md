## Current development setup:

### Data to be stored in NFC URI field:

https://chrisrice.github.io/device?apName=Wispr-E44D05&password=gobadgers

### Content of JSON required in /root/.well-known/apple-app-site-association

{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "Z5GXLHSZ6G.com.MPR.BadgerImageClient4",
        "paths": ["/device*"]
      }
    ]
  }
}

### Content of /root/device/Index.html 
Which will be the "fallback" if the iPhone can't
load the app. the below launches the instagram page in the app store, to be replaced
with our app store page.

<!DOCTYPE html> 
<html lang="en"> 
  <head> 
    <meta charset="utf-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1"> 
    <title>Wispr</title> 
  </head> 
  <body> 
    <p>Opening Wispr…</p> 

    <!--
    <p><a id="store"href="https://apps.apple.com/app/idYOURAPPID">Get Wispr on the App Store</a></p> 
    -->
    <p><a id="store"href="https://apps.apple.com/us/app/instagram/id389801252">Get Wispr on the App Store</a></p> 
    <script> 
      // Forward to the App Store. (Replace with your real App Store URL/ID.)
      window.location.replace("https://apps.apple.com/us/app/instagram/id389801252");
      // window.location.replace("https://apps.apple.com/app/idYOURAPPID"); 
    </script> 
  </body> 
</html>

### Important Notes 
* See SceneDelegate.swift, "scene" functions for code that handles the incoming APName and password parameters.
* The app also requires the "Associated Domains" capability, configured with the domain "applinks:chrisrice.github.io?mode=developer". See target settings, Signing and Capabilities for this config
* The "mode=developer" parameter allows use of github, which might not provide JSON format as apple is looking for.  development mode is format-friendlier
* This mode requires the phone setting "Developer->Associated Domains Development" to be checked.  In production with a real website, we should remove mode=developer and shouldn't need to switch the developer iPhone setting.
