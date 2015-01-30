# Unit Testing

Unit testing is a software development process in which the smallest testable parts of an application, called units, are individually and independently scrutinized for proper operation. Unit testing is often automated but it can also be done manually.

---

## Big Picture

~~Write Once, Run Anywhere~~

Learn Once, Write Anywhere

---

## What Does it Solve?
1. See impact of localized code changes
2. See impace of dependencies Change over time
3. House... everybody lies

![alt text](http://img0077.popscreencdn.com/154282320_amazoncom-house---everybody-lies-vinyl-die-cut-decal-.jpg "Everybody Lies")

---

## Additional Benefits

1. More reliable code base
2. Catching issues earlier
3. Promotes best practices in software dev

---

## Which Best Practices?

Is your codes testable?

1. Write smaller classes (single responsibility principle)
2. write more clear method names
3. Fewer pathways within individual methods (easier to "cover")
4. Pay attendtion to how easy it is to bootstrap the code, mock data

## Anatomy of a Unit Test

1. A test runner (PHPUnit)
2. Some configuration (XML..)
3. A bootstrap (where is my framework?)
4. A test suite (a class)
5. Unit Test (methods)

---

### Config

```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="./tests/bootstrap.php" colors="true">
    <testsuites>
        <testsuite name="BetterLesson Test Suite">
            <directory>./tests/</directory>
        </testsuite>
    </testsuites>
</phpunit>
```

### Bootstrap

```php
<?php
date_default_timezone_set('UTC');
require_once __DIR__.'/../vendor/autoload.php';
```

### Test Suite

```php
<?php
use PHPUnit_Framework_TestCase;
use Guzzle\Http\Client;

class RegistrationTest extends PHPUnit_Framework_TestCase {
    public function testCreateAccountSuccess () {
        $request = self::$client->post(self::$host . '/register?from', array(), array());
        $request->setHeader('Accept', 'application/json');
        $request->setHeader('X-Requested-With', 'XMLHttpRequest');

        $email = 'ryan.mahoney+' . uniqid() . '@betterlesson.com';

        $request->addPostFields(array(
            'User' => array(
                'Grade'               => array('id' => 12),
                'Subject'             => array('id' => 1),
                'email'               => $email,
                'first_name'          => 'Ryan',
                'is_landing_template' => 'true',
                'last_name'           => 'Mahoney',
                'password'            => 'password',
                'registration_action' => '',
                'registration_url'    => ''
            )
        ));

        $response = $request->send();
        $data = json_decode($response->getBody(), true);
        $this->assertTrue($data['auth_user_email'] == $email);
    }
}
```

### Running Tests

![alt text](http://cdn-ak.f.st-hatena.com/images/fotolife/K/Kenji_s/20120117/20120117095833.png "Running Tests")

### Code Coverage

![alt text](https://camo.githubusercontent.com/9408c3510fd2ced7720fb6beaca86731472681c0/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313237373532362f323233383832372f65323337346132362d396330332d313165332d383066342d3135656234383765643361652e706e67 "Code Coverage")

### TDD

Pactical TDD