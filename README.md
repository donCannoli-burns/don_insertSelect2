# insertSelect2

Function for KoLmafia scripts to make `<select>` HTML elements searchable on a given page. It does this by reading in a given page, then outputting the page modified to make use of [select2](https://select2.org/) to facilitate that.

A repo with some already-made relay override scripts making use of this for a few pages can be found here: https://github.com/donCannoli-burns/don_insertSelect2-relays

## Installation

Can be installed from KoLmafia's CLI via:

```
git checkout https://github.com/donCannoli-burns/don_insertSelect2.git
```

## Usage

`import`ing this script gives access to this function:

```java
string insertSelect2(string page,string option)
```

* `page` is the HTML of some page to modify
* `option` is optional and is used to change select2-specific options, especially if the defaults are inadequate on a particular page
* `return`s `page` modified to make use of [select2](https://select2.org/) to make `<select>` HTML elements searchable

### Usage examples

Cribbing from [Ezandora's Choice Override](https://github.com/Ezandora/Choice-Override) script for examples here, since choice override scripts are probably where this script would get the most usage. However, this script can be used with any page that can be overridden with a relay script to make any `<select>` elements there searchable.

#### ASH

```java
import "relay/choice.ash"
import <insertSelect2.ash>

void main(string page_text_encoded)
{
	string page_text = page_text_encoded.choiceOverrideDecodePageText();

	page_text = insertSelect2(page_text);

	//modify page_text in other ways here

	write(page_text);
}
```

#### JavaScript

```javascript
const kol = require("kolmafia");

module.exports.main = function (page_text_encoded)
{
	var choice_override_script = require("relay/choice.ash");
	var page_text = choice_override_script.choiceOverrideDecodePageText(page_text_encoded);

	//insertSelect2
	const { insertSelect2 } = require("insertSelect2.ash");
	page_text = insertSelect2(page_text);

	//modify page_text in other ways here

	kol.write(page_text);
}
```

## Fork provenance and compatibility

This repository is a fork of [C2Talon's insertSelect2](https://github.com/C2Talon/insertSelect2), which provides the original function and usage pattern. See the upstream project for original credit and documentation. The example installation command above installs **this fork**; the linked [relay overrides](https://github.com/donCannoli-burns/don_insertSelect2-relays) are a separate optional checkout.

In [don_custom_functions](https://github.com/donCannoli-burns/don_custom_functions), the `don_relay_select2.ash` HTML class-tagging helper is **not** a drop-in replacement for the complete Select2 frontend provided by this script.

## Related maintained KoLmafia / ASH projects

- [don-ash-lib](https://github.com/donCannoli-burns/don-ash-lib) — reusable import-safe ASH utilities.
- [don_custom_functions](https://github.com/donCannoli-burns/don_custom_functions) — runnable KoLmafia ASH commands and related relay integration.

These are **separate repositories**, not implicit dependencies installed by this fork. The standalone retirement program for `boneFarm`, `boneTrack.ash`, and `codMaster` is documented at [Retired-KOL-Scripts](https://github.com/donCannoli-burns/Retired-KOL-Scripts). This fork is **not** one of those three retiring scripts.
