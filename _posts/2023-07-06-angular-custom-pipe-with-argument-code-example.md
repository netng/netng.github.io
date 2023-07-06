---
layout: post
title: "Angular custom pipe with argument code example"
categories: angular
---

`ng g pipe pipe-name`

```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'summarize'
})
export class SummarizePipe implements PipeTransform {

  transform(value: string, length?: number, ellipis?: string): unknown {
    if (!ellipis){
      ellipis = "...";
    }

    if (!length){
      length = 50;
    }

    return `${value.substring(0, length) + ellipis}`;
  }

}
```

call the pipe on the angular html template:

`{{ theSuperStringExample | summarize: 160 : ",,," }}`
