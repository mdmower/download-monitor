# Download Monitor Unit Tests

## Initial Setup

1) Install [PHPUnit](http://phpunit.de/) by following their [installation guide](https://phpunit.de/getting-started.html). If you've installed it correctly, this should display the version:

    $ phpunit --version

2) Install WordPress and the WP Unit Test lib using the `install.sh` script. Change to the plugin root directory and type:

    $ tests/bin/install.sh <db-name> <db-user> <db-password> [db-host]

Sample usage:

    $ bash tests/bin/install.sh dlm_tests root root

**Important**: The `<db-name>` database will be created if it doesn't exist and all data will be removed during testing.

## Running Tests

Simply change to the plugin root directory and type:

    $ phpunit

The tests will execute and you'll be presented with a summary. Code coverage documentation is automatically generated as HTML in the `tmp/coverage` directory.

You can run specific tests by providing the path and filename to the test class:

    $ phpunit tests/unit-tests/api/webhooks

A text code coverage summary can be displayed using the `--coverage-text` option:

    $ phpunit --coverage-text

## Writing Tests

* Each test file should roughly correspond to an associated source file
* Each test method should cover a single method or function with one or more assertions
* A single method or function can have multiple associated test methods if it's a large or complex method
* Use the test coverage HTML report (under `tmp/coverage/index.html`) to examine which lines your tests are covering and aim for 100% coverage
* For code that cannot be tested (e.g. they require a certain PHP version), you can exclude them from coverage using a comment: `// @codeCoverageIgnoreStart` and `// @codeCoverageIgnoreEnd`.
* In addition to covering each line of a method/function, make sure to test common input and edge cases.
* Prefer `assertsEquals()` where possible as it tests both type & equality
* Remember that only methods prefixed with `test` will be run so use helper methods liberally to keep test methods small and reduce code duplication.
* Filters persist between test cases so be sure to remove them in your test method or in the `tearDown()` method.

## Automated Tests

Tests are automatically run with [Travis-CI](https://travis-ci.org) for each commit and pull request.

## Code Coverage

Code coverage is available on [Coveralls](https://coveralls.io/) which receives updated data after each Travis build.

## Credits
Tests install script inspired by WooCommerce script.