wabt.js
=======

**wabt.js** is a port of [WABT](https://github.com/WebAssembly/wabt), the WebAssembly Binary Toolkit, to the Web.

[![npm](https://img.shields.io/npm/v/wabt.svg)](https://www.npmjs.com/package/wabt) [![npm](https://img.shields.io/npm/v/wabt/nightly.svg)](https://www.npmjs.com/package/wabt)

Usage
-----

```
$> npm install wabt
```

```js
var wabt = require("wabt");

var wasm = ...; // a buffer holding the contents of a wasm file

var myModule = wabt.readWasm(wasm, { readDebugNames: true });
myModule.applyNames();

var wast = myModule.toText({ foldExprs: false, inlineExport: false });

console.log(wast);
```

API
---

* **parseWast**(filename: `string`, buffer: `string | Uint8Array`): `WasmModule`<br />
  Parses a wast source to a module.
* **readWasm**(buffer: `Uint8Array`, options: `IReadWasmOptions`): `WasmModule`<br />
  Reads a wasm binaryen to a module.

* **WasmModule**<br />
  A class representing a WebAssembly module.

  * **generateNames**(): `void`<br />
    Generates textual names for function types, globals, labels etc.
  * **applyNames**(): `void`<br />
    Applies textual names.
  * **toText**(options: `IToTextOptions`): `string`<br />
    Converts the module to wast text format.
  * **toBinary**(options: `IToBinaryOptions`): `IToBinaryResult`<br />
    Converts the module to a wasm binary.
  * **destroy**(): `void`<br />
    Disposes the module and frees its resources.

* **IReadWasmOptions**<br />
  Options modifying the behavior of `readWasm`.

   * **readDebugNames**: `boolean`<br />
     Reads textual names from the name section.

* **IToTextOptions**<br />
  Options modifying the behavior of `WasmModule#toText`.

  * **foldExprs**: `boolean`
  * **inlineExport**: `boolean`

* **IToBinaryOptions**<br />
  Options modifying the behavior of `WasmModule#toBinary`.

  * **log**: `boolean`
  * **canonicalize_lebs**: `boolean`
  * **relocatable**: `boolean`
  * **write_debug_names**: `boolean`

* **IToBinaryResult**<br />
  Result object of `WasmModule#toBinary`.

  * **buffer**: `Uint8Array`<br />
    The wasm binary buffer.

  * **log**: `string`<br />
    Generated log output.
