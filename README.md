# middlewares/firewall

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE.md)
[![Build Status][ico-travis]][link-travis]
[![Quality Score][ico-scrutinizer]][link-scrutinizer]
[![Total Downloads][ico-downloads]][link-downloads]
[![SensioLabs Insight][ico-sensiolabs]][link-sensiolabs]

Middleware to provide IP filtering using [M6Web/Firewall](https://github.com/M6Web/Firewall).

**Note:** This middleware is intended for server side only

## Requirements

* PHP >= 5.6
* A [PSR-7](https://packagist.org/providers/psr/http-message-implementation) http mesage implementation ([Diactoros](https://github.com/zendframework/zend-diactoros), [Guzzle](https://github.com/guzzle/psr7), [Slim](https://github.com/slimphp/Slim), etc...)
* A [PSR-15](https://github.com/http-interop/http-middleware) middleware dispatcher ([Middleman](https://github.com/mindplay-dk/middleman), etc...)

## Installation

This package is installable and autoloadable via Composer as [middlewares/firewall](https://packagist.org/packages/middlewares/firewall).

```sh
composer require middlewares/firewall
```

## Example

```php
$dispatcher = new Dispatcher([
	(new Middlewares\Firewall(['123.0.0.*']))
        ->blacklist([
            '123.0.0.1',
            '123.0.0.2',
        ])
]);

$response = $dispatcher->dispatch(new ServerRequest());
```

## Options

#### `__construct(array $whitelist)`

An array with the whitelist ips. [See the ip formats allowed](https://github.com/M6Web/Firewall#entries-formats).

#### `blacklist(array $blacklist)`

The blacklist ips. The ip format is the same than whitelist.

#### `ipAttribute(string $ipAttribute)`

By default uses the `REMOTE_ADDR` server parameter to get the client ip. This option allows to use a request attribute. Useful to combine with any ip detection middleware, for example [client-ip](https://github.com/middlewares/client-ip):

```php
$dispatcher = new Dispatcher([
    //detect the client ip and save it in client-ip attribute
    new Middlewares\ClientIP(),

    //use that attribute
    (new Middlewares\Firewall(['123.0.0.*']))
        ->ipAttribute('client-ip')
]);
```

---

Please see [CHANGELOG](CHANGELOG.md) for more information about recent changes and [CONTRIBUTING](CONTRIBUTING.md) for contributing details.

The MIT License (MIT). Please see [LICENSE](LICENSE) for more information.

[ico-version]: https://img.shields.io/packagist/v/middlewares/firewall.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/middlewares/firewall/master.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/g/middlewares/firewall.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/middlewares/firewall.svg?style=flat-square
[ico-sensiolabs]: https://img.shields.io/sensiolabs/i/0dec27d8-7743-416b-8959-62f9e07a3d6e.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/middlewares/firewall
[link-travis]: https://travis-ci.org/middlewares/firewall
[link-scrutinizer]: https://scrutinizer-ci.com/g/middlewares/firewall
[link-downloads]: https://packagist.org/packages/middlewares/firewall
[link-sensiolabs]: https://insight.sensiolabs.com/projects/0dec27d8-7743-416b-8959-62f9e07a3d6e
