---
title: "Prism.js"
linkTitle: "Prism.js"
weight: 13
Description: >
  Prism.js
---

# Code Snippets with Prism.js

```powershell
Measure-Command {
    $list = [System.Collections.Generic.List[string]]::new()
    foreach ($num in 1..1000000) {
        $null = $list.Add("$num")
    }
}
Measure-Command {
    $list = [System.Collections.Generic.List[string]]::new()
    1..1000000 | foreach-object {$null = $list.Add("$_")}
}
```

```javascript
const Var = "Hi!";
console.log(`${Var} world!`);
```
