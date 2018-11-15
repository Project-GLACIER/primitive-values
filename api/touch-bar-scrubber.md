## Class: TouchBarScrubber

> Create a scrubber (a scrollable selector)

Process: [Main](../tutorial/application-architecture.md#main-and-renderer-processes)

### `new TouchBarScrubber(options)` _Experimental_

* `options` Object
  * `items` [ScrubberItem[]](structures/scrubber-item.md) - An array of items to place in this scrubber.
  * `select` Function - Called when the user taps an item that was not the last tapped item.
    * `selectedIndex` Integer - The index of the item the user selected.
  * `highlight` Function - Called when the user taps any item.
    * `highlightedIndex` Integer - The index of the item the user touched.
  * `selectedStyle` string - Selected item style. Defaults to `null`.
  * `overlayStyle` string - Selected overlay item style. Defaults to `null`.
  * `showArrowButtons` boolean - Defaults to `false`.
  * `mode` string - Defaults to `free`.
  * `continuous` boolean - Defaults to `true`.

### Instance Properties

The following properties are available on instances of `TouchBarScrubber`:

#### `touchBarScrubber.items`

A `ScrubberItem[]` array representing the items in this scrubber. Updating this value immediately
updates the control in the touch bar. Updating deep properties inside this array **does not update the touch bar**.

#### `touchBarScrubber.selectedStyle`

A `string` representing the style that selected items in the scrubber should have. Updating this value immediately
updates the control in the touch bar. Possible values:

* `background` - Maps to `[NSScrubberSelectionStyle roundedBackgroundStyle]`.
* `outline` - Maps to `[NSScrubberSelectionStyle outlineOverlayStyle]`.
* `null` - Actually null, not a string, removes all styles.

#### `touchBarScrubber.overlayStyle`

A `string` representing the style that selected items in the scrubber should have. This style is overlayed on top
of the scrubber item instead of being placed behind it. Updating this value immediately updates the control in the
touch bar. Possible values:

* `background` - Maps to `[NSScrubberSelectionStyle roundedBackgroundStyle]`.
* `outline` - Maps to `[NSScrubberSelectionStyle outlineOverlayStyle]`.
* `null` - Actually null, not a string, removes all styles.

#### `touchBarScrubber.showArrowButtons`

A `boolean` representing whether to show the left / right selection arrows in this scrubber. Updating this value
immediately updates the control in the touch bar.

#### `touchBarScrubber.mode`

A `string` representing the mode of this scrubber. Updating this value immediately
updates the control in the touch bar. Possible values:

* `fixed` - Maps to `NSScrubberModeFixed`.
* `free` - Maps to `NSScrubberModeFree`.

#### `touchBarScrubber.continuous`

A `boolean` representing whether this scrubber is continuous or not. Updating this value immediately
updates the control in the touch bar.
