# facebookDemo - David Bernstein
Last Updated: April 20, 2016

##Introduction
As promised in the Tufts University Comp 20 (Web Development) class, here is a short tutorial/demo for how to use the Facebook API using front-end javascript. I do not claim to be an expert in it, but after many weeks of working with the API, I can safely say that I am fairly familiar with the fundamentals of the site. Feel free to copy and paste code directly from this tutorial; I know how hard it is to find code about the Facebook API that makes sense (though please do cite the code accordingly!).

## Initial Setup
So the first thing we want to do is actually set up the app through Facebook! Start by going to [www.developers.facebook.com](www.developers.facebook.com). Click on quick start, choose www (web), and you'll presented with this page: ![QuickStartPage](https://github.com/davidrocks88/facebookDemo/blob/master/img/QuickStartPage.png?raw=true) Give a name, category, etc., and you'll eventually get your app ID (super important number, don't give it away willy nilly!). When you scroll down, you'll see this code for setting up the Facebook SDK for Javascript:

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

Copy and paste this code into an HTML file, load it up, and there we go! Facebook has loaded! Exciting, right?! Well, not exactly. nothing has really happened yet, all you've done is loaded the SDK. Before moving forward, make sure that you scroll down to the part which asks about which url you are using. ![URL: Change it to localhost:8000](https://github.com/davidrocks88/facebookDemo/blob/master/img/URL.png?raw=true) I chose to use http://localhost:8000 since that's where I'm hosting my content, but when you are actually hosting content on a website on the web, change this url!

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
Not too bad, right? A simple javascript callback function. But how do you actually implement this into your code, you ask? Well, as an example, I puth the script into a functin and made a button that, when clicked, would log in the user. The code is as follows:
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
When you load the page, all you will see is this:![Homepage with only login button](https://github.com/davidrocks88/facebookDemo/blob/master/img/OneButton.png?raw=true)
When you click the login button, though, you get this wonderul popup:![QuickStartPage](https://raw.githubusercontent.com/davidrocks88/facebookDemo/master/img/initalLogin.png)
After saying yes, then letting the app have the appropriate permissions, you should be all set with the basics!

## Doing useful things with the API: User Info
One of the best uses for the API is to get unique user information, which means that you personally do not have to generate user IDs or handle any secure login, which is extremely convenient! One should note that every Facebook user has a unique identifier. You can actually copy your own identifier, go to facebook.com/[identifier], and you'll see your home page pop up! 
So, how do you get user info? Well, we can use this handy little script here:

```js
  FB.api('/me', 'GET', {fields: 'first_name,last_name,name,id'}, function(response) {
          alert("Hello, " + response.first_name + " " + response.last_name + ", ID #" + response.id);
  });
```
Lets examine this code briefly. The API usually has the parameters of path (aka /me, who is the current person logged in), the action (in this case, we are doing a 'GET' action), some parameters (in this case, what info you want to get back), and a callback function with what you want to do with the response you get from Facebook. In practice, this is what my HTML code looks like now:
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
function getInfo() {
  FB.api('/me', 'GET', {fields: 'first_name,last_name,name,id'}, function(response) {
          alert("Hello, " + response.first_name + " " + response.last_name + ", ID #" + response.id);
  });
}
</script>
<button onclick="login()"> login </button>
<button onclick="getInfo()"> getInfo </button>
</body>
</html>
```

When you open it, notice that after you click the login button, it'll automatically log you in! Next, when you press the getInfo button, you can see your first name, last name, and id number!
![Page with getInfo button](https://github.com/davidrocks88/facebookDemo/blob/master/img/getInfo.png?raw=true)

From here, most people have what they need from Facebook; a secure way to have unique users log in. I'll briefly go into posting to the user's Facebook wall, but most readers can stop reading here!

## Posting to a User's wall
The code for this is fairly simple too, and can be found on the developers page (though some digging might be required).
```js
        var msg = prompt("give me a post!", "example");
        FB.api('/me/feed', 'post', { message: msg }, function(response) {
          if (!response || response.error) {
            alert('Error occured');
          } else {
            alert('Post ID: ' + response.id);
          }
        });
```
Let's quickly dissect this code. First, we get a message that we want to post to the user's wall. Then we make a call to the api, where the path is the user's home feed (/me/feed), the action is post, the parameters are the message (and nothing else), and we have a callback function outlining what happens when a post works correctly. 
After putting this code into a new friendly button function, this is what the code finally looks like:
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
function getInfo() {
  FB.api('/me', 'GET', {fields: 'first_name,last_name,name,id'}, function(response) {
          alert("Hello, " + response.first_name + " " + response.last_name + ", ID #" + response.id);
  });
}

function post() {
        var msg = prompt("give me a post!", "example");
        FB.api('/me/feed', 'post', { message: msg }, function(response) {
          if (!response || response.error) {
            alert('Error occured');
          } else {
            alert('Post ID: ' + response.id);
          }
        });
    }
</script>
<button onclick="login()"> login </button>
<button onclick="getInfo()"> getInfo </button>
<button onclick="post()"> post </button>
</body>
</html>
```

When you reload the page, you'll see three buttons there! Make sure to test the login and getInfo buttons to make sure they're working. Finally, click the post button. You'll be prompted like this: ![Post prompt example](https://github.com/davidrocks88/facebookDemo/blob/master/img/postExample.png?raw=true) 
Fill in the box, hit enter, and if it works, you'll get a post ID! Now, go check your Facebook wall. I'll wait......
Did you see that?! It worked! You can now post to a client's wall! You can also do a bunch of other cool stuff with posting to user's walls too, such as links and whatnot (however, posting images is a different monster, as you'll see in the authorization section).

## Authorization
Authorization is tricky with Facebook. You only get the most basic permissions at the beginning, and if you want more permissions, you have to make a request to Facebook directly using the app dashboard that we saw in the beginning. Things such as posting pictures, for instance, will require you to do things like that. After getting the appropriate permissions, you have to then add extra parameters to the appropriate API call, such as access tokens and {scope: 'publish_actions'}. Let me know if you have any questions, and I'll try to help you the best I can.

## Concluding Notes
The Facebook API can be...finicky, at times. The learning curve is somewhat steep at the beginning, but hopefully after this tutorial, you'll be a master at it! Feel free to contact me if you have any questions! Otherwise, happy coding!






