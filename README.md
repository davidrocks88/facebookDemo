# facebookDemo - David Bernstein

##Introduction
As promised in the Tufts University Comp 20 (Web Development) class, here is a short tutorial/demo for how to use the Facebook API using front-end javascript. I do not claim to be an expert in it, but after many weeks of working with the API, I can safely say that I am fairly familiar with the fundamentals of the site. Feel free to copy and paste code directly from this tutorial; I know how hard it is to find code about the Facebook API that makes sense (though please do cite the code accordingly!).

## Initial Setup
So the first thing we want to do is actually set up the app through Facebook! Start by going to [www.developers.facebook.com](www.developers.facebook.com). Click on quick start, choose www (web), and you'll presented with this page: ![QuickStartPage](https://github.com/davidrocks88/facebookDemo/blob/master/QuickStartPage.png?raw=true). Give a name, category, etc., and you'll eventually get your app ID (super important number, don't give it away willy nilly!). When you scroll down, you'll see this code for setting up the Facebook SDK for Javascript:

```html
<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '[your app id]',
      xfbml      : true,
      version    : 'v2.6'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "//connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>
```

Copy and paste this code into an HTML file, load it up, and there we go! Facebook has loaded! Exciting, right?! Well, not exactly. nothing has really happened yet, all you've done is loaded the SDK. Before moving forward, make sure that you scroll down to the part which asks about which url you are using. ![URL: Change it to localhost:8000](https://github.com/davidrocks88/facebookDemo/blob/master/URL.png?raw=true). I chose to use http://localhost:8000 since that's where I'm hosting my content, but when you are actually hosting content on a website on the web, change this url!

So far, this is the HTML I have:
```html
<!doctype html> 
<html>
<head>
  <title>facebookDemo</title>
</head>
<body>
<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '[your app id]',
      xfbml      : true,
      version    : 'v2.6'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "//connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>

</body>
</html>

```

## Loggin' In
So naturally, the first thing we want to do is let the user log in to Facebook. The cool thing about this is that once a user logs in, they won't have to log in again! The code for logging in can be found in the Facebook API, but you can just copy and paste this code to make your life easier:

```js
FB.login(function(response) {
                if (response.status === 'connected') {
                    alert("connected");
                } else if (response.status === 'not_authorized') {
                    alert("not authorized");
                } else {
                    alert('You are not logged into Facebook.');
                }
            });

```
Not too bad, right? A simple javascript callback function. But how do you actually implement this into your code, you ask? Well, as an example, I made a button that, when clicked, would log in the user. The code is as follows:
```html
<!doctype html> 
<html>
<head>
  <title>facebookDemo</title>
</head>
<body>
<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '1674115936182026',
      xfbml      : true,
      version    : 'v2.6'
    });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "//connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));


function login() {
            FB.login(function(response) {
                if (response.status === 'connected') {
                    alert("connected");
                } else if (response.status === 'not_authorized') {
                    alert("not authorized");
                } else {
                    alert('You are not logged into Facebook.');
                }
            });
        }
</script>
<button onclick="login()"> login </button>
</body>
</html>
```
When you load the page, all you will see is this:![Homepage with only login button](https://github.com/davidrocks88/facebookDemo/blob/master/OneButton.png?raw=true).

