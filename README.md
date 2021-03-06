# zend-expressive-authentication-session

[![Build Status](https://secure.travis-ci.org/zendframework/zend-expressive-authentication-session.svg?branch=master)](https://secure.travis-ci.org/zendframework/zend-expressive-authentication-session)
[![Coverage Status](https://coveralls.io/repos/github/zendframework/zend-expressive-authentication-session/badge.svg?branch=master)](https://coveralls.io/github/zendframework/zend-expressive-authentication-session?branch=master)

This library provides a [zend-expressive-authentication](https://github.com/zendframework/zend-expressive-authentication/)
adapter that handles form-based username/password authentication credentials
where the user details are subsequently stored in a session.

## Installation

Run the following to install this library:

```bash
$ composer require zendframework/zend-expressive-authentication-session
```

## Configuration

You will need to provide configuration for this module to work correctly. The
following demonstrates:

- Mapping a custom `UserRepositoryInterface` implementation for use as a backend
  to the functionality this authentication adapter provides.
- Mapping the `PhpSession` adapter as the `AuthenticationInterface`
  implementation to use in your application.
- Providing configuration for this adapter, including custom field names for the
  username and password, as well as a path in the application to which to redirect
  when no valid credentials are present.

```php
<?php
// in a config/autoload/*.global.php file:

declare(strict_types=1);

//use App\Infrastructure\Repository\UserRepository;
//use App\Infrastructure\Repository\UserRepositoryFactory;
use Zend\Expressive\Authentication\AuthenticationInterface;
use Zend\Expressive\Authentication\Session\PhpSession;
use Zend\Expressive\Authentication\UserRepositoryInterface;

return [
    'dependencies' => [
        'aliases' => [
            AuthenticationInterface::class => PhpSession::class,
            UserRepositoryInterface::class => UserRepository::class,
        ],

        'factories' => [
            UserRepository::class => UserRepositoryFactory::class,
        ],
    ],

    'authentication' => [
        'username' => null, // provide a custom field name for the username
        'password' => null, // provide a custom field name for the password
        'redirect' => '/login', // URI to which to redirect if no valid credentials present
    ],
];
```

## Documentation

Documentation is [in the doc tree](docs/book/), and can be compiled using [mkdocs](http://www.mkdocs.org):

```bash
$ mkdocs build
```

You may also [browse the documentation online](https://docs.zendframework.com/zend-expressive-authentication-session/).
