---
layout: post
title: "Angular custom pipe example"
categories: angular
---

In particular situation, the built in angular pipes might not full fill for our situation. So, we can create our own custom pipes.

1. Create file with naming convention like this, end with `.pipe.ts`, but its up to you, its just follow the naming convention:

`example.pipe.ts`

Fill out that file with this code:

```
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({name: "example"})
export class ExamplePipe implements PipeTransform {
    transform(value: any, args?: any) {
        return "City name : " + value;
    }
}
```

2. Register to angular `@NgModule` at `app.module.ts` in `declarations` section:
```
......
......
declarations: [
    AppComponent,
    AppendPipe
  ],
.....
```

Thats all!, to use that pipe, we can use on the html template like this:

```
<p>{{ 'Indonesia' | example }}</p>
```
