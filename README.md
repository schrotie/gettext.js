# gettext.js

gettext.js is a lightweight (3k minified!) yet complete and accurate GNU
gettext port for node and the browser. Manage your i18n translations the right
way in your javascript projects.


## Why another i18n javascript library?

gettext.js aim is to port the famous GNU gettext and ngettext functions to
javascript node and browser applications.
It should be standards respectful and lightweight (no dictionary loading
management, no extra features).

The result is a < 200 lines javascript tiny lib yet implementing fully
`gettext()` and `ngettext()` and having the lighter json translation files
possible (embeding only translated forms, and not much headers).

There are plenty good i18n libraries out there, notably
[Jed](https://github.com/SlexAxton/Jed) and [i18n-next](http://i18next.com/),
but either there are too complex and too heavy, or they do not embrace fully
the gettext API and philosophy.

There is also [gettext.js](https://github.com/Orange-OpenSource/gettext.js)
which is pretty good and heavily inspired this one, but not active since 2012
and without any tests.


## Installation

### Node

Install the lib with the following command: `npm install gettext.js --save`

Require it in your project:

```javascript
var i18n = require('gettext.js');
i18n.gettext('foo');
```

### Browser

```html
<script src="/PATH/TO/gettext.js" type="text/javascript"></script>
<script>
  window.i18n.gettext('foo');
</script>
```

## Usage

### Load your messages

### `gettext(msgid)`

Translate a string.

### `ngettext(msgid, msgid_plural, n)`

Translate a pluralizable string

### Variabilized strings

`gettext('There are %1 in the %2`, 'apples', 'bowl'); -> "There are apples in the bowl`
`ngettext('One %2', '%1 %2', 10, 'bananas'); -> "10 bananas"`

It uses the public method `i18n.strfmt("string", var1, var2, ...)` you could
reuse elsewhere in your project.

## Required JSON format

You'll find in `/bin` a `po2json.js` converter, based on the excellent
[po2json](https://github.com/mikeedwards/po2json) project that will dump your
`.po` files into the proper json format below:

```json
{
    "": {
        "lang": "en",
        "plural_forms": "nplurals=2; plural=(n!=1);"
    },
    "simple key": "It's tranlation",
    "another with %1 parameter": "It's %1 tranlsation",
    "a key with plural": [
        "a plural form",
        "another plural form",
        "could have up to 6 forms with some languages"
    ],
    "a context\u0004a contextualized key": "translation here"
}
```

Use `bin/po2json.js input.po output.json` or
`bin/po2json.js input.po output.json -p` for pretty format.

## Parsers

## License

MIT
