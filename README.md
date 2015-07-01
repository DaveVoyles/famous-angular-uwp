# famous-angular-uwp
### Author(s): Dave Voyles | [@DaveVoyles](http://www.twitter.com/DaveVoyles)
### URL: [www.DaveVoyles.com][1]

Turn a famous + angular web application into a Windows 10 UWP App
----------
### Objective

- *[Download the finished version of this tutorial. Open with Visual Studio](https://github.com/DaveVoyles/Famous-Angular-Pokemon-Cordova)*
- *[View the project in your browser](http://famous-angular-pokemon.azurewebsites.net/app/#/)*
- *[Tutorial for the web portion of the project](https://github.com/DaveVoyles/famous-angular-Pokemon/blob/master/README.md)*

I love high performance JavaScript, and have faith that others will finally come around and understand its true potential someday too. Famo.us allows you to maintain a silky smooth 60 Frames Per Second while having fluid animations on screen. Famo.us does this by utilizing the CSS3 primitive -webkit-transform: matrix3d, which lets the framework compute the composite matrix and skip the browser’s renderer. No plug-in, no download, no hack. By appending this to each DIV, developers can render the composite matrix and go straight to the GPU. Even better, we can have this running on mobile devices.

I go more in depth when discussing the ins-and-outs of Famo.us in an [earlier blog post.](http://www.davevoyles.com/creating-a-mobile-app-with-famo-us-and-manifoldjs/) 

### By the end of this project you will be able to:

- Understand how to turn a web application into a hybrid Windows 10 application that takes advantage of the Universal Windows Platform.

My goal for this project to illustrate how easily you can create HTML5 / JS projects which work at near native speeds on mobile / desktop applications. 


### Requirements
- [Visual Studio 2015 or 2013](https://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx) 
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Windows 10 SDK (Included with Visual Studio).](https://dev.windows.com/en-us/downloads/windows-10-developer-tools)
- [Visual Studio Tools for Cordova](https://msdn.microsoft.com/en-us/library/dn771545.aspx)


### Setup
 1.  Download the source from [GitHub](https://github.com/DaveVoyles/Famous-Angular-Pokemon-Cordova)
 2.  Install the [Git Command Line Iterface (CLI)](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
 3.  Install [Visual Studio 2015 or 2013](https://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx) 
 3.  Install [Windows 10 SDK (Included with Visual Studio).](https://dev.windows.com/en-us/downloads/windows-10-developer-tools) 
 4.  Install - [Visual Studio Tools for Cordova](https://msdn.microsoft.com/en-us/library/dn771545.aspx) 
 
 **NOTE:** You can find the project this is based off of (just the web stuff) [here.](https://github.com/DaveVoyles/famous-angular-Pokemon)


---------
### Building Cordova from the CLI
The Cordova website offers some [excellent docs](https://cordova.apache.org/docs/en/4.0.0/guide_cli_index.md.html) on how to do this, but I'll dive into a bit of detail to explain how some of it works. 

The first thing you'll want to do is [download the finished web project from my GitHub repo.](https://github.com/DaveVoyles/famous-angular-Pokemon). From there, we'll need to create the app using the Cordova CLI (Command Line Interface). 

### Creating the app
I'm going to start from the path *Users/DaveVoyles/Documents*. If you aren't comfortable with using the CLI or Terminal in OSX, I'd suggest watching this [6 minute YouTube video](https://www.youtube.com/watch?v=YRuK2cJ9GI4) which provides a great overview and explains some of the terms I'll be using. 

To navigate here you can enter the Change Directory command (cd) in the Terminal, then *drag* the folder you want to start in:

```
cd <drag your folder from the Finder app into here>
```

Then press enter. We are now working out of this folder. We need to make a folder to hold this content, so enter this command first:

```
mkdir FamousCordova
```

This will create a new directory (folder) at our current location and name it 'FamousCordova'. We need to navigate into that folder now, as this will be our starting point for creating the project.

```
cd FamousCordova
```
Let's actually create the Cordova project now: 

```
cordova create PokemonApp PokemonApp
```

It looks like of funny because I entered *PokemonApp* twice, right? The first time, I am creating a project called "PokemonApp". The second time I enter it, I am entering the display title, which is what you see at the top of your app inside of the iOS emulator. This argument is optional. 

![](https://dl.dropboxusercontent.com/s/mcaybz08cks2ndp/Screenshot%202015-06-26%2010.32.16.png?dl=0)


### Adding the iOS platform
We've got our first project! But we still need to add inidividual platforms. Let's add iOS right now. 

First, we need to navigate into the PokemonApp folder:

```
cd PokemonApp
```

Now add the iOS platform:

```
cordova platform add ios
```

![](https://dl.dropboxusercontent.com/s/fiedvrswxkcywgb/Screenshot%202015-06-26%2010.36.39.png?dl=0)

We've now got some new items in our platforms folder! One more step and we'll have this project running. Let's emulate the app on iOS:

```
cordova emulate ios
```

![](https://dl.dropboxusercontent.com/s/kp60hx7ckjovevc/Screenshot%202015-06-26%2010.45.35.png?dl=0)

You'll see it throw a bunch of text within the terminal. If all went well, we should see **BUILD SUCCEEDED**. This command combines a few steps into one. 

First, it is performing the build process, which is shorthand for:

```
cordova prepare ios
cordova compile ios
```

Finally the *emulate* command tells the simulator from within Xcode to boot up and executes our application.

### Merging content from our web project

#### Combining index.html
You'll notice that our *www* folder is essentially a website. It's got folders for *css img* and *js*. What we're doing to do here is combine this project with our own.

Rename  the Cordova *index.html* in our www folder to *bu_index.html* (short for Back Up). Copy *index.html* from the project we downloaded earlier, and paste it into the www folder. 

We are going to start by copying some of the meta tags from *bu_index.html* Grab these tags and paste them into your *index.html* file:

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *">
<meta name="format-detection"              content="telephone=no">
<meta name="msapplication-tap-highlight"   content="no">
<meta name="viewport"                      content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width">

<link rel="stylesheet" type="text/css" href="css/index.css">
```

Do the same for the two Javascript files at the bottom of the body:

```html
<script type="text/javascript" src="cordova.js"></script>
<script type="text/javascript" src="js/index.js"></script>
```

#### Copying over the folders 
Add the prefix *bu_* to all of the folders found inside of www (css, img, js).

Copy the folders from our downloaded web project into www (*images, partials, scripts, styles, bower_components*). Also grab the *bower_components* folder found outside of the *app* folder. So in the end, you should have two (2) *bower_components* folders, and the structure should look like this:

```
- bower_components
- www
    - bu_css
    - bu_img
    - bu_js
    - bu_index.html
    - images
    - partials
    - scripts
    - styles
    - index.html
 - config.xml
```

Many of these folders mean the same thing (ex: Style & css or Scripts and js), but I wanted to keep with the naming convention that I had for the previous project. It doesn't matter what you name the folder, as long as you correct the references to those files within your index.html file. So if we move a file from the *css* folder and place it in the *styles* folder, we need to make sure that we also update our *index.html* file which is pointing to that file!

#### Copying files between folders
1. Copy *index.js* from *bu_js* into the *scripts* folder
2. Copy *logo.png* from *bu_img* into the *images* folder
3. Copy *index.css* from *bu_css_ into the *styles* folder

You can now delete the folders with the *bu_* prefix, as well as *bu_index.html*. Your folder structure should now look like this:

```
- bower_components
- www
    - images
    - partials
    - scripts
    - styles
    - index.html
 - config.xml
```

#### Fixing the references within *index.html*
Since we've moved our css and js files from their original location in the Cordova project, we need to update their location (reference to them) within our index.html file. They should now read:

``` html
<link rel="stylesheet" type="text/css" href="styles/index.css">
<script type="text/javascript" src="cordova.js"></script>
<script type="text/javascript" src="scripts/index.js"></script>
```

I know what you're thinking: 
"Where did *cordova.js* come from? I don't see that file!"

That's because Cordova actually generates that file for us when we build the project, and it then places it in the folder for us. We won't ever see it.

Your index.html should now look like this:

``` html
<!doctype html>
<html class="no-js" ng-app="famousAngularStarter">
  <head>
    <meta charset="utf-8">
    <title>Famo.us/Angular</title>

    <!-- Cordova --> 
    <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: http://pokeapi.co/ http://img.pokemondb.net gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *">
    <meta name="format-detection"              content="telephone=no">
    <meta name="msapplication-tap-highlight"   content="no">
    <meta name="viewport"                      content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width">
    <meta name="description"                   content="">
    <meta name="viewport"                      content="width=device-width">
    <!-- Place favicon.ico and apple-touch-icon.png in the root directory -->

    <!-- build:css styles/vendor.css -->
    <!-- bower:css -->
    <!-- endbower -->
    <!-- endbuild -->

    <!-- build:css({.tmp,app}) styles/main.css -->
    <link rel="stylesheet" href="styles/main.css">
    <!-- endbuild -->
    <link rel="stylesheet" href="bower_components/famous-angular/dist/famous-angular.css">
    <!-- Cordova -->
    <link rel="stylesheet" type="text/css" href="styles/index.css">

  </head>
  <body>

    <div ui-view></div>

    <script src="bower_components/angular/angular.js"></script>
    <script src="bower_components/angular-animate/angular-animate.js"></script>
    <script src="bower_components/angular-cookies/angular-cookies.js"></script>
    <script src="bower_components/angular-touch/angular-touch.js"></script>
    <script src="bower_components/angular-sanitize/angular-sanitize.js"></script>
    <script src="bower_components/angular-resource/angular-resource.js"></script>
    <script src="bower_components/angular-ui-router/release/angular-ui-router.js"></script>
    <script src="bower_components/angular-route/angular-route.js"></script>

    <script src="bower_components/underscore/underscore.js"></script>
    <script src="bower_components/famous/famous-global.js"></script>
    <script src="bower_components/famous-angular/dist/famous-angular.js"></script>


    <!-- build:js({app,.tmp}) scripts/main.js -->
    <script src="scripts/famousAngularStarter.js"></script>
    <script src="scripts/main/main-ctrl.js"></script>
    <script src="scripts/main/pokemon.js"></script> 
    <!-- inject:partials -->
    <!-- Cordova --> 
    <script type="text/javascript" src="cordova.js"></script>
    <script type="text/javascript" src="scripts/index.js"></script>
    <!-- endinject -->
    <!-- endbuild -->

  </body>
</html>
```

### Cordova's strict security settings
You may have noticed that my line for *http-equiv* looks slightly different than yours:

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: http://pokeapi.co/ http://img.pokemondb.net gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *"
```

This is because I added a few references to external URLs, such as the pokeAPI and pokemonDB. If you try to build your project now, it will work up until the point where you try to retreive information from the database.

![](https://dl.dropboxusercontent.com/s/5ryhvtvak2cn87y/Screenshot%202015-06-26%2012.02.17.png?dl=0)

The error reads "Couldn't get Pokemon from the Database" (the Database part is obscured by the image). This is because of Cordova's strict security settings. Let's try to debug this.

### Using Safari's remote debugger
Apple's Safari browser allows us to create a remote connection to the iOS Simulator and debug our Cordova app, becuase the app is running within a webview in iOS. 

In short, open up Safari in OS X, and navigate to **Safari -> Preferences ->  Advanced**, check the *Show Develop Menu* in the menu bar checkbox. This article explains [how to remote debug using your physical device](http://moduscreate.com/enable-remote-web-inspector-in-ios-6/), as well. 

Let's emulate the app in iOS again, and we can connect the remote debugger. 

```
cordova emulate iOS
```

The iOS simulator should be up again. At the top of your Safari window, you will see a new tab for *Develop*. cick on **Develop -> iOS Simlator -> Index.html** and you'll see the Web Inspector window pop-up.  

![](https://dl.dropboxusercontent.com/s/8vfrdxy7fzq32hz/Screenshot%202015-06-26%2017.11.05.png?dl=0)

Now hit the *Next* button in the Pokemon app and you'll receive the error again, but let's see what the response from the console is. In the Web Inspector, click on the red ! icon towards the top of the application. This will bring us to the errors generated in the console.

![](https://dl.dropboxusercontent.com/s/isispm8172c85xz/Screenshot%202015-06-26%2017.15.31.png?dl=0)

This says it all. THe call to the pokemon API is violating the [Content Security Policy](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), which for right now, can only grab information from the files we have stored on the device itself. That's what the 'self' text is telling us.

Let's resolve that by altering our Content Security Policy, which we've set in the head of our index.html file.
Add the URLs for the pokemon API and the DB.

```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: http://pokeapi.co/ http://img.pokemondb.net gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *">
```

Let's emulate the iOS app again.

```
cordova emulate ios
```

Now hit the *Next* button and watch as a new Pokemon appears!

![](https://dl.dropboxusercontent.com/s/qh1hhjm37k0ecrm/Screenshot%202015-06-26%2017.21.36.png?dl=0)

### Conclusion
That's all there is to it. You have a fully functioning Cordova app made for iOS. In the next lession I'll cover how to do this on Windows with Visual Studio, where we can debug Windows Phone, Android, and even iOS. 




----------
## Resources

- [Famo.us Slackchat ](http://famous.org/support/)
- [BizSpark, for free MSFT dev licenses and web hosting](http://davevoyles.azurewebsites.net/bizspark-free-software-cloud-services-o/)
- [E-mail me with questions](mailto:Dvoyles@microsoft.com "Dvoyles@microsoft.com")

----------

##Change Log
###v1.0.0
Initial build of the app


  [1]: http://www.daveVoyles.com "My website"
