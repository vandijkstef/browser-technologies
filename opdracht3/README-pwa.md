# PWA - Typing Game
**Note: The actual app is found in this [repository](https://github.com/vandijkstef/typetitan/tree/browser-tech-layer-3)**

## Core functionality
A typing game in the browser. The game will return you some scores so you can track your own improvements.

---

## Features
Here described are the features that are used within the app. 

### Javascript
A large part of the game will use Javascript. The game will work without any JS, but statistics are less complete and accurate. The game makes use of three JS functions described below. If any of these aren't supported, the game will work in non-JS mode. If all of these are supported, the body will have the JS class.

#### AddEventListener
Since we need a number of diffent types eventListeners, we require this to be available. It's [supported](https://caniuse.com/#feat=addeventlistener) by every browser except IE8 and lower. 

#### QuerySelector
The [querySelector](https://caniuse.com/#feat=queryselector) is available in all browsers, except IE7 and lower, and Firefox 3 and lower. It's buggy in IE8, but we this app already isn't working when the eventListener isn't available.

#### ClassList
The [classList](https://caniuse.com/#feat=classlist) is well supported on the newer browsers. A major bug in slightly older versions is that **multiple classes in an .add() aren't supported**. 

#### WebSocket
If [WebSocket](https://caniuse.com/#feat=websockets) is available, the browser will connect to the socket server and periodically ask the server for updated information. It's supported in all major browser, even slightly outdated ones. (IE since version 10). Older browsers do have certain bugs, or are hidden behind an option, but the websocket is solely enhancing the experience.

### CSS
Most CSS is basic and functional in major browsers. Some newer techniques are used:

#### Flexbox
If [flexbox](https://caniuse.com/#feat=flexbox) is supported the game is neatly centered on the screen. Otherwise the game will align top-left. It's supported on most browsers, though older ones do not support flex wrapping, flex-flow or align-content. It's buggy in every version of IE, but IE also conveniently ignores any @support rule.

#### Variables
[CSS Variables](https://caniuse.com/#feat=css-variables) are fairly supported (except for, IE and Opera Mini). When used, I will first declare the value in a traditional way. If variables are not supported, they will just be ignored. Keep in mind that any JS use of these variables are purely an enhancement and **use of classes** is higly recommended over this technique.

#### RGBA
[RGBA](https://caniuse.com/#feat=css3-colors) color definitions are widely supported, yet not in IE8 or lower. They will be ignored by non-supporting browsers. Setting a fallback first is recommended.

---

## Layering
![progression sheet](progression_sheet_typtitan.png?raw=true)

### Layer 1
* Functional without JS or browser that don't support any of the following:
	* addEventListener
	* classList
	* querySelector
* Game functions:
	* Creating a game
	* Playing the game
	* Seeing basic statistics post-game

### Layer 2
* Functional when methods described in layer 1 are available
* Flexbox enhancements
* Game enhancements:
	* Centered Game
	* Automatic swapping of Input fields
	* Feedback on input (TODO:)

### Layer 3
* Requires WebSockets
* Game enhancements:
	* TODO: Update post-game score screen with competitor scores
	* TODO: Show other players actions during game

---
