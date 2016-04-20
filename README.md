# facebookDemo - David Bernstein

##Introduction
As promised in the Tufts University Comp 20 (Web Development) class, here is a short tutorial/demo for how to use the Facebook API using front-end javascript. I do not claim to be an expert in it, but after many weeks of working with the API, I can safely say that I am fairly familiar with the fundamentals of the site. Feel free to copy and paste code directly from this tutorial; I know how hard it is to find code about the Facebook API that makes sense (though please do cite the code accordingly!).

## Initial Setup
So the first thing we want to do is actually set up the app through Facebook! Start by going to [www.developers.facebook.com](www.developers.facebook.com). Click on quick start, choose www (web), and you'll presented with this page: [image1]. Give a name, category, etc., and you'll eventually get your app ID (super important number, don't give it away willy nilly!). When you scroll down, you'll see this code for setting up the Facebook SDK for Javascript:

```html
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
</script>
```

