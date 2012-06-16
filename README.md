jquery.mobile.smooth.scrollTo
============================= 

Using the files provided in this repo will give you more than just the smooth scrollTo that you may or may not have seen in one of the video demonstrations I posted on vimeo.  The jquery.mobile.defaults.overrides.js and jquery.mobile.structure.overrides.css files pretty much completely override most if not all of the CSS3 for the transitions as well as the sequential and simultaneous transition handlers.  

I've been able to get rid of most of the blinks and jumps (most noticeable on the Android platform) with the exception of one blink that sometimes occurs before the start of a transition and one after the transition is complete.  I believe that blink is caused by the fundamental way in which the transitions are implemented.  When the ui-page-active class is added to the $to page at the start of the transition, it seems to sometimes cause a blink.  There doesn't seem to be any way around it because that's how it makes the page visible so it can begin the transition.  Similarly, when the ui-page-active class is removed from the $from page, it sometimes causes another blink.  Overall though, I think the page transition experience is better, but slower.  That's because I had to slow down the transitions to help get rid of some of the blinks and flashes.  

There is another fundamental issue that should be pointed out.  Sometimes, the page transitioning from blinks back into view at the end of the transition.  Similarly, the $to page blinks into view befoe the start of the transition.  This seems to be caused by a lack of browser support for the CSS animation-fill-mode property.  In the jquery.mobile.structure.overrides.css file you will see that I've set the vendor specific animation-fill-mode properties to "both".  That should fix the blink in and/or out of the pages involved with the transition when browsers add support for it.  For an easy test of whether a particular browser supports the animation-fill-mode property, check this page:

http://css3animator.com/examples/animation-fill-mode/both.html

Click the red ball.  It will change to green and start bouncing.  If it returns to red after the transition is over, then your browser does NOT support the animation-fill-mode property and you will likely experience the aforementioned blink in of the to or from pages involved with a transition in jQuery Mobile.  

Last but not least, one of the jumps I had to fix is written up in issue #4535.  

https://github.com/jquery/jquery-mobile/issues/4535

I fixed it and submitted a pull request to the jQuery Mobile team.  

https://github.com/jquery/jquery-mobile/pull/4536

If they don't approve the pull request and merge the fix in with the official codebase, then you will need to manually apply the fix for an optimal transition experience.  I'll add to this readme if that scenario presents itself.  

To see what the files included in this repo can do for your transitions, check out the Live Demo of MPDTunes.  Go to http://www.mpdtunes.com/ and click on the "Live Demo" tab and log in.  If you have an Android phone, you should notice less blinkyness and jumpiness in the transitions.  You will also notice the smooth scroll to top rather than the sometimes jarring experience of jumping to top before a transition. 

### Using the smooth.scrollTo and other transition overrides

First, you need to download two jQuery plugins, easing v1.3 and scrollTo v1.4.2:  

http://gsgd.co.uk/sandbox/jquery/easing/
http://flesler.blogspot.com/2009/05/jqueryscrollto-142-released.html

Then, just include the files in this order:

```html
<link rel="stylesheet" href="includes/css/jquery.mobile.structure-1.1.0.min.css" />
<link rel="stylesheet" href="includes/css/jquery.mobile.structure.overrides.css" />

<script type="text/javascript" src="includes/js/jquery-1.7.2.min.js"></script>
<script type="text/javascript" src="includes/js/jquery.easing.1.3.js"></script>
<script type="text/javascript" src="includes/js/jquery.scrollTo-1.4.2.js"></script>
<script type="text/javascript" src="includes/js/jquery.mobile.defaults.overrides.js"></script>
<script type="text/javascript" src="includes/js/jquery.mobile-1.1.0-min.js"></script>
```
Note:  The files are not minified, so it's up to you to concatenate and minify them for best performance.