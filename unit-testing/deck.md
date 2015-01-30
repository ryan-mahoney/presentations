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
4. A folder for test suites (a folder of tests)
5. A test suite (a class)
6. Unit Test (methods)

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