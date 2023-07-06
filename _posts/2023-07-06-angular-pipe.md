---
layout: post
title: "Angular pipe"
categories: angular
---

Angular pipes is use for transforming data, like string, currency amount, dates, etc.

Exmaple of angular pipes:

- `uppercase`
- `lowercase`
- `currency`
- `number`
- `json`
- `date`
- `slice`
- `percent`

Usage example:

```
"<h2>{{ title | lowercase }}</h2>

<h2>{{ count | number }}</h2>

<h2>{{ dcNumber | number: '1.0-0' }}</h2>

<h2>{{ price | currency: 'USD': false : '.1-3'  }}</h2>

<h2>{{ today | date | uppercase }}</h2>

<p>{{ objValue | json }}</p>

<p>{{ 0.05467 | percent: '1.1-2' }}</p>

<p>{{ arrayValue | slice: 1:3 }}</p>"
```

Nice to read: https://angular.io/guide/pipes