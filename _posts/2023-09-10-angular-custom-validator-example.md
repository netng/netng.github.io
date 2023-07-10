---
layout: post
title: "Angular custom validator example"
categories: angular
---

```
import { AbstractControl, ValidationErrors } from "@angular/forms";

export class NoSpace {
  static noSpaceValidation(control: AbstractControl): ValidationErrors | null {
    let controlValue = control.value as string;

    if(controlValue.indexOf(' ') >= 0) {
      return { noSpaceValidator: true };
    } else {
      return null;
    }
  }
}
```

use on component.ts:

```
constructor(fb: FormBuilder) {
    this.form = fb.group({
      username: ['', [
        Validators.required,
        Validators.minLength(5),
        NoSpace.noSpaceValidation
      ]],
      password: ['', [
        Validators.required
      ]]
    })
  }
```

use on html template:
```
<div class="alert alert-danger" *ngIf="fc.username.errors.noSpaceValidator">Username can not contains any space</div>
```