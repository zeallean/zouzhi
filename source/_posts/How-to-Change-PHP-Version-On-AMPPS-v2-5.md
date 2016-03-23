title: How to Change PHP Version On AMPPS v2.5
tags: []
date: 2015-08-13 17:16:08
---

After I install AMPPS(v2.5) on my Macbook Pro(2013),There is something confuse me. I can’t change the PHP version!

<!-- more -->

In the control Panel. `PHP`->`Change PHP Version`.There are only have `PHP 5.3` can choose. But what I want is PHP 5.6 for the use of php namespace. How can I do that?

The Almighty Google! I find this. [**_I’m using Ampps version 2.5 and my php version is 5.3 ??_**](http://www.softaculous.com/board/index.php?tid=5847&amp;tpg=all&amp;title=i%27m_using_Ampps_version_2.5_and_my_php_version_is_5.3_%3F%3F "i%27m_using_Ampps_version_2.5_and_my_php_version_is_5.3_%3F%3F")

> Hi,
> 
> Work around for Mac Users is to run Ampps from Terminal:

`The Code:`

    user> cd /Applications/AMPPS 

    user> ./Ampps.app/Contents/MacOS/Ampps

obviously! It is a bug with Ampps v2.5.But the best solution to solve my requirement is this.

By the way. When you follow the above to change the PHP version, Ampps will be crash when you open the app normally and change the PHP version by the panel.

Ok, I know you can’t understand what I am talking about above!! Yes, My English is poor!

Orz! Thank you for your reading to here ~~~