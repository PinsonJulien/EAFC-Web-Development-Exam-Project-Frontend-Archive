# (ARCHIVED) School Website Frontend Angular

## Archive note
This repository will be archived as of **08/02/2022 (D/M/Y), 9PM (UTC+1 Brussels)** for school access.
You can find the forked repository (here)[  WRITE URL ]

## Context
This repository is part of the web development course of my bachelor degree in Business Computing, 2nd year.
You can consult the *scope statement* (in French) in the `scope.pdf` file at root.

I chose to use **Angular 15** for my frontend.
This frontend should match the same URL set in the backend, as it relies on CSRF protection by cookies.

## Minimal requirements
- [NodeJS v16.13.1](https://nodejs.org/en/download/)
- NPM v8.3.0 (included with NodeJS)
- Backend from this [repository](https://github.com/PinsonJulien/school-website-backend-laravel)
- [Angular CLI v15.1.4](https://angular.io/guide/setup-local#install-the-angular-cli)

## Initial setup 
- If it's not done, install the Angular CLI : `npm install -g @angular/cli`
- run `npm install`
- In `src/environments/enronment.ts`, make sure the `baseUrl` matches the backend URL, including the port.

## Development server
Run `ng serve` and access the application at `http://127.0.0.1:4200/`.

## Contribution tools

### Useful commands
- Build : `ng build`
- Unit test (Karma): `ng test`
- E2E test : `ng e2e`

### Project evolutions

### Ideas
- Accessibility with theme color pickers.
- Keep the favorite language (or the one selected before login / register) in state, use it to fill the favorite language field default value on registration.

### Possible improvements / todo

- Overall styling :
  - Customize the color scheme of Angular Material.

- AppComponent
  - Should handle the session expiration by listening to every store errors, will redirecto to /login

- AuthLayout
  - Fix the styling.

- RegisterPage (Lot of rework)
  - Form should be in a [linear stepper](https://material.angular.io/components/stepper/overview)
  - Mark invalid the username or email on 422 error + specified field.
    - Keep already existing email/username in an array for validation.
  - Use the CountryStore instead of the service. Only fetch once.

- RegisterPage & LoginPage
  - Should have a function called "setupFormErrors()"
    - Remove all the "get...ErrorMessage" methods.
    - Errors will be set like so : `control.setErrors({'required': 'Field is required'});`
    - Html : Errors will be handled like so :
```
<div *ngIf="form.get('fieldName').invalid && form.get('fieldName').touched">
  <div *ngIf="form.get('fieldName').errors['required']">
    {{ form.get('fieldName').errors['required'] }}
  </div>
  <div *ngIf="form.get('fieldName').errors['custom']">
    {{ form.get('fieldName').errors['custom'] }}
  </div>
</div>
```

- Enrollments : History
  - Show enrollments in drawers instead for tables for better responsivity.
  - Button to show the message that are not null, on enrollments that aren't *pending*

- Admin
  - Enrollments
    - Table sort by the header, triggers a change in array of sorts

- AuthStoreService : 
  - Store the session expiration date and react to it for automatic disconnection ? Localstorage ?

- User experience : 
  - Show loading on async pipes maybe using this solution : https://medium.com/angular-in-depth/angular-show-loading-indicator-when-obs-async-is-not-yet-resolved-9d8e5497dd8
  - Always show a snackBar on requests where the user interacts (post, patch, delete)
  - On login, if  the role is secretary, redirect to */admin* instead of */home*


### Backend features that aren't implemented 

## Urgent todo :
- Banned page (fast) + fix the routes in backend to allow disconnect.
- Fix user storage to be on ID.

- AuthStore should only store the user id in local storage and perform a getById on instantiation. This will ensure the right user is logged in and no personal data is locally stored. If the UserApiService got an authorization error, the store will trigger the logout().
