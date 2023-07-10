---
layout: post
title: "Angular template driven example"
categories: angular
---

This is just an example of template driven in angular

```
<div class="form-input">
    <form #f="ngForm" (ngSubmit)="onSubmit(f)">
      <div class="form-group">
        <label>Fullname</label>
        <input
          ngModel
          type="text"
          placeholder="Fullname"
          class="form-control"
          name="fullName"
          minlength="5"
          maxlength="50"
          #fullName="ngModel"
          [ngClass]="{ 'is-invalid': fullName.invalid && fullName.touched }"
          required
          >
        <div *ngIf="fullName.errors?.['required']">
          <div class="alert alert-danger" *ngIf="fullName.invalid && fullName.touched">Fullname is required</div>
        </div>
        <div *ngIf="fullName.errors?.['minlength']">
          <div class="alert alert-danger" *ngIf="fullName.invalid && fullName.touched">Fullname minimum is 5 characters</div>
        </div>
      </div>

      <div class="form-group">
        <label>Email</label>
        <input
          ngModel
          type="email"
          placeholder="email"
          class="form-control"
          name="email"
          #email="ngModel"
          [ngClass]="{ 'is-invalid': email.invalid && email.touched }"
          pattern="[a-z0-9._%+\-]+@[a-z0-9.\-]+\.[a-z]{2,}$"
          required
          >
        <div *ngIf="email.errors?.['required']">
          <div class="alert alert-danger" *ngIf="email.invalid && email.touched">Email is required</div>
        </div>
        <div *ngIf="email.errors?.['pattern']">
          <div class="alert alert-danger" *ngIf="email.invalid && email.touched">Email format is invalid</div>
        </div>
      </div>

      <div class="form-group">
        <label>Address</label>
        <textarea
          ngModel
          rows="5"
          cols="25"
          class="form-control"
          name="address"
          #address="ngModel"
          [ngClass]="{ 'is-invalid': address.invalid && address.touched }"
          minlength="5"
          required
        ></textarea>
        <div *ngIf="address.errors?.['required']">
          <div class="alert alert-danger" *ngIf="address.invalid && address.touched">Address is required</div>
        </div>
        <div *ngIf="address.errors?.['minlength']">
          <div class="alert alert-danger" *ngIf="address.invalid && address.touched">Address minimum is 5 characters</div>
        </div>
      </div>

      <button class="btn btn-primary" [disabled]="f.invalid">Submit</button>
    </form>
</div>
```