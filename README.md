![Robert Gramner - Unsplash (UL) #as2iiiiFdqk](https://images.unsplash.com/photo-1525069396440-d4c44fa51343?ixlib=rb-1.2.1&auto=format&fit=crop&w=1280&h=400&q=80)

[![Latest Stable Version](https://poser.pugx.org/darkghosthunter/passless/v/stable)](https://packagist.org/packages/darkghosthunter/passless) [![License](https://poser.pugx.org/darkghosthunter/passless/license)](https://packagist.org/packages/darkghosthunter/passless)
![](https://img.shields.io/packagist/php-v/darkghosthunter/passless.svg) [![Build Status](https://travis-ci.com/DarkGhostHunter/Passless.svg?branch=master)](https://travis-ci.com/DarkGhostHunter/Passless) [![Coverage Status](https://coveralls.io/repos/github/DarkGhostHunter/Passless/badge.svg?branch=master)](https://coveralls.io/github/DarkGhostHunter/Passless?branch=master) [![Maintainability](https://api.codeclimate.com/v1/badges/8f1790a00c264e287df4/maintainability)](https://codeclimate.com/github/DarkGhostHunter/Passless/maintainability) [![Test Coverage](https://api.codeclimate.com/v1/badges/8f1790a00c264e287df4/test_coverage)](https://codeclimate.com/github/DarkGhostHunter/Passless/test_coverage)

# Passless

Passwordless Authentication Driver for Laravel 5.7. Just add water.

## Requirements

* Laravel 5.7 (Lumen *may* work)

## What includes

* Passless Authentication Guard Driver
* `LoginAuthentication` Notification
* Resend Email Blade view
* Little magic

## How to use

Passless is easy to integrate into your application, but before start using it you should change some strings in your configuration to point your app to use this package.

Don't worry, it doesn't breaks your Laravel installation.

### 1) Add the Guard Driver

Go into your `config/auth.php` and add `passless` as the driver for your guard.

```
'guards' => [
    'web' => [
        'driver' => 'passless',
        'provider' => 'users',
    ],
    'api' => [
        'driver' => 'token',
        'provider' => 'users',
    ],
],
```

> Remember to set the correct guard (in this case, `web`) to use the passless driver in your Login controllers. 

### 2) Add the Login redirect to Passless

Since the user won't be logged in immediately into your application when his credentials are validated, you should return a view which Notifies the user to check his email with an alert.

While you are free to use any view to inform the user, you can just simply add a flash notification in your Login route.

If you're using the default controller, add or replace this code:

```php
/**
 * The user has been authenticated.
 *
 * @param  \Illuminate\Http\Request  $request
 * @param  mixed  $user
 * @return mixed
 */
protected function authenticated(Request $request, $user)
{
    return view('auth.login')->flash('message', 'Login Email Sent');
}
```

> Since there is no password check in the login form, you may want to add a throttler to your Login route to avoid Mail asphyxiation.

## Configuration

For fine tuning, publish the Passless configuration:

```bash
php artisan vendor:publish --provider="DarkGhostHunter\Passless\PasslessServiceProvider"
```

The contents of the config file are self-explanatory, so check the comments. 

You should definitively edit this config file if:

* You're using a custom authentication controllers.
* You're using additional middleware across your routes.
* Need a different Login for Passless.
* Want to use different Notification or Resend View.
* Modify the Resend throttle.

## License 

This package is licenced by the [MIT License](LICENSE).