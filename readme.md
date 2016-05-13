## PHPT tests runner - Runner for PHPT tests (with few differences comparing to original PHPT format)

```
PHPT Tests runner

Usage:
  phpt-tests-runner [-h] [files] [directories]

Arguments:
  h Print this help message

Examples:
  Execute tests from tests directory:
    phpt-tests-runner tests
  Execute tests single test:
    phpt-tests-runner tests/sample.phpt
  Execute tests from tests directory, but skip slow tests using environment variable:
    SKIP_SLOW_TESTS=1 phpt-tests-runner tests

PHPT Format:
  This runner uses modification of PHPT format used by PHP itself, so that it can run many original PHPT tests without any changes.

  PHPT test if text file with *.phpt extension.
  Each file contains sections followed by section contents, everything before first section is ignored, you can use it for storing test description.

  Required sections are --FILE-- and one of [--EXPECT--, --EXPECTF--, --EXPECTREGEX--].

PHPT sections supported:
  --FILE--        The test source code
  --EXPECT--      The expected output from the test script (will be executed as PHP script, so it might be code as well as plain text)
  --EXPECTF--     Similar to --EXPECT--, but it uses substitution tags for strings, spaces, digits, which may vary between test runs
    The following is a list of all tags and what they are used to represent:
      %s One or more of anything (character or white space) except the end of line character
      %S Zero or more of anything (character or white space) except the end of line character
      %a One or more of anything (character or white space) including the end of line character
      %A Zero or more of anything (character or white space) including the end of line character
      %w Zero or more white space characters
      %i A signed integer value, for example +3142, -3142
      %d An unsigned integer value, for example 123456
      %x One or more hexadecimal character. That is, characters in the range 0-9, a-f, A-F
      %f A floating point number, for example: 3.142, -3.142, 3.142E-10, 3.142e+10
      %c A single character of any sort (.)
  --EXPECTREGEX-- Similar to --EXPECT--, but is treated as regular expression
  --SKIPIF--      If output of execution starts with `skip` then test will be skipped
  --INI--         Specific php.ini setting for the test, one per line
  --ARGS--        A single line defining the arguments passed to php
  --CLEAN--       Code that is executed after a test completes

PHPT tests examples:
  Examples can be found at <https://qa.php.net/phpt_details.php> (taking into account differences here)

Main differences from original PHPT tests files:
  1. --TEST-- is not required and not even used (files names are used instead)
  2. Only sub-set of sections supported and only sub-set of --EXPECTF-- tags
  3. --EXPECT*-- sections are interpreted as code and its output is used as expected result
```

## Requirements:

* PHP 5.6+ or HHVM

## How to use?

Simply add dependency on `nazar-pc/phpt-tests-runner` to your project's `composer.json`:

```json
{
    "require-dev": {
        "nazar-pc/phpt-tests-runner": "1.*"
    }
}
```

Then execute tests as following:
```
vendor/bin/phpt-tests-tunner tests
```
Or if you need environment variables to propagate into tests:
```
php -d variables_order=EGPCS vendor/bin/phpt-tests-tunner tests
```

Alternatively you can install it globally using Composer like this:
```bash
sudo COMPOSER_BIN_DIR=/usr/local/bin composer global require nazar-pc/phpt-tests-tunner
```
`COMPOSER_BIN_DIR=/usr/local/bin` will instruct Composer to install binary to `/usr/local/bin` so that you'll be able to call just `phpt-tests-tunner` after installation.
Alternatively you can skip it and add `~/.composer/vendor/bin/` to your PATH.

## Contribution
Feel free to create issues and send pull requests, they are highly appreciated!

## License
MIT License, see license.txt
