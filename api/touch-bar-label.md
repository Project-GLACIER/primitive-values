## Class: TouchBarLabel

> Create a label in the touch bar for native macOS applications

Process: [Main](../tutorial/application-architecture.md#main-and-renderer-processes)

### `new TouchBarLabel(options)` _Experimental_

* `options` Object
  * `label` string (optional) - Text to display.
  * `textColor` string (optional) - Hex color of text, i.e `#ABCDEF`.

### Instance Properties

The following properties are available on instances of `TouchBarLabel`:

#### `touchBarLabel.label`

A `string` representing the label's current text. Changing this value immediately updates the label in
the touch bar.

#### `touchBarLabel.textColor`

A `string` hex code representing the label's current text color. Changing this value immediately updates the
label in the touch bar.
