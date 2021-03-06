# virtual-hyperscript

<!--
    [![build status][1]][2]
    [![NPM version][3]][4]
    [![Coverage Status][5]][6]
    [![gemnasium Dependency Status][7]][8]
    [![Davis Dependency status][9]][10]
-->

<!-- [![browser support][11]][12] -->

A DSL for creating virtual trees

# **MOVED.** Please check out [virtual-dom](https://github.com/Matt-Esch/virtual-dom/tree/master/virtual-hyperscript) for the source code.

## Example

```js
var h = require('virtual-hyperscript')

var tree = h('div.foo#some-id', [
    h('span', 'some text'),
    h('input', { type: 'text', value: 'foo' })
])
```

## Docs

See [hyperscript](https://github.com/dominictarr/hyperscript) which has the
  same interface.
  
Except `virtual-hyperscript` returns a virtual DOM tree instead of a DOM
  element.

### `h(selector, properties, children)`

`h()` takes a selector, an optional properties object and an
  optional array of children or a child that is a string.
  
If you pass it a selector like `span.foo.bar#some-id` it will
  parse the selector and change the `id` and `className`
  properties of the `properties` object.
  
If you pass it an array of `children` it will have child
  nodes, normally ou want to create children with `h()`.
  
If you pass it a string it will create an array containing
  a single child node that is a text element.

### Special properties in `h()`

#### `key`

If you call `h` with `h('div', { key: someKey })` it will
  set a key on the return `VNode`. This `key` is not a normal
  DOM property but is a virtual-dom optimization hint.

It basically tells virtual-dom to re-order DOM nodes instead of
  mutating them.

#### `namespace`

If you call `h` with `h('div', { namespace: "http://www.w3.org/2000/svg" })`
  it will set the namespace on the returned `VNode`. This
  `namespace` is not a normal DOM property, instead it will
  cause `vdom` to create a DOM element with a namespace.

#### `data-*`

If you call `h` with `h('div', { data-foo: "bar" })` it will
  set `data-foo` to be a `VHook` that set's a `DataSet` property
  named `foo` with the value `"bar"` on the actual dom element.

It will not set a property `data-foo` on the dom element.

This means that somewhere else in your code you can use
  `DataSet(elem).foo` to read this property.

#### `ev-*`

If you call `h` with `h('div', { ev-click: function (ev) { } })` it
  will store the event handler on the dom element. It will not
  set a property `'ev-foo'` on the DOM element.

This means that `dom-delegator` will recognise the event handler
  on that element and correctly call your handler when an a click
  event happens.

#### `children`

If you call `h` with `h('div', { children: "foo" })` it will use
  `properties.children` as the nodes children instead of the third
  argument.

## Installation

`npm install virtual-hyperscript`

## Contributors

 - Raynos

## MIT Licenced

  [1]: https://secure.travis-ci.org/Raynos/virtual-hyperscript.png
  [2]: https://travis-ci.org/Raynos/virtual-hyperscript
  [3]: https://badge.fury.io/js/virtual-hyperscript.png
  [4]: https://badge.fury.io/js/virtual-hyperscript
  [5]: https://coveralls.io/repos/Raynos/virtual-hyperscript/badge.png
  [6]: https://coveralls.io/r/Raynos/virtual-hyperscript
  [7]: https://gemnasium.com/Raynos/virtual-hyperscript.png
  [8]: https://gemnasium.com/Raynos/virtual-hyperscript
  [9]: https://david-dm.org/Raynos/virtual-hyperscript.png
  [10]: https://david-dm.org/Raynos/virtual-hyperscript
  [11]: https://ci.testling.com/Raynos/virtual-hyperscript.png
  [12]: https://ci.testling.com/Raynos/virtual-hyperscript
