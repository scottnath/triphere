---
layout: page
title: About2
permalink: /about2/
---

## this page is test code for a facebook feed
<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '353075521483775',
      xfbml      : true,
      version    : 'v2.2'
    });
// FB.api('/113124472034820', function(response) {
//   console.log(response);
// });
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "//connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
function apitest(){

  FB.api(
      "/10152301012256776/home",
      function (response) {
    console.log(response);
        if (response && !response.error) {
          /* handle the result */
        }
      }
  );
}
function facebookLogin(){
    FB.login(function(response){
        if (response.authResponse) {
            console.log('Welcome! Fetching your information');
            FB.api('/me', function(response) {
                console.log('Good to see you, ' + response.name + '.');
            });

            console.log(response);
        } else {
            console.log('User cancelled login or did not fully authorize.');
        }
    });
}

</script>

<a href="javascript:facebookLogin();">Login</a>
<a href="javascript:apitest();">apitest</a>

<script>
  // This is called with the results from from FB.getLoginStatus().
  function statusChangeCallback(response) {
    console.log('statusChangeCallback');
    console.log(response);
    // The response object is returned with a status field that lets the
    // app know the current login status of the person.
    // Full docs on the response object can be found in the documentation
    // for FB.getLoginStatus().
    if (response.status === 'connected') {
      // Logged into your app and Facebook.
      testAPI();
    } else if (response.status === 'not_authorized') {
      // The person is logged into Facebook, but not your app.
      document.getElementById('status').innerHTML = 'Please log ' +
        'into this app.';
    } else {
      // The person is not logged into Facebook, so we're not sure if
      // they are logged into this app or not.
      document.getElementById('status').innerHTML = 'Please log ' +
        'into Facebook.';
    }
  }

  // This function is called when someone finishes with the Login
  // Button.  See the onlogin handler attached to it in the sample
  // code below.
  function checkLoginState() {
    FB.getLoginStatus(function(response) {
      statusChangeCallback(response);
    });
  }

  window.fbAsyncInit = function() {
  FB.init({
    appId      : '353075521483775',
    cookie     : true,  // enable cookies to allow the server to access 
                        // the session
    xfbml      : true,  // parse social plugins on this page
    version    : 'v2.2'
  });

  // Now that we've initialized the JavaScript SDK, we call 
  // FB.getLoginStatus().  This function gets the state of the
  // person visiting this page and can return one of three states to
  // the callback you provide.  They can be:
  //
  // 1. Logged into your app ('connected')
  // 2. Logged into Facebook, but not your app ('not_authorized')
  // 3. Not logged into Facebook and can't tell if they are logged into
  //    your app or not.
  //
  // These three cases are handled in the callback function.

  FB.getLoginStatus(function(response) {
    statusChangeCallback(response);
  });

  };

  // Load the SDK asynchronously
  (function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/sdk.js";
    fjs.parentNode.insertBefore(js, fjs);
  }(document, 'script', 'facebook-jssdk'));

  // Here we run a very simple test of the Graph API after login is
  // successful.  See statusChangeCallback() for when this call is made.
  function testAPI() {
    console.log('Welcome!  Fetching your information.... ');
    FB.api('/me', function(response) {
      console.log('Successful login for: ' + response.name);
      document.getElementById('status').innerHTML =
        'Thanks for logging in, ' + response.name + '!';
    });
  }
</script>

<!--
  Below we include the Login Button social plugin. This button uses
  the JavaScript SDK to present a graphical Login button that triggers
  the FB.login() function when clicked.
-->

<fb:login-button scope="public_profile,email" onlogin="checkLoginState();">
</fb:login-button>

<div id="status">
</div>
<!-- <div id="fbactivityfeedhtml5">
  <div
    class="fb-activity"
    data-action="{{ action }}"
    data-colorscheme="{{ colorscheme }}"
    data-filter="{{ filter }}"
    data-header="{{ showheader }}"
    data-height="{{ height }}"
    data-linktarget="{{ linktarget }}"
    data-max-age="{{ maxage }}"
    data-recommendations="{{ recommendations }}"
    data-ref="{{ ref }}"
    data-site="{{ site }}"
    data-width="{{ width }}"
  ></div>
</div>
<div
  class="fb-like"
  data-share="true"
  data-width="450"
  data-show-faces="true">
</div> -->