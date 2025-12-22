# fpp
origin os project manager (fork of [opal](https://github.com/originOSL/opal/tree/main))

# additions (to opal)

## include
include allows you to... well include other files that arent specified with import("name")
```json5
{
  /* ... */
  "include": ["./module.osl"]
}
```

## icon
simple icon parameter in opal.json that sets the built osl file's icon
```json5
{
  /* ... */
  "icon": "icn code"
}
```

## 'asset' importing
fpp allows you to also include non osl files, such as js files,

lets say in the project structure
```
myProject
|- script.osl
\- randomScript.js
```

fpp allows you to do
```js
myScript @= import("./randomScript.js")
log myScript // the contents of randomScript.js as a string
```

and have that be packaged alongside the .osl files,
> [!NOTE]
> you will need `__import @= import;import @= i -> (i.endsWith(".osl") ? __import(i) open(i))` in your base script.osl if you want this functionality without fpp, but isnt required to build as fpp automatically removes it

## scripts system
terminal commands in opal.json that can be executed by `fpp script <name>`
```json5
{
  ...,
  "scripts": {
    "myScript": "echo hi!",
    "myOtherScript": [
      "echo im a command",
      "echo im another command"
    ]
  }
}
```

## build global variable
fpp provides a `build` global variable with the structure:
```json5
{
  "built": true/false,
  "package": /* opal.json */
}
```

> [!NOTE]
> similarly to imports, you will need `build ??= { built: false, package: import("./opal.json").JsonParse() }` if you are running it without fpp, and fpp does also automatically remove this.
