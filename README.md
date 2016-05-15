# z(ero)Query

Here you find pure JavaScript alternatives to jQuery things and some neat JS hacks. With content from [here](https://github.com/ndugger/youdontneedjquery). 

You can share this repo here as [git.io/zQuery](http://git.io/zQuery).

## AJAX GET

jQuery

```js
$.get(
  'path/to/json',
  data => {/* use 'data' here */}
).error(
  error => {/* use 'error' here */}
);
```

JavaScript (+[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), +[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise))

```js
fetch('/path/to/json')
.then(response => response.json())
.then(data   => {/* use 'data' here */})
.catch(error => {/* use 'error' here */});
```

## AJAX POST

jQuery

```js
$.post(
  'https://example.com/api',
  JSON.stringify(myObjectHere),
  data => {/* use 'data' here */ }
).error(
  error => {/* use 'error' here */}
);
```

JavaScript (+[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), +[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise))

```js
fetch('path/to/whatever', {
  method: 'POST',
  headers: new Headers({ 'Content-Type': 'application/json' }),
  body: JSON.stringify(myObjectHere)
})
.then(response => response.json())
.then(data   => {/* use 'data' here */})
.catch(error => {/* use 'error' here */}
);
```

## Bind

jQuery

```js
$(".foo").bind("contextmenu", function (event) { /* do something */ });
$(".foo").click(function (event) { /* do something */ });
```

JavaScript

```js
document.querySelector(".foo").addEventListener("contextmenu", function (event) { /* do something */ });
document.querySelector(".foo").addEventListener('click', function() { /* do something */ });
```

## DOM Ready

jQuery

```js
$(document).ready(function() {
  alert("DOM ready.");
});
```

```js
function onDOMReady(f){/in/.test(document.readyState)?setTimeout(arguments.callee.name+'('+f+')',9):f()}

onDOMReady(function(){
  alert("DOM ready.");
});
```

This is faster than other JS (intrinsic) functions, but still slower than just putting the JS at the end of your HTML file. Further, this works in IE8, whereas other solutions don't.

## DOM Query

jQuery

```js
const myElement = $('.foo');
```

JavaScript

```js
const myElement          = document.querySelector('.foo');
const myMultipleElements = document.querySelectorAll('.foo');
```

## Element Attributes

jQuery

```js
const foo = $(myElement).attr('foo');
$(myElement).attr('bar', foo);
```

JavaScript

```js
const foo = myElement.getAttribute('foo');
myElement.setAttribute('bar', foo);
```

## Element Childs

jQuery

```js
$(myElement).children();
```

JavaScript

```js
myElement.children;
```

## Element Child Manipulation

jQuery

```js
$(myElement).append(anotherElement);
$(myElement).prepend(anotherElement);
$(myElement).remove();
```

JavaScript

```js
myElement.appendChild(anotherElement);
myElement.insertBefore(anotherElement, myElement.firstChild);
myElement.remove();
```

## Element Class

jQuery

```js
$(myElement).addClass('foo');
$(myElement).removeClass('foo');
$(myElement).toggleClass('foo');
```

JavaScript

```js
myElement.classList.add('foo');
myElement.classList.remove('foo');
myElement.classList.toggle('foo');
```

## Element Content

jQuery

```js
$(myElement).text('lorem ispum');
$(myElement).html('<span>lorem ipsum</span>');
```

JavaScript

```js
myElement.textContent = 'lorem ipsum';
myElement.innerHTML = '<span>lorem ipsum</span>';
```

## Element Data Attributes

jQuery

```js
$(myElement).data('foo', 'bar');
```

JavaScript

```js
myElement.dataset.foo = 'bar';
```

## Element Foreach

jQuery

```js
$(myMultipleElements).each((i, x) => {/* use 'x' here */});
```

JavaScript

```js
Array.from(myMultipleElements).forEach((x, i) => {/* use 'x' here */});
```

## Element Filters

jQuery

```js
$(myMultipleElements).filter('.some-class-here');
```

JavaScript

```js
[...myMultipleElements].filter(x => x.classList.contains('some-class-here'));
```

## Element Find

jQuery

```js
const x = $(myElement).find('.foo');
const y = $(myMultipleElements).find('.foo');
```

JavaScript

```js
const x = myElement.querySelectorAll('.foo');
const y = [...myMultipleElements].map(x => [...x.querySelectorAll('.foo')]).reduce((a, b) => [...a, ...b]);
```

## Element Listeners

jQuery

```js
$(myElement).on('click', myEventHandler);
$(myElement).off('click', myEventHandler);
```

JavaScript

```js
myElement.addEventListener('click', myEventHandler);
myElement.removeEventListener('click', myEventHandler);
```

## Element Parent

jQuery

```js
$(myElement).parent();
$(myMultipleElements).parents('.foo'); // all parents
```

JavaScript

```js
myElement.parentElement;
[...myMultipleElements].map(x => x.closest('.foo')); // all parents
```

## Element Siblings

jQuery

```js
$(myElement).siblings();
```

JavaScript

```js
[...myElement.parentElement.children].filter(x => x !== myElement);
```

## Element Sibling Navigation

jQuery

```js
$(myElement).next();
$(myElement).prev();
```

JavaScript

```js
myElement.nextElementSibling;
myElement.previousElementSibling;
```

## Element Styles

jQuery

```js
$(myElement).css({ background: 'red', color: 'white' });
```

JavaScript

```js
Object.assign(myElement.style, { background: 'red', color: 'white' });
// or
myElement.style.background = 'red';
myElement.style.color = 'white';
```

## Element Value

jQuery

```js
const value = $(myElement).val();
$(myElement).val('foo');
```

JavaScript

```js
const value = myElement.value;
myElement.value = 'foo';
```

## Element Visibility

jQuery

```js
$(myElement).hide();
$(myElement).show();
```

JavaScript

```js
myElement.style.display = 'none';
myElement.style.display = null;
```

## Window (Viewport) Dimensions

jQuery

```js
var height = $(window).height();   
var width = $(window).width();   
```

JavaScript

```js
var width = window.innerWidth   || document.documentElement.clientWidth  || document.body.clientWidth;
var height = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight;
```
