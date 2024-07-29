<p align="center"><a href="https://medv.io/codejar/"><img src="https://medv.io/assets/codejar.svg" width="72"></a></p>
<h3 align="center">CodeJar – an embeddable code editor for the browser</h3>

[![npm](https://img.shields.io/npm/v/codejar-async?color=brightgreen)](https://www.npmjs.com/package/codejar-async)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/codejar-async?label=size)](https://bundlephobia.com/result?p=codejar-async)

**CodeJar-Async** is a fork of [CodeJar](https://medv.io/codejar/) with async highlighting support.

## Features

* Lightweight (**2.5 kB** only)
* No dependencies
* Preserves indentation on a new line
* Adds closing brackets, quotes
* Indents line with the **Tab** key
* Supports **undo**/**redo**
* **Async** highlighting (${\color{red}NEW}$)$\textcolor{red}{\textsf{NEW}}$

## Getting Started

Install CodeJar-Async 🍯 &nbsp; via npm:

```bash
npm i codejar-async
```

Create an element and init the CodeJar 🍯:

```html
<div class="editor"></div>
<script>
  let jar = CodeJar(document.querySelector('.editor'), highlight)
</script>
```

Second argument to `CodeJar` is an async highlighting function (like Prism.js, highlight.js):

```ts
const highlight = async (editor: HTMLElement): string => {
  const code = editor.textContent
  return code.replace('foo', '<span style="color: red">foo</span>')
}

const jar = CodeJar(editor, highlight)
```

Third argument to `CodeJar` is options:

- `tab: string` replaces "tabs" with given string. Default: `\t`.
  - Note: use css rule `tab-size` to customize size.
- `spellcheck: boolean` enables spellchecking on the editor. Default `false`.
- `catchTab: boolean` catches Tab keypress events and replaces it with `tab` string. Default: `true`.
- `preserveIdent: boolean` keeps indent levels on new line. Default `true`.
- `addClosing: boolean` automatically adds closing brackets, quotes. Default `true`.
- `history` records history. Default `true`.
- `window` window object. Default: `window`.

```js
const options = {
  tab: ' '.repeat(4), // default is '\t'
}

const jar = CodeJar(editor, highlight, options)
```

## API

### `updateCode(string)`

Updates the code.

```js
jar.updateCode(`let foo = bar`)
```

### `updateOptions(Partial<Options>)`

Updates the options.

```js
jar.updateOptions({tab: '\t'})
```

### `onUpdate((code: string) => void)`

Calls callback on code updates.

```js
jar.onUpdate(code => {
  console.log(code)
})
```

### `onHighlight((editor: HTMLElement) => void)`

Calls callback after the async highlighting is done.

```js
jar.onHighlight(editor => {
  console.log(editor.innerHTML)
})
```

### `toString(): string`

Return current code.

```js
let code = jar.toString()
```

### `save(): string`

Saves current cursor position.

```js
let pos = jar.save()
```

### `restore(pos: Position)`

Restore cursor position.

```js
jar.restore(pos)
```

### `recordHistory()`

Saves current editor state to history.

### `destroy()`

Removes event listeners from editor.

## Related

* [react-codejar](https://github.com/guilhermelimak/react-codejar) - a React wrapper for CodeJar.
* [ngx-codejar](https://github.com/julianpoemp/ngx-codejar) - an Angular wrapper for CodeJar.
* [codejar-linenumbers](https://github.com/julianpoemp/codejar-linenumbers) - an JS library for line numbers.

## License

[MIT](LICENSE)
