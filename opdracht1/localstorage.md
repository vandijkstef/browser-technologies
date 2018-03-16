# LocalStorage
The read-only localStorage property allows you to access a Storage object for the Document's origin; the stored data is saved across browser sessions. localStorage is similar to sessionStorage, except that while data stored in localStorage has no expiration time, data stored in sessionStorage gets cleared when the page session ends — that is, when the page is closed.

It should be noted that data stored in either localStorage or sessionStorage is specific to the protocol of the page.
[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

## How to test
* Chrome: Start with CLI using the **--disable-local-storage** option
* Firefox: about:config -> dom.storage.enabled

## Problems
According to [CanIuse.com](https://caniuse.com/#search=localstorage) there are still quite some issues regarding localStorage. Most issues arise in outdated browsers. The most important issues:
* IE 8 & IE 9 didn't properly implement the spec, and localStorage data is shared between HTTP and HTTPS. Data for the HTTPS site could be changed by a HTTP request. This is a serious security risk.
* IE 10 & IE 11 also didn't properly implement the spec. The event **storage** doesn't work like it should.
* IE doesn't have localStorage over the file:// protocol.
* IE 11 doesn't properly sync localStorage data over multiple windows.
* iOS 5 & 6 store localStorage within cache, and it can occasionally be cleared by the OS.
* Some browsers (mainly Safari) won't store localStorage data when browsing as private.

## Examples
Reddit user Grillorafael made a [list of major sites using localStorage](https://www.reddit.com/r/webdev/comments/2wgrs1/checking_how_big_sites_use_localstorage/).
Most sites store "simple" values like config settings for the UI. Some sites however, do use localStorage to cache data. Two cases studies:

### Twitter
Uncached with localStorage: 113 requests, 4.0MB  
Uncached without localStorage: 133 requests, 4.6MB  
Cached with localStorage: 127 requests, 474kb  
Cached without localStorage: 135 request, 851kb  

localStorage seems to skip some requests, but it's very hard to actually test this since the content is changing too rapidly.

### WAFS app
Uncached without localStorage: 162 req, 304kb
Uncached with localStorage: 19 requests, 31.4kb

Unfortunately, the app doesn't function when localStorage is disabled, so the first request is used to gather the data. It's clear that localStorage saves a lot of requests.

## Solutions
The main usage of localStorage is caching (large) amounts of data. Storing and retrieving data shouldn't build upon, but instead used as an enhancement to improve loading times. In case localStorage is not functioning, the user will have to wait for the data to be retrieved again.