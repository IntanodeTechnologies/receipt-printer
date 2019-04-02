# Laravel Receipt Printer

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Total Downloads][ico-downloads]][link-downloads]
[![Build Status][ico-travis]][link-travis]
[![StyleCI][ico-styleci]][link-styleci]

Simple Laravel package to integrate ESC/POS Print Driver for PHP.

## Installation

Via Composer

``` bash
$ composer require charlieuki/receiptprinter
```

## Usage

```
printReceipt()
```

```
printRequest()
```

## Example (Print Receipt)

```
// Set params
$mid = '123123456';
$store_name = 'YOURMART';
$store_address = 'Mart Address';
$store_phone = '1234567890';
$store_email = 'yourmart@email.com';
$store_website = 'yourmart.com';
$tax_percentage = 10;
$transaction_id = 'TX123ABC456';

// Set items
$items = [
    [
        'name' => 'French Fries (tera)',
        'qty' => 2,
        'price' => 65000,
    ],
    [
        'name' => 'Roasted Milk Tea (large)',
        'qty' => 1,
        'price' => 24000,
    ],
    [
        'name' => 'Honey Lime (large)',
        'qty' => 3,
        'price' => 10000,
    ],
    [
        'name' => 'Jasmine Tea (grande)',
        'qty' => 3,
        'price' => 8000,
    ],
];

// Init printer
$printer = new ReceiptPrinter;
$printer->init(
    config('receiptprinter.connector_type'),
    config('receiptprinter.connector_descriptor')
);

// Set store info
$printer->setStore($mid, $store_name, $store_address, $store_phone, $store_email, $store_website);

// Add items
foreach ($items as $item) {
    $printer->addItem(
        $item['name'],
        $item['qty'],
        $item['price']
    );
}
// Set tax
$printer->setTax($tax_percentage);

// Calculate total
$printer->calculateSubTotal();
$printer->calculateGrandTotal();

// Set transaction ID
$printer->setTransactionID($transaction_id);

// Set qr code
$printer->setQRcode([
    'tid' => $transaction_id,
]);

// Print receipt
$printer->printReceipt();
```

## Example (Print Request)

```
// Set params
$mid = '123123456';
$store_name = 'YOURMART';
$store_address = 'Mart Address';
$store_phone = '1234567890';
$store_email = 'yourmart@email.com';
$store_website = 'yourmart.com';
$tax_percentage = 10;
$transaction_id = 'TX123ABC456';

// Init printer
$printer = new ReceiptPrinter;
$printer->init(
    config('receiptprinter.connector_type'),
    config('receiptprinter.connector_descriptor')
);

// Set store info
$printer->setStore($mid, $store_name, $store_address, $store_phone, $store_email, $store_website);

// Set request amount
$printer->setRequestAmount($request_amount);

// Set transaction ID
$printer->setTransactionID($transaction_id);

// Set qr code
$printer->setQRcode([
    'tid' => $transaction_id,
    'amount' => $request_amount,
]);

// Print payment request
$printer->printRequest();
```

## Change log

Please see the [changelog](changelog.md) for more information on what has changed recently.

## Contributing

Please see [contributing.md](contributing.md) for details and a todolist.

## Security

If you discover any security related issues, please email charlie@usahakreatif.co.id instead of using the issue tracker.

## Credits

- *Mike42* for the awesome [PHP ESC/POS Print Driver][https://github.com/mike42/escpos-php]

## License

MIT. Please see the [license file](license.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/charlieuki/receiptprinter.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/charlieuki/receiptprinter.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/charlieuki/receiptprinter/master.svg?style=flat-square
[ico-styleci]: https://styleci.io/repos/12345678/shield

[link-packagist]: https://packagist.org/packages/charlieuki/receiptprinter
[link-downloads]: https://packagist.org/packages/charlieuki/receiptprinter
[link-travis]: https://travis-ci.org/charlieuki/receiptprinter
[link-styleci]: https://styleci.io/repos/12345678
[link-author]: https://github.com/charlieuki
[link-contributors]: ../../contributors