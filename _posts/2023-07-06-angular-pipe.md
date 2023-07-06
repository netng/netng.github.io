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

Usage example:

```
<h2>{{ title | lowercase }}</h2>

<h2>{{ count | number }}</h2>

<h2>{{ dcNumber | number: '1.0-0' }}</h2>

<h2>{{ price | currency: 'USD': false : '.1-3'  }}</h2>
```

Good to read: https://angular.io/guide/pipes