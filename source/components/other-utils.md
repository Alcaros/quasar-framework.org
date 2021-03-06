title: Other Utils
---
## Open External URL
``` js
import { openURL } from 'quasar'

openURL('http://...')
```

It will take care of the quirks involved when running under Cordova or on a browser, including notifying the user he/she has to acknowledge opening popups.

## Debounce Function
If your App uses JavaScript to accomplish taxing tasks, a debounce function is essential to ensuring a given task doesn't fire so often that it bricks browser performance. Debouncing a function limits the rate at which the function can fire.

Debouncing enforces that a function not be called again until a certain amount of time has passed without it being called. As in "execute this function only if 100 milliseconds have passed without it being called."

A quick example: you have a resize listener on the window which does some element dimension calculations and (possibly) repositions a few elements. That isn't a heavy task in itself but being repeatedly fired after numerous resizes will really slow your App down. So why not limit the rate at which the function can fire?

``` js
// Returns a function, that, as long as it continues to be invoked, will not
// be triggered. The function will be called after it stops being called for
// N milliseconds. If `immediate` is passed, trigger the function on the
// leading edge, instead of the trailing.
import { debounce } from 'quasar'

(Debounced Function) debounce(Function fn, Number milliseconds_to_wait, Boolean immediate)

// Example:
window.addEventListener(
  'resize',
  debounce(function() {
    .... things to do ...
  }, 300 /*ms to wait*/)
)
```

There's also a `frameDebounce` available which delays calling your function until next browser frame is scheduled to run (read about `requestAnimationFrame`).

``` js
import { frameDebounce } from 'quasar'

(Debounced Function) frameDebounce(Function fn)

// Example:
window.addEventListener(
  'resize',
  frameDebounce(function() {
    .... things to do ...
  })
)
```

## Throttle Function
Throttling enforces a maximum number of times a function can be called over time. As in "execute this function at most once every 300 milliseconds."

``` js
// Returns a function, that, as long as it continues to be invoked, will not
// be triggered. The function will be called after it stops being called for
// N milliseconds. If `immediate` is passed, trigger the function on the
// leading edge, instead of the trailing.
import { throttle } from 'quasar'

(Throttled Function) throttle(Function fn, Number limit_in_milliseconds)

// Example:
window.addEventListener(
  'resize',
  throttle(function() {
    .... things to do ...
  }, 300 /* execute at most once every 0.3s */)
)
```

## (Deep) Copy Objects
A basic respawn of `jQuery.extend()`. Takes same parameters:
``` js
import { extend } from 'quasar'

let newObject = extend([Boolean deepCopy], targetObj, obj, ...)
```
Watch out for methods within objects.

## Generate UID
Generate unique identifiers:
``` js
import { uid } from 'quasar'

let uid = uid()
// Example: 501e7ae1-7e6f-b923-3e84-4e946bff31a8
```

## Handling event on a DOM event handler
It's cross-browser.

``` js
import { event } from 'quasar'

node.addEventListener('click', evt => {
  // left clicked?
  (Boolean) event.leftClick(evt)

  // middle clicked?
  (Boolean) event.middleClick(evt)

  // right clicked?
  (Boolean) event.rightClick(evt)

  // key in number format
  (Number) event.getEventKey(evt)

  // Mouse wheel distance (in pixels)
  (Number) event.getMouseWheelDistance(evt)

  // position on viewport
  // works both for mouse and touch events!
  (Object {top, left}) event.position(evt)

  // get target DOM Element on which mouse or touch
  // event has fired upon
  (DOM Element) event.targetElement(evt)

  // call stopPropagation and preventDefault
  event.stopAndPrevent(evt)
})
```

## Colors
You can change colors from RGB to Hex format (and reverse too).

``` js
import { colors } from 'quasar'

console.log(colors.rgbToHex(85, 165, 1)) // #55a532
console.log(colors.hexToRgb('#55a532')) // [85, 165, 1]
```

## Filter
Filter out an array of Objects based on a certain field:

``` js
import { filter } from 'quasar'

let data = [{fee: 5, desc: 'Bla bla'}, {fee: 10, desc: 'Bla bla'}, {fee: 1, desc: 'Bla bla'}]
console.log(filter('5', {field: 'fee', list: data})
// [{fee: 5, desc: 'Bla bla'}]
```
