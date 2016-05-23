# Wai

Web application installer

## Usage

In your entry file (eg. index.php) add statements like below to get this work.

```php
<?php

// index.php

// informative start flag
Wai::start(__FILE__, 6);

// configuration
$config = [
    // current version
    'version'      => '0.1.0',
    // used for saving installed version and schema
    'workingDir'   => 'tmp/',
    // schema directory that contains every schema that need to be installed
    // filename should be prefixed by ordered number
    'schemaDir'    => 'app/schema/',
    // argument for constructing PDO class
    'database'     => [
        // dsn, string, without database name
        'dsn'      => 'mysql:host=127.0.0.1',
        // username, string
        'username' => 'root',
        // password, string
        'password' => null,
        // options, array
        'options'  => [],
        // database name
        'dbname'   => 'test_wai',
        // drop db first
        'dropdb'   => false,
    ],
];
Wai::setup($config);

// check if current version is same as installed version
if (Wai::isNotInstalled()) {

	// not installed, install it
	// you can pass array of callback that will be execute
	// after database procedure has been done
    $dir = __DIR__;
    $callbacks = [
        function() use ($dir) {
            chmod($dir.'/tmp', 0777);
        },
        function() {
            // other statements to do
        },
    ];
    Wai::handleInstallation();
}

// informative finish flag
Wai::finish(__FILE__, 60);

// catch result
// $result = Wai::result();

// or write result and exit
Wai::hold();
```
