---
layout: post
title: "Angular NgClass directive example"
categories: angular
---

Below is an example `ngClass` angular directive.

```
<h2
  [ngClass]="{
    'text-color': isActive,
    'text-transform': isActive
  }">
  NgClass Directive Example
</h2>
```

The `isActive` is a variable that's defined at xx.component.ts
