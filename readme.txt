Why is <video> on a web page (e.g. Youtube) resized?

<video> has a container (like width=100%) & by default it's video{object-fit:contain} of the user agent stylesheet of Chrome, Firefox, Falkon.
If no width, no height in the web page, the default is width:auto & height:auto. 
If video{object-fit:contain} is removed from the user agent stylesheet & no video{object-fit:...} in the web page, the default is video{object-fit:fill}. 

The web page author can override the user agent stylesheet, e.g. on Youtube there's html5-main-video from class from <video> that points to a CSS rule containing object-fit:cover.

How to let/get <video> (e.g. Youtube) at its native resolution, not resized?

On web browser:
3 ways: <video> without container, or with the container using max-width:100% &/or max-height:100%, otherwise to object-fit:none <video>.

On VLC (or other media player).

How to auto object-fit:none <video>?

Generally, by video{object-fit:none!important}, overriding all other web page <video> object-fit value(s) if there is/are. Or video{object-fit:none} may be enough.

User agent stylesheet:

On Firefox:
with the help of https://udn.realityripple.com/docs/Mozilla/About_omni.ja_(formerly_omni.jar), in chrome/toolkit/res/html.css of omni.ja: edit video{object-fit:contain} to video{object-fit:none!important}.

On Linux Chrome:
Install git, brotli.
In Konsole:
cd $a_path$;git clone https://chromium.googlesource.com/chromium/src/tools/grit;cd $another_path$;$a_path$/grit/pak_util.py extract /opt/google/chrome/resources.pak --brotli /usr/bin/brotli
E.g. Kate, open $another_path$/45300, edit video{object-fit:contain} to video{object-fit:none!important} then save (45300 found by grep -r 'video {').
$a_path$/grit/pak_util.py create /opt/google/chrome/resources.pak

Notes:

The new resources.pak isn't compressed as the original:
$a_path$/grit/pak_util.py create /opt/google/chrome/resources.pak --brotli /usr/bin/brotli
usage: pak_util.py [-h] {repack,extract,create,print,list-id}...
pak_util.py: error: unrecognized arguments: --brotli /usr/bin/brotli
I wonder how to do that...

There's also https://github.com/myfreeer/chrome-pak-customizer but at the time I write, the last release 2.0 & the 3.x branch (to compile) don't work...

User stylesheet:

On Firefox:
follow https://www.thoughtco.com/user-style-sheet-3469931, in userContent.css put video{object-fit:none!important}.

On Chrome:
it's impossible without extension: https://stackoverflow.com/questions/21207474/custom-css-has-stopped-working-in-32-0-1700-76-m-google-chrome-update.
But yes with an extension that injects a user stylesheet (.css file) with video{object-fit:none!important} inside.

On Falkon:
Preferences, Other, User Style Sheet, select a .css file with video{object-fit:none!important}.

It works on Youtube, Facebook, Vimeo, Koreus, Twitter, Dailymotion...

Locally, add object-fit:none to style from <video> with an extension...

Modify the web browser source code to change the default video{object-fit:fill} to video{object-fit:none!important} & remove video{object-fit:contain} from the user agent stylesheet.

How to auto get the video without container?

By video{width:auto!important;height:auto!important}.

As above...

Remove like width=100% from <video> with an extension...

How to auto get <video> with the container using max-width:100% & max-height:100%?

By video{max-width:100%!important;max-height:100%!important}.

As above...

If possible, right click on the video then Open video in new tab, or Save video as then play it on the web browser. I've never seen this on Youtube, we can assume that Google doesn't want it to be possible to download the video except with Premium, paying after the free trial...
If impossible, get the URL of the video or download it (with yt-dlp) then play it on the web browser.

How to VLC ?
If possible, right click on the video then Copy link, or Save video as then VLC.
As above, if impossible, get the URL of the video or download it (with yt-dlp) then play it on VLC.
https://code.videolan.org/videolan/vlc/-/issues/26174
https://stackoverflow.com/questions/76988482/play-youtube-in-vlc-with-yt-dlp-exe-no-ads-context-menu-in-firefox

On web browser, <video> without container vs object-fit:none <video>:

E.g. on Youtube: the video without container is on the top corner left of the player, centered with object-fit:none.

https://www.w3schools.com/css/css3_object-fit.asp
https://www.w3schools.com/cssref/pr_dim_width.php
https://www.w3schools.com/css/css_important.asp
https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade
https://chromium.googlesource.com/chromium/blink/+/master/Source/core/css/html.css
https://developer.chrome.com/docs/extensions/mv3/manifest/
https://developer.chrome.com/docs/extensions/mv3/manifest/content_scripts/

video no-fit on chrome web store:
https://chromewebstore.google.com/detail/video-no-fit/jpacddkbicjapaflpjakcljhejcpakjc
