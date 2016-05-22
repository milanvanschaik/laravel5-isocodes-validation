# Laravel 5 IsoCodes Validation

[![Latest Version on Packagist](https://img.shields.io/packagist/v/pixelpeter/laravel5-isocodes-validation.svg?style=flat-square)](https://packagist.org/packages/pixelpeter/laravel5-isocodes-validation)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Travis Build](https://img.shields.io/travis/pixelpeter/laravel5-isocodes-validation/master.svg?style=flat-square)](https://travis-ci.org/pixelpeter/laravel5-isocodes-validation)
[![Scrutinizer Quality](https://img.shields.io/scrutinizer/g/pixelpeter/laravel5-isocodes-validation.svg?style=flat-square)](https://scrutinizer-ci.com/g/pixelpeter/laravel5-isocodes-validation)
[![Scrutinizer Build](https://img.shields.io/scrutinizer/build/g/pixelpeter/laravel5-isocodes-validation.svg?style=flat-square)](https://scrutinizer-ci.com/g/pixelpeter/laravel5-isocodes-validation)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/edfbddc6-ccbc-425c-9db8-726a5bc371e7.svg?style=flat-square)](https://insight.sensiolabs.com/projects/edfbddc6-ccbc-425c-9db8-726a5bc371e7)
[![Total Downloads](https://img.shields.io/packagist/dt/pixelpeter/laravel5-isocodes-validation.svg?style=flat-square)](https://packagist.org/packages/pixelpeter/laravel5-isocodes-validation)

A simple Laravel 5 wrapper for the [IsoCodes Validation library](https://github.com/ronanguilloux/IsoCodes) from ronanguilloux.

## Installation

### Step 1: Install Through Composer
``` bash
composer require pixelpeter/laravel5-isocodes-validation
```

### Step 2: Add the Service Provider
Add the service provider in `app/config/app.php`
```php
'provider' => [
    ...
    Pixelpeter\IsoCodesValidation\IsoCodesValidationServiceProvider::class,
    ...
];
```

## Usage

### Simple examples

```php
// Checking out your e-commerce shopping cart?
$payload = [
    'creditcard' => '12345679123456'
];
$rules = [
    'creditcard' => 'creditcard'
];

$validator = Validator::make($payload, $rules);
```

### Examples with parameter
Some rules need a reference to be validated against (e.g. `country` for `zipcode`).

Just pass the name of the field holding the reference to the rule.

```php
// Sending letters to the Labrador Islands ?
$payload = [
    'zipcode' => 'A0A 1A0',
    'country' => 'CA'
];
$rules = [
    'zipcode' => 'zipcode:country'
];

$validator = Validator::make($payload, $rules);

// Publishing books?
$payload = [
    'isbn' => '2-2110-4199-X',
    'isbntype' => 13
];
$rules = [
    'zipcode' => 'isbn:isbntype'
];

$validator = Validator::make($payload, $rules);
```

### Validation error messages
Error messages can contain the name and value of the field and the value of the reference
```php
$payload = [
    'phonenumber' => 'invalid',
    'country' => 'GB'
];
$rules = [
    'phonenumber' => 'phonenumber:country'
];

$validator = Validator::make($payload, $rules);

print $validator->errors()->first(); // The value "invalid" of phonenumber is not valid for "GB".
```

### More Examples
Refer to [IsoCodes Validation library](https://github.com/ronanguilloux/IsoCodes) for more examples and documentation.

## Testing
Run the tests with:
```bash
vendor/bin/phpunit
```

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.