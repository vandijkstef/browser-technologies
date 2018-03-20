# Faqcordeon

## Sketches
This image shows a fully collapsed (JS and/or new CSS available). The second sketch is half collapsed version.
![Schets](img/IMG_2011.jpg)
This image shows the fully uncollapsed FAQ. Note, the arrows show interaction and should only be visible when that interaction is possible
![Schets](img/IMG_2012.jpg)

## Used Techniques
This section will describe the main steps taken in progressively enhancing the module. 

### CSS Variables
CSS variables are used for the colors. For clarity, I'm using another color scheme when they are not supported.
To safely use CSS variables, you should use a cascading fallback. Older browsers will use **red**, newer browsers, supporting CSS variables will use **blue**. If a variable is undefined, and variables are supported, in this case, **green** will be used.

``` CSS
:root {
	--foo: blue;
}

* {
	color: red;
	color: var(--foo);
	color: var(--undefined, green)
}
```

This image shows the fallback. Left IE without CSS variable support, right Chrome with CSS variable support. Note: The used colors are different on purpose.
![cssvars](img/cssvars.png)

### Folding without JS
To fold the FAQ without JS I will make use of the :target selector. This will be applied to the questions, the subjects won't be able to fold. Another limitation is that only one question can be unfolded at the time. In CSS I will only fold the questions if :target is supported, [which comes down to not folding at all on non-js versions of IE <= 8](https://www.quirksmode.org/css/selectors/).
``` HTML
<!--[if lte IE 8]>
	HTML for IE <= 8, other browsers will ignore this.
	This text is probably being shown as comment
<![endif]-->
<p>Proof the other text is a comment, or are you using an old browser?</p>
```

### Folding with JS
Upon loading the page, I will add a class to the outer element (ul), so style rules can make the whole thing collapse. Then I will use the querySelector and the classList to handle the objects and apply CSS classes. The folding will be done using CSS, and enhanced with animations. Additionally, I will need to suppress the functionality of :target, so multiple questions can be opened and closed at will.
``` JS
window.addEventListener('DOMContentLoaded', function() {
	// Do all the things!
});
```

### Animations
All animation will be CSS animations (transition). These are not supported on IE <= 9. I won't need to catch this, as the transition property will be ignored and the elements will just "pop". 

``` CSS
div {
	transition: .2s /* will be ignored on IE < 9 */
}
```

## Additional notes
This section will describe the steps taken in small scale progressive enhancements, speaking of additional usages of **@supports in CSS** and **if ('foo' in bar)** in JS.

### CSS @supports
With the @supports rule I can test if a property and value is available in the browser.  
**Important: All versions of IE will ignore these rules since they don't support @supports in the first place**
``` CSS
@supports (display: block) {
	/* Supported code here */
}
```

### querySelector
The [querySelector](https://caniuse.com/#feat=queryselector) isn't supported in IE <= 7, and still buggy in IE 8. To support these browsers I've used helper functions (getElement/getElements) that will try to use the querySelector, and else will try to achieve the same result using older DOM query methods. If anything keeps failing, I will remove the **js-interactive** class so the FAQ will unfold.
``` JS
if ('querySelector' in document)
```

### classList Add/Remove/Toggle
[ClassList](https://caniuse.com/#feat=classlist) isn't supported on IE <= 9. 
In this case, I will try to update the classes by updating the class string as a string. The limitations present in IE 10 and IE 11 are not important for this module.
``` JS
if ('classList' in element)
```