![contra.png][logo]

> A sane event emitter component

This is the event emitter found in [`contra`][1].

# Install

Install using `npm` or `bower`. Or get the [source code][3] and embed that in a `<script>` tag.

```shell
npm i contra.emitter --save
```

```shell
bower i contra.emitter --save
```

You can use it as a Common.JS module, or embed it directly in your HTML.

```js
var emitter = require('contra.emitter');
```

```html
<script src='contra.emitter.js'></script>
<script>
var λ = contra;
var emitter = λ.emitter;
</script>
```

## `λ.emitter(thing={}, options={})`

Augments `thing` with the event emitter methods listed below. If `thing` isn't provided, an event emitter is created for you. Emitter methods return the `thing` for chaining.

- `thing` Optional. Writable JavaScript object
- `emit(type, ...arguments)` Emits an event of type `type`, passing arguments
- `on(type, fn)` Registers an event listener `fn` for `type` events
- `once(type, fn)` Same as `on`, but the listener is discarded after one callback
- `off(type, fn)` Unregisters an event listener `fn` from `type` events
- `off(type)` Unregisters all event listeners from `type` events
- `off()` Unregisters all event listeners

The emitter can be configured with the following options, too.

- `async` Debounce listeners asynchronously. By default they're executed in sequence.
- `throws` Throw an exception if an `error` event is emitted and no listeners are defined. Defaults to `true`.

```js
var thing = λ.emitter(); // also, λ.emitter({ foo: 'bar' })

thing.once('something', function (level) {
  console.log('something FIRST TROLL');
});

thing.on('something', function (level) {
  console.log('something level ' + level);
});

thing.emit('something', 4);
thing.emit('something', 5);
// <- 'something FIRST TROLL'
// <- 'something level 4'
// <- 'something level 5'
```

Returns `thing`.

Events of type `error` have a special behavior. `λ.emitter` will throw if there are no `error` listeners when an error event is emitted. This behavior can be turned off setting `throws: false` in the options.

```js
var thing = { foo: 'bar' };

λ.emitter(thing);

thing.emit('error', 'foo');
<- throws 'foo'
```

If an `'error'` listener is registered, then it'll work just like any other event type.

```js
var thing = { foo: 'bar' };

λ.emitter(thing);

thing.on('error', function (err) {
  console.log(err);
});

thing.emit('error', 'foo');
<- 'foo'
```

# License

MIT

  [logo]: https://raw.github.com/bevacqua/contra/master/resources/contra.png
  [1]: https://github.com/bevacqua/contra
