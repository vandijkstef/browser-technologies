# Enhancement analysis
This document describes the possible enhancements for the [WAFS app](https://github.com/vandijkstef/wafs).

## Images
The site doesn't use any images. Therefore, none could be optimized.

## Custom fonts
The current font-stack is as following: **Ubuntu, Calibri, Arial, Helvetica, sans-serif**.
While Ubuntu is a Linux/Ubuntu only font, and Calibri is a Windows only font, neither of them are being loaded as a custom font and will just fall back to Arial/Helvetica/sans-serif. No improvements can be made.

## Javascript (fully disabled)
When JS is disabled, the site will not function since it uses JS to gather data from external API's. To make the site function without JS, the data needs to be gathered (and rendered) on a server.
The site currently shows a loading animation, even though there isn't actually something loading. Further documentation on this problem is found under a [github issue](https://github.com/vandijkstef/wafs/issues/3).

## Color
Colors have been tested using **Sim Daltonism**. The used colors provide enough contrast to be functional.


## Cookies
The site isn't using any cookies.

## localStorage
localStorage is being used to cache API data, and isn't in the core of the system. However, when it's not available, JS still crashes and nothing will function anymore. Further documentation is linked under a [github issue](https://github.com/vandijkstef/wafs/issues/4).

## Keyboard only navigation
The site is a simple single column, containing some sections with links or lists. They are tabbable, though the focus state is still browser default.


Aanvullen DOCS, hoe, screenshots etc. Kopje screenreader. Trycatch op de localstorage
