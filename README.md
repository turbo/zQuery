# z(ero)Query

Here you find pure JavaScript alternatives to jQuery things and some neat JS hacks. With content from [here](https://github.com/ndugger/youdontneedjquery).

**AJAX GET**

jQuery

```js
$.ajax({
  url: 'path/to/json',
  success: data  => {/* use 'data' here */},
  error:   error => {/* use 'error' here */}
});
```

JavaScript (+[fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), +[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise))

```js
fetch('/path/to/json')
.then(response => response.json())
.then(data   => {/* use 'data' here */})
.catch(error => {/* use 'error' here */});
```

**AJAX POST**

jQuery

```js
$.ajax({
  url: 'https://example.com/api',
  type: 'POST',
    contentType: 'application/json',
    data: JSON.stringify(myObjectHere),
    success: data => {/* use 'data' here */ },
    error: error  => {/* use 'error' here */}
});
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

**Bind**

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

**DOM Ready**

jQuery

```js
$(document).ready(function() {
  alert("DOM ready.");
});
```

```js
function _(f){/in/.test(document.readyState)?setTimeout('_('+f+')',9):f()}_(function(){
  alert("DOM ready.");
});
```

This is faster than other JS (intrinsic) functions, but still slower than just putting the JS at the end of your HTML file. Further, this works in IE8, whereas other solutions don't.

**DOM Query**

jQuery

```js
const myElement = $('.foo');
```

JavaScript

```js
const myElement          = document.querySelector('.foo');
const myMultipleElements = document.querySelectorAll('.foo');
```

**Element Attributes**

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

**Element Childs**

jQuery

```js
$(myElement).children();
```

JavaScript

```js
myElement.children;
```

**Element Child Manipulation**

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

**Element Class**

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

**Element Content**

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

**Element Data Attributes**

jQuery

```js
$(myElement).data('foo', 'bar');
```

JavaScript

```js
myElement.dataset.foo = 'bar';
```

**Element Foreach**

jQuery

```js
$(myMultipleElements).each((i, x) => {/* use 'x' here */});
```

JavaScript

```js
Array.from(myMultipleElements).forEach((x, i) => {/* use 'x' here */});
```

**Element Filters**

jQuery

```js
$(myMultipleElements).filter('.some-class-here');
```

JavaScript

```js
Array.from(myMultipleElements).filter(x => x.classList.contains('some-class-here'));
```

**Element Find**

jQuery

```js
const x = $(myElement).find('.foo');
const y = $(myMultipleElements).find('.foo');
```

JavaScript

```js
const x = myElement.querySelectorAll('.foo');
const y = Array.from(myMultipleElements).map(x => Array.from(x.querySelectorAll('.foo'))).reduce((a, b) => a.concat(b));
```

**Element Listeners**

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

**Element Parent**

jQuery

```js
$(myElement).parent();
$(myMultipleElements).parents('.foo'); // all parents
```

JavaScript

```js
myElement.parentElement;
Array.from(myMultipleElements).map(x => x.closest('.foo')); // all parents
```

**Element Siblings**

jQuery

```js
$(myElement).siblings();
```

JavaScript

```js
Array.from(myElement.parentElement.children).filter(x => x !== myElement);
```

**Element Sibling Navigation**

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

**Element Styles**

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

**Element Value**

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

**Element Visibility**

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
