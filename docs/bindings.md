<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

# LocalizationObserver

The `LocalizationObserver` class is responsible for localizing DOM trees.
It also implements the iterable protocol which allows iterating over and
retrieving available `Localization` objects.

Each `document` will have its corresponding `LocalizationObserver` instance
created automatically on startup, as `document.l10n`.

## constructor

Returns **[LocalizationObserver](#localizationobserver)** 

## has

Test if the `Localization` object with a given name already exists.

```javascript
if (document.l10n.has('extra')) {
  const extraLocalization = document.l10n.get('extra');
}
```

**Parameters**

-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** key for the object

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 

## get

Retrieve a reference to the `Localization` object by name.

```javascript
const mainLocalization = document.l10n.get('main');
const extraLocalization = document.l10n.get('extra');
```

**Parameters**

-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** key for the object

Returns **Localization** 

## set

Sets a reference to the `Localization` object by name.

```javascript
const loc = new Localization();
document.l10n.set('extra', loc);
```

**Parameters**

-   `name` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** key for the object
-   `value` **Localization** `Localization` object

Returns **[LocalizationObserver](#localizationobserver)** 

## requestLanguages

Trigger the language negotation process with an array of language codes.
Returns a promise with the negotiated array of language objects as above.

```javascript
document.l10n.requestLanguages(['de-DE', 'de', 'en-US']);
```

**Parameters**

-   `requestedLangs` **[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>** array of requested languages

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>>** 

## setAttributes

Set the `data-l10n-id` and `data-l10n-args` attributes on DOM elements.
L20n makes use of mutation observers to detect changes to `data-l10n-*`
attributes and translate elements asynchronously.  `setAttributes` is
a convenience method which allows to translate DOM elements declaratively.

You should always prefer to use `data-l10n-id` on elements (statically in
HTML or dynamically via `setAttributes`) over manually retrieving
translations with `format`.  The use of attributes ensures that the
elements can be retranslated when the user changes their language
preferences.

```javascript
document.l10n.setAttributes(
  document.querySelector('#welcome'), 'hello', { who: 'world' }
);
```

This will set the following attributes on the `#welcome` element.  L20n's
MutationObserver will pick up this change and will localize the element
asynchronously.

```html
<p id='welcome'
  data-l10n-id='hello'
  data-l10n-args='{"who": "world"}'>
</p>
```

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** Element to set attributes on
-   `id` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** l10n-id string
-   `args` **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)&lt;[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String), [string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)>** KVP list of l10n arguments```

    ```

## getAttributes

Get the `data-l10n-*` attributes from DOM elements.

```javascript
document.l10n.getAttributes(
  document.querySelector('#welcome')
);
// -> { id: 'hello', args: { who: 'world' } }
```

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** HTML element

Returns **{id: [string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String), args: [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)}** 

## observeRoot

Add a new root to the list of observed ones.

**Parameters**

-   `root` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** Root to observe.
-   `l10n` **\[Localization](default this.get('main'))** `Localization` object

## disconnectRoot

Remove a root from the list of observed ones.
If the root is the last to be associated with a given `Localization` object
the `Localization` object association will also be removed.

Returns `true` if the root was the last one associated with at least
one `Localization` object.

**Parameters**

-   `root` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** Root to disconnect.

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 

## pause

Pauses the `MutationObserver`

## resume

Resumes the `MutationObserver`

## translateAllRoots

Triggers translation of all roots associated with the
`LocalizationObserver`.

Returns a `Promise` which is resolved once all translations are
completed.

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** 

## translateFragment

Translate a DOM node or fragment asynchronously.

You can manually trigger translation (or re-translation) of a DOM fragment
with `translateFragment`.  Use the `data-l10n-id` and `data-l10n-args`
attributes to mark up the DOM with information about which translations to
use.

Returns a `Promise` that gets resolved once the translation is complete.

**Parameters**

-   `frag` **DOMFragment** DOMFragment to be translated

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** 

## translateElement

Translates a single DOM node asynchronously.

Returns a `Promise` that gets resolved once the translation is complete.

**Parameters**

-   `element` **[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)** HTML element to be translated

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)** 
