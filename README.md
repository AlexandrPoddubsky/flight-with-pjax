# Simple Pjax mixin-component for twitter flight

Easily enable fast Ajax navigation on any FlightJS app.

## Usage example:

####Component with router

```js
define('component_ui/route', [
        'flight/lib/component',
        'path/to/flight-pjax'
    ],

    function(defineComponent, withPjax) {

        return defineComponent(newComponent, withPjax);

        function newComponent() {

            this.after('initialize', function() {
                this.on('touchend click', this.click);

                this.on('pjax:loading', this.loading);
                this.on('pjax:complete', this.complete);
                this.on('pjax:error', this.error);
            });

            this.loading = function() {
                // maybe show a loader
            };

            this.complete = function() {
                // hide loader
            };

            this.error = function() {
                // give the user a nice message
            };
        }
    }
);
```
####Initializing

```js
require([
    'path/to/flight-component-with-pjax'
], function(component) {

    // Attach pjax to the body
    pjax.attachTo(document.body, {
        defaultAnimation: 'fade',
        container: '.content-wrapper',
        selectors: [
            '.flash-messages',
            '.nav-bar'
        ]
    });
    
});
```

## Documentation

### this.navigate(URL, [boolean]);

- **URL** is url like string. Must start from '/'.
- **Boolean** if passed state would not be pushed, but replaced, to save history clean.

### this.load(url, [args])

This will perform an Ajax call to load the page.

- **URL** is url like string. Must start from '/'.
- **Args** is optional object with following params:

```js
    replaceState: Boolean
```
If passed state would not be pushed, but replaced, to save history clean.

```js
    transition: String
```
The animation for the container when being displayed.

```js
    forced: Boolean
```
Param that tells fire new state any way even if URL is same.


## CSS for container animation

Where `.content-wrapper` is the classname of your `container`.

```css
/* Fade animation */
.content-wrapper.fade {
    opacity: 0;
    transition: opacity .1s;
}
.content-wrapper.fade.in {
  opacity: 1;
}

/* Slide animation */
.content-wrapper.sliding {
    z-index: 2;
    transition: transform .4s;
    transform: translate3d(0, 0, 0);
}
.content-wrapper.sliding.left {
  z-index: 1;
  transform: translate3d(-100%, 0, 0);
}
.content-wrapper.sliding.right {
  z-index: 3;
  transform: translate3d(100%, 0, 0);
}
```

## Using Laravel

Checkout the [Laravel Pjax Middleware](https://packagist.org/packages/torann/laravel-pjax-middleware) package.