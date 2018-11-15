# clipboard

> Perform copy and paste operations on the system clipboard.

Process: [Main](../glossary.md#main-process), [Renderer](../glossary.md#renderer-process)

In the renderer process context it depends on the [`remote`](remote.md) module on Linux,
it is therefore not available when this module is disabled.

The following example shows how to write a string to the clipboard:

```javascript
const { clipboard } = require('electron')
clipboard.writeText('Example string')
```

On X Window systems, there is also a selection clipboard. To manipulate it
you need to pass `selection` to each method:

```javascript
const { clipboard } = require('electron')
clipboard.writeText('Example string', 'selection')
console.log(clipboard.readText('selection'))
```

## Methods

The `clipboard` module has the following methods:

**Note:** Experimental APIs are marked as such and could be removed in future.

### `clipboard.readText([type])`

* `type` string (optional)

Returns `string` - The content in the clipboard as plain text.

### `clipboard.writeText(text[, type])`

* `text` string
* `type` string (optional)

Writes the `text` into the clipboard as plain text.

### `clipboard.readHTML([type])`

* `type` string (optional)

Returns `string` - The content in the clipboard as markup.

### `clipboard.writeHTML(markup[, type])`

* `markup` string
* `type` string (optional)

Writes `markup` to the clipboard.

### `clipboard.readImage([type])`

* `type` string (optional)

Returns [`NativeImage`](native-image.md) - The image content in the clipboard.

### `clipboard.writeImage(image[, type])`

* `image` [NativeImage](native-image.md)
* `type` string (optional)

Writes `image` to the clipboard.

### `clipboard.readRTF([type])`

* `type` string (optional)

Returns `string` - The content in the clipboard as RTF.

### `clipboard.writeRTF(text[, type])`

* `text` string
* `type` string (optional)

Writes the `text` into the clipboard in RTF.

### `clipboard.readBookmark()` _macOS_ _Windows_

Returns `Object`:

* `title` string
* `url` string

Returns an Object containing `title` and `url` keys representing the bookmark in
the clipboard. The `title` and `url` values will be empty strings when the
bookmark is unavailable.

### `clipboard.writeBookmark(title, url[, type])` _macOS_ _Windows_

* `title` string
* `url` string
* `type` string (optional)

Writes the `title` and `url` into the clipboard as a bookmark.

**Note:** Most apps on Windows don't support pasting bookmarks into them so
you can use `clipboard.write` to write both a bookmark and fallback text to the
clipboard.

```js
clipboard.write({
  text: 'https://electronjs.org',
  bookmark: 'Electron Homepage'
})
```

### `clipboard.readFindText()` _macOS_

Returns `string` - The text on the find pasteboard. This method uses synchronous
IPC when called from the renderer process. The cached value is reread from the
find pasteboard whenever the application is activated.

### `clipboard.writeFindText(text)` _macOS_

* `text` string

Writes the `text` into the find pasteboard as plain text. This method uses
synchronous IPC when called from the renderer process.

### `clipboard.clear([type])`

* `type` string (optional)

Clears the clipboard content.

### `clipboard.availableFormats([type])`

* `type` string (optional)

Returns `string[]` - An array of supported formats for the clipboard `type`.

### `clipboard.has(format[, type])` _Experimental_

* `format` string
* `type` string (optional)

Returns `boolean` - Whether the clipboard supports the specified `format`.

```javascript
const { clipboard } = require('electron')
console.log(clipboard.has('<p>selection</p>'))
```

### `clipboard.read(format)` _Experimental_

* `format` string

Returns `string` - Reads `format` type from the clipboard.

### `clipboard.readBuffer(format)` _Experimental_

* `format` string

Returns `Buffer` - Reads `format` type from the clipboard.

### `clipboard.writeBuffer(format, buffer[, type])` _Experimental_

* `format` string
* `buffer` Buffer
* `type` string (optional)

Writes the `buffer` into the clipboard as `format`.

### `clipboard.write(data[, type])`

* `data` Object
  * `text` string (optional)
  * `html` string (optional)
  * `image` [NativeImage](native-image.md) (optional)
  * `rtf` string (optional)
  * `bookmark` string (optional) - The title of the url at `text`.
* `type` string (optional)

```javascript
const { clipboard } = require('electron')
clipboard.write({ text: 'test', html: '<b>test</b>' })
```
Writes `data` to the clipboard.
