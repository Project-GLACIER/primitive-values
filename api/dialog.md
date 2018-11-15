# dialog

> Display native system dialogs for opening and saving files, alerting, etc.

Process: [Main](../glossary.md#main-process)

An example of showing a dialog to select multiple files and directories:

```javascript
const { dialog } = require('electron')
console.log(dialog.showOpenDialog({ properties: ['openFile', 'openDirectory', 'multiSelections'] }))
```

The Dialog is opened from Electron's main thread. If you want to use the dialog
object from a renderer process, remember to access it using the remote:

```javascript
const { dialog } = require('electron').remote
console.log(dialog)
```

## Methods

The `dialog` module has the following methods:

### `dialog.showOpenDialog([browserWindow, ]options[, callback])`

* `browserWindow` [BrowserWindow](browser-window.md) (optional)
* `options` Object
  * `title` string (optional)
  * `defaultPath` string (optional)
  * `buttonLabel` string (optional) - Custom label for the confirmation button, when
    left empty the default label will be used.
  * `filters` [FileFilter[]](structures/file-filter.md) (optional)
  * `properties` string[] (optional) - Contains which features the dialog should
    use. The following values are supported:
    * `openFile` - Allow files to be selected.
    * `openDirectory` - Allow directories to be selected.
    * `multiSelections` - Allow multiple paths to be selected.
    * `showHiddenFiles` - Show hidden files in dialog.
    * `createDirectory` _macOS_ - Allow creating new directories from dialog.
    * `promptToCreate` _Windows_ - Prompt for creation if the file path entered
      in the dialog does not exist. This does not actually create the file at
      the path but allows non-existent paths to be returned that should be
      created by the application.
    * `noResolveAliases` _macOS_ - Disable the automatic alias (symlink) path
      resolution. Selected aliases will now return the alias path instead of
      their target path.
    * `treatPackageAsDirectory` _macOS_ - Treat packages, such as `.app` folders,
      as a directory instead of a file.
  * `message` string (optional) _macOS_ - Message to display above input
    boxes.
  * `securityScopedBookmarks` boolean (optional) _masOS_ _mas_ - Create [security scoped bookmarks](https://developer.apple.com/library/content/documentation/Security/Conceptual/AppSandboxDesignGuide/AppSandboxInDepth/AppSandboxInDepth.html#//apple_ref/doc/uid/TP40011183-CH3-SW16) when packaged for the Mac App Store.
* `callback` Function (optional)
  * `filePaths` string[] (optional) - An array of file paths chosen by the user. If the dialog is cancelled this will be `undefined`.
  * `bookmarks` string[] (optional) _macOS_ _mas_ - An array matching the `filePaths` array of base64 encoded strings which contains security scoped bookmark data. `securityScopedBookmarks` must be enabled for this to be populated.

Returns `string[]`, an array of file paths chosen by the user,
if the callback is provided it returns `undefined`.

The `browserWindow` argument allows the dialog to attach itself to a parent window, making it modal.

The `filters` specifies an array of file types that can be displayed or
selected when you want to limit the user to a specific type. For example:

```javascript
{
  filters: [
    { name: 'Images', extensions: ['jpg', 'png', 'gif'] },
    { name: 'Movies', extensions: ['mkv', 'avi', 'mp4'] },
    { name: 'Custom File Type', extensions: ['as'] },
    { name: 'All Files', extensions: ['*'] }
  ]
}
```

The `extensions` array should contain extensions without wildcards or dots (e.g.
`'png'` is good but `'.png'` and `'*.png'` are bad). To show all files, use the
`'*'` wildcard (no other wildcard is supported).

If a `callback` is passed, the API call will be asynchronous and the result
will be passed via `callback(filenames)`.

**Note:** On Windows and Linux an open dialog can not be both a file selector
and a directory selector, so if you set `properties` to
`['openFile', 'openDirectory']` on these platforms, a directory selector will be
shown.

### `dialog.showSaveDialog([browserWindow, ]options[, callback])`

* `browserWindow` [BrowserWindow](browser-window.md) (optional)
* `options` Object
  * `title` string (optional)
  * `defaultPath` string (optional) - Absolute directory path, absolute file
    path, or file name to use by default.
  * `buttonLabel` string (optional) - Custom label for the confirmation button, when
    left empty the default label will be used.
  * `filters` [FileFilter[]](structures/file-filter.md) (optional)
  * `message` string (optional) _macOS_ - Message to display above text fields.
  * `nameFieldLabel` string (optional) _macOS_ - Custom label for the text
    displayed in front of the filename text field.
  * `showsTagField` boolean (optional) _macOS_ - Show the tags input box,
    defaults to `true`.
  * `securityScopedBookmarks` boolean (optional) _masOS_ _mas_ - Create a [security scoped bookmark](https://developer.apple.com/library/content/documentation/Security/Conceptual/AppSandboxDesignGuide/AppSandboxInDepth/AppSandboxInDepth.html#//apple_ref/doc/uid/TP40011183-CH3-SW16) when packaged for the Mac App Store. If this option is enabled and the file doesn't already exist a blank file will be created at the chosen path.
* `callback` Function (optional)
  * `filename` string (optional) If the dialog is cancelled this will be `undefined`.
  * `bookmark` string (optional) _macOS_ _mas_ - Base64 encoded string which contains the security scoped bookmark data for the saved file. `securityScopedBookmarks` must be enabled for this to be present.

Returns `string`, the path of the file chosen by the user,
if a callback is provided it returns `undefined`.

The `browserWindow` argument allows the dialog to attach itself to a parent window, making it modal.

The `filters` specifies an array of file types that can be displayed, see
`dialog.showOpenDialog` for an example.

If a `callback` is passed, the API call will be asynchronous and the result
will be passed via `callback(filename)`.

### `dialog.showMessageBox([browserWindow, ]options[, callback])`

* `browserWindow` [BrowserWindow](browser-window.md) (optional)
* `options` Object
  * `type` string (optional) - Can be `"none"`, `"info"`, `"error"`, `"question"` or
  `"warning"`. On Windows, `"question"` displays the same icon as `"info"`, unless
  you set an icon using the `"icon"` option. On macOS, both `"warning"` and
  `"error"` display the same warning icon.
  * `buttons` string[] (optional) - Array of texts for buttons. On Windows, an empty array
    will result in one button labeled "OK".
  * `defaultId` Integer (optional) - Index of the button in the buttons array which will
    be selected by default when the message box opens.
  * `title` string (optional) - Title of the message box, some platforms will not show it.
  * `message` string - Content of the message box.
  * `detail` string (optional) - Extra information of the message.
  * `checkboxLabel` string (optional) - If provided, the message box will
    include a checkbox with the given label. The checkbox state can be
    inspected only when using `callback`.
  * `checkboxChecked` boolean (optional) - Initial checked state of the
    checkbox. `false` by default.
  * `icon` [NativeImage](native-image.md) (optional)
  * `cancelId` Integer (optional) - The index of the button to be used to cancel the dialog, via
    the `Esc` key. By default this is assigned to the first button with "cancel" or "no" as the
    label. If no such labeled buttons exist and this option is not set, `0` will be used as the
    return value or callback response.
  * `noLink` boolean (optional) - On Windows Electron will try to figure out which one of
    the `buttons` are common buttons (like "Cancel" or "Yes"), and show the
    others as command links in the dialog. This can make the dialog appear in
    the style of modern Windows apps. If you don't like this behavior, you can
    set `noLink` to `true`.
  * `normalizeAccessKeys` boolean (optional) - Normalize the keyboard access keys
    across platforms. Default is `false`. Enabling this assumes `&` is used in
    the button labels for the placement of the keyboard shortcut access key
    and labels will be converted so they work correctly on each platform, `&`
    characters are removed on macOS, converted to `_` on Linux, and left
    untouched on Windows. For example, a button label of `Vie&w` will be
    converted to `Vie_w` on Linux and `View` on macOS and can be selected
    via `Alt-W` on Windows and Linux.
* `callback` Function (optional)
  * `response` Number - The index of the button that was clicked.
  * `checkboxChecked` boolean - The checked state of the checkbox if
    `checkboxLabel` was set. Otherwise `false`.

Returns `Integer`, the index of the clicked button, if a callback is provided
it returns undefined.

Shows a message box, it will block the process until the message box is closed.
It returns the index of the clicked button.

The `browserWindow` argument allows the dialog to attach itself to a parent window, making it modal.

If a `callback` is passed, the dialog will not block the process. The API call
will be asynchronous and the result will be passed via `callback(response)`.

### `dialog.showErrorBox(title, content)`

* `title` string - The title to display in the error box.
* `content` string - The text content to display in the error box.

Displays a modal dialog that shows an error message.

This API can be called safely before the `ready` event the `app` module emits,
it is usually used to report errors in early stage of startup. If called
before the app `ready`event on Linux, the message will be emitted to stderr,
and no GUI dialog will appear.

### `dialog.showCertificateTrustDialog([browserWindow, ]options, callback)` _macOS_ _Windows_

* `browserWindow` [BrowserWindow](browser-window.md) (optional)
* `options` Object
  * `certificate` [Certificate](structures/certificate.md) - The certificate to trust/import.
  * `message` string - The message to display to the user.
* `callback` Function

On macOS, this displays a modal dialog that shows a message and certificate
information, and gives the user the option of trusting/importing the
certificate. If you provide a `browserWindow` argument the dialog will be
attached to the parent window, making it modal.

On Windows the options are more limited, due to the Win32 APIs used:

 - The `message` argument is not used, as the OS provides its own confirmation
   dialog.
 - The `browserWindow` argument is ignored since it is not possible to make
   this confirmation dialog modal.

## Sheets

On macOS, dialogs are presented as sheets attached to a window if you provide
a [`BrowserWindow`](browser-window.md) reference in the `browserWindow` parameter, or modals if no
window is provided.

You can call `BrowserWindow.getCurrentWindow().setSheetOffset(offset)` to change
the offset from the window frame where sheets are attached.
