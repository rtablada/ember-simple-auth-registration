# Ember Simple Auth Registration Authenticator

[![npm version](https://badge.fury.io/js/ember-simple-auth-registration.svg)](http://badge.fury.io/js/ember-simple-auth-registration)
[![Ember Observer Score](http://emberobserver.com/badges/ember-simple-auth-registration.svg)](http://emberobserver.com/addons/ember-simple-auth-registration)
This addon provides an OAuth2 password grant Authenticator that allows passing of user profile information for user registration.

## Installation

`ember install ember-simple-auth-registration`

## Use

In your application create an authorizer that extends from `oauth2-password-registration`:

```js
// app/authenticators/register.js
import Registration from 'ember-simple-auth-registration/authenticators/oauth2-password-registration';

export default Registration.extend();
```

Then in your registration action:

```js
let { identification, password } = this.getProperties('identification', 'password');
let userData = /* get your user data some way */ {};
this.get('session').authenticate('authenticator:register', identification, password, userData).catch((reason) => {
  this.set('errorMessage', reason.error || reason);
});
```

This will JSON stringify the `userData` variable and pass it as a `user_data` parameter to your server.

## Customization

You will likely want to customize the `registrationEndpoint` to match the API route for your registration:

```js
// app/authenticators/register.js
import Registration from 'ember-simple-auth-registration/authenticators/oauth2-password-registration';

export default Registration.extend({
  registrationEndpoint: '/api/register',
});
```
