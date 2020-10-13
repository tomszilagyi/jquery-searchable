jQuery Searchable Plugin
========================

Tiny, fast jQuery plugin to search through elements as you type.

## Features

- **Lightweight**. This plugin is only ~1kB minified and gzipped!

- **Fast**. This plugin is optimized for fast, lagless searching even
  through large element sets.

- **Multiple search types**. This plugin provides three different
  search types out-of-the-box! Fuzzy matching, strict (case sensitive)
  matching and default (case insensitive) matching. Also Helm-style
  multi-keyword narrowing search!

- **Automatic row striping**. When searching through a table, rows get
  hidden when they don't match. When using a CSS framework like
  [Bootstrap](http://getbootstrap.com) this would mess up your table
  striping. This plugin makes allows you to define the CSS to be
  applied to odd and even rows, and updates them while searching.

- **Custom show/hide**. You can define custom functions for showing
  and hiding the elements while searching.

- **Search anything**. This plugin isn't restricted to use on tables,
  any set of elements that has 'rows' with 'columns' inside them can
  be used.

## Getting started

### Basic usage

After downloading this plugin, include it in your HTML file after
loading jQuery:

```html
<script src="jquery.js"></script>
<script src="jquery.searchable.js"></script>
```

After that, you can simply initialize the plugin on the desired
element. This example uses a table with an id of 'table'. By default,
the plugin uses an input with an id of 'search' (read about how to
change this in the Configuration section below):

```js
$('#table').searchable ();
```

### Configuration

This plugin provides the following configuration options:

| Option  | Default value  | Description  |
| :------ | :------------- | :----------- |
| selector | `'tbody tr'` | Defines the main jQuery selector within the element on which the plugin is initialized. This selects the container elements to show or hide, such as `tr`s within a table, or a `div.your-special-class` within the searchable element.|
| childSelector | `'td'` | Defines the child selector within the 'selector' defined above. This selects the searchable elements within the 'selector' element, such as `td` or `.searchable`.|
| searchField | `'#search'` | The input element that is used for the search input filter |
| striped | `false` | Defines whether the element is striped and should be re-striped upon searching (either `true` or `false`) |
| oddRow | `{ }` | Defines the CSS object to apply to the odd rows (when `striped` is set to `true`). |
| evenRow | `{ }` | Defines the CSS object to apply to the even rows (when `striped` is set to `true`). |
| hide | `function` | Allows you to define a custom hiding function. This function accepts one parameter, which is the element (row) being hidden. By default it will use `elem.hide ()` to hide the row. |
| show | `function` | Allows you to define a custom show function. This function accepts one parameter, which is the element (row) being hidden. By default it will use `elem.show ()` to show the row. |
| getContent | `function` | Allows you to define a custom function to get the textual content of the elements being searched. This function accepts one parameter, which is the element being looked at, and should return a string with the content of this element. By default, `'elem.text ()'` is used. |
| searchType | `'default'` | Defines the matcher to be used when searching. Allowed values are `'fuzzy'`, `'helm'`, `'strict'` and `'default'`. |
| onSearchActive | `false` | Allows you to define a function to be called when the search is active. This function will be called whenever the user is typing into the search input and the search input is not empty. The searchable element and the search term will be passed to the function. |
| onSearchEmpty | `false` | Allows you to define a function to be called when the search input is empty. This function will be called once when the search input is empty or cleared. The searchable element will be passed to the function. |
| onSearchFocus | `false` | Allows you to define a function to be called when the search input is focussed. The `this` context of this function will be the search input element. |
| onSearchBlur | `false` | Allows you to define a function to be called when the search input is blurred. The `this` context of this function will be the search input element. |
| onAfterSearch | `false` | Allows you to define a function to be called after searchable has hidden/shown the elements. This can be used to count the number of elements being hidden/shown. |
| clearOnLoad | `false` | Determines whether the search input should be cleared on page load (either `true` or `false`). |
| ignoreDiacritics | `false` | Determines if diacritic letters should be ignored. For example, when searching for `u` -> `ú` and `ü` will also be found. |

### Example usage

This example uses the configurations shown above to customize the plugin:

```js
$('#element').searchable ({
    selector      : '.row',
    childSelector : '.column',
    searchField   : '#mySearchInput',
    striped       : true,
    oddRow        : { 'background-color': '#f5f5f5' },
    evenRow       : { 'background-color': '#fff' },
    hide          : function (elem) {
        elem.fadeOut (50);
    },
    show          : function (elem) {
        elem.fadeIn (50);
    },
    searchType    : 'fuzzy',
    onSearchActive : function (elem, term) {
        elem.show ();
    },
    onSearchEmpty: function (elem) {
        elem.hide ();
    },
    onSearchFocus: function () {
        $('#feedback').show ().text ('Type to search.');
    },
    onSearchBlur: function () {
        $('#feedback').hide ();
    },
    onAfterSearch: function () {
        // i.e. count number of items shown
    },
    clearOnLoad: true,
    ignoreDiacritics: true
});
```

Starting with version 1.1.3, it is also possible to configure the
content getter method used to read the text of the searched
elements. The default is to invoke the element's `text ()` method,
which is not always what you want. For example, if you are searching
on `input` fields, you would do something like this:

```js
$('#element').searchable ({
    ...
    childSelector : 'input',
    getContent    : function (elem)
    {
        return elem [0].value;
    },
    ...
});
```

## Changelog

**Version 1.0.0:**

- Initial release.

**Version 1.1.0:**

- Added some events that allow you to call custom functions during the
  search lifecycle: onSearchActive, onSearchEmpty, onSearchFocus,
  onSearchBlur (view the [configuration](#configuration) for more
  information).

- Added the `clearOnLoad` setting which allows you to clear the search
  input on page load / refresh.

**Version 1.1.1:**

- Added onAfterSearch callback.

- Added ignoreDiacritics option. Default is false so it should be
  backwards compatible.

**Version 1.1.2:**

- Added searchType `helm` to support incremental narrowing on multiple
  space-separated keyword fragments as in Emacs Helm.

**Version 1.1.3:**

- Added ability to override text content getter method for searchable
  elements (useful if you want to e.g., search on form input fields)

- Removed ancillary files I do not care about

## Contributing & Issues

Please feel free to submit any issues or pull requests, they are more
then welcome. When submitting an issue, please specify the version
number and describe the issue in detail so that it can be solved as
soon as possible!

## License

Licensed under [the MIT license](LICENSE).

Copyright (c) 2020 - Tom Szilagyi

Copyright (c) 2014 - Stidges
