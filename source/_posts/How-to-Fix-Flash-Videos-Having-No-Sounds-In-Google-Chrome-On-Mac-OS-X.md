title: How to Fix Flash Videos Having No Sounds In Google Chrome On Mac OS X
tags: []
date: 2015-08-13 02:06:03
---

My new MacBook has had a weird issue lately — for some reason, there isn’t any sound when I play a web video in Chrome. There’s nothing wrong with Chrome, or the sound, but it just wasn’t working. After some digging, I figured out that it is just Flash related.

<!-- more -->

Turns out, the real problem is a conflict between the built-in Flash plugin in Chrome, and the Adobe one that I must have downloaded elsewhere.

And the solution is to remove one of them. In this case, the built-in one. Start by typing about:plugins into the location bar.

![img_51d44226e4989.png](http://zozorz-typechoupload.stor.sinaapp.com/1172181251.png)

Then click the Details link on the right-hand side of that page.

![img_51d4428f4ca7f.png](http://zozorz-typechoupload.stor.sinaapp.com/3705071358.png)

And then disable one of the two plugins that are loaded, since you should only have one. In my case, the sound didn’t work until I disabled the built-in “Pepper” Flash player, but your mileage may vary.

![img_51d442dc7dac1.png](http://zozorz-typechoupload.stor.sinaapp.com/1712560933.png)

Note that you’ll need to reload the tab that you are testing for the plugin situation to resolve itself. Or you could close your browser and re-open.

转载自:[How to Fix Flash Videos Having No Sounds In Google Chrome On Mac OS X](http://www.howtogeek.com/tips/how-to-fix-flash-videos-having-no-sound-in-chrome-on-mac-os-x/)