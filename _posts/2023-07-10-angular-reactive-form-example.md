---
layout: post
title: "Angular reactive form example"
categories: angular
---

This is just an example of reactive form in angular

```
<div class="form-input">
    <h2>Reactive Form</h2>
    <form [formGroup]="form">
      <div class="form-group">
        <label>Fullname</label>
        <input
          type="text"
          placeholder="Fullname"
          class="form-control"
          [ngClass]="{'is-invalid': fullName.invalid && fullName.touched}"
          name="fullName"
          formControlName="fullName"
          required
        >
        <div class="alert alert-danger" *ngIf="fullName.invalid && fullName.touched">
          <div  *ngIf="fullName.errors.required">Fullname is required</div>
          <div  *ngIf="fullName.errors.minlength">Fullname minimum 5 characters</div>
        </div>

      </div>

      <div class="form-group">
        <label>Email</label>
        <input
          type="email"
          placeholder="email"
          class="form-control"
          [ngClass]="{'is-invalid': email.invalid && email.touched}"
          name="email"
          (change)="getValue()"
          formControlName="email"
        >
        <div class="alert alert-danger" *ngIf="email.invalid && email.touched">
          <div  *ngIf="email.errors.required">Email is required</div>
          <div  *ngIf="email.errors.email">Invalid email format</div>
        </div>

      </div>

      <div class="form-group">
        <label>Address</label>
        <textarea
          rows="5"
          cols="25"
          class="form-control"
          [ngClass]="{'is-invalid': address.invalid && address.touched}"
          name="address"
          formControlName="address"
        ></textarea>

        <div class="alert alert-danger" *ngIf="address.invalid && address.touched">
          <div *ngIf="address.errors.required">Address required</div>
          <div *ngIf="address.errors.minlength">Address minimum length is 10</div>
        </div>
      </div>

      <button class="btn btn-primary" [disabled]="form.invalid">Submit</button>
    </form>
  </div>
```