# Firebase for Laravel

A Laravel package for the [Firebase PHP Admin SDK](https://github.com/kreait/firebase-php).

[![Current version](https://img.shields.io/packagist/v/kreait/laravel-firebase.svg?logo=composer)](https://packagist.org/packages/kreait/laravel-firebase)
[![Monthly Downloads](https://img.shields.io/packagist/dm/kreait/laravel-firebase.svg)](https://packagist.org/packages/kreait/laravel-firebase/stats)
[![Total Downloads](https://img.shields.io/packagist/dt/kreait/laravel-firebase.svg)](https://packagist.org/packages/kreait/laravel-firebase/stats)
[![Tests](https://github.com/kreait/laravel-firebase/workflows/Tests/badge.svg?branch=main)](https://github.com/kreait/laravel-firebase/actions)
[![codecov](https://codecov.io/gh/kreait/laravel-firebase/branch/main/graph/badge.svg)](https://codecov.io/gh/kreait/laravel-firebase)
[![Sponsor](https://img.shields.io/static/v1?logo=GitHub&label=Sponsor&message=%E2%9D%A4&color=ff69b4)](https://github.com/sponsors/jeromegamez)

- [Installation](#installation)
  - [Laravel](#laravel)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Multiple projects](#multiple-projects)
- [Supported Versions](#supported-versions)
- [License](#license)

## Installation

```bash
composer require kreait/laravel-firebase
```

## Configuration

In order to access a Firebase project and its related services using a server SDK, requests must be authenticated.
For server-to-server communication this is done with a Service Account.

The package uses auto discovery for the default project to find the credentials needed for authenticating requests to
the Firebase APIs by inspecting certain environment variables and looking into Google's well known path(s).

If you don't want a service account to be auto-discovered, provide it by setting the `GOOGLE_APPLICATION_CREDENTIALS`
environment variable or by adapting the package configuration.

If you don't already have generated a Service Account, you can do so by following the instructions from the
official documentation pages at https://firebase.google.com/docs/admin/setup#initialize_the_sdk.

Once you have downloaded the Service Account JSON file, you can configure the package by specifying
environment variables starting with `FIREBASE_` in your `.env` file. Usually, the following are
required for the package to work:

```
# You can find the database URL for your project at
# https://console.firebase.google.com/project/_/database
FIREBASE_DATABASE_URL=https://<your-project>.firebaseio.com
```

For further configuration, please see [config/firebase.php](config/firebase.php). You can modify the configuration
by copying it to your local `config` directory or by defining the environment variables used in the config file:

```bash
# Laravel
php artisan vendor:publish --provider="Kreait\Laravel\Firebase\ServiceProvider" --tag=config
```

## Usage

Once you have retrieved a component, please refer to the [documentation of the Firebase PHP Admin SDK](https://firebase-php.readthedocs.io)
for further information on how to use it.

**You don't need and should not use the `new Factory()` pattern described in the SDK documentation, this is already
done for you with the Laravel Service Provider. Use Dependency Injection, the Facades or the `app()` helper instead**

### Multiple projects

Multiple projects can be configured in [config/firebase.php](config/firebase.php) by adding another section to the projects array.

When accessing components, the facade uses the default project. You can also explicitly use a project:

```php
use Kreait\Laravel\Firebase\Facades\Firebase;

// Return an instance of the Auth component for the default Firebase project
$defaultAuth = Firebase::auth();
// Return an instance of the Auth component for a specific Firebase project
$appAuth = Firebase::project('app')->auth();
$anotherAppAuth = Firebase::project('another-app')->auth();
```

## Supported Versions

**Only the latest version is actively supported.**

Earlier versions will receive security fixes as long as their **lowest** SDK requirement receives security fixes. You
can find the currently supported versions and support options in the [SDK's README](https://github.com/kreait/firebase-php).

| Version | Initial Release | Supported SDK Versions | Supported Laravel Versions | Status         |
|---------|-----------------|------------------------|----------------------------|----------------|
| `5.x`   | 13 Jan 2023     | `^7.0`                 | `^9.0`                     | Active support |
| `4.x`   | 09 Jan 2022     | `^6.0`                 | `^8.0`                     | End of life    |
| `3.x`   | 01 Nov 2020     | `^5.24`                | `^6.0, ^7.0, ^8.0`         | End of life    |
| `2.x`   | 01 Apr 2020     | `^5.0`                 | `^5.8, ^6.0, ^7.0, ^8.0`   | End of life    |
| `1.x`   | 17 Aug 2019     | `^4.40.1`              | `^5.8, ^6.0, ^7.0`         | End of life    |

## License

This project is licensed under the [MIT License](LICENSE).

Your use of Firebase is governed by the [Terms of Service for Firebase Services](https://firebase.google.com/terms/).
