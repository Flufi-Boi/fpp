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
