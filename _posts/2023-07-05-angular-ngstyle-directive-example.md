---
layout: post
title: "Angular NgStyle directive example"
categories: angular
---

Below is an example `ngStyle` angular directive.

```
<h2
  [ngStyle]="{
    color: isActive ? 'red' : 'black',
    textTransform: isActive ? 'uppercase' : 'lowercase'
  }">
  NgStyle Directive Example
</h2>
```

The `isActive` is a variable that's defined at xx.component.ts
