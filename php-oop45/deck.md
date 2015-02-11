# Chapters 4 of PHP Advanced and Object-Oriented Programming
---
## About Me
Ryan Mahoney

Senior Software Engineer @ BetterLesson.com

15 years of software development, database adminstration and software architecture exerperience.

---

## Why is OOP Important?

- popular / universal
- good for building systems
- proven strategy of modularization
- benefits of encapsulation
- mature tools for automated testing / analysis
- makes libraries and services more "composable"
- it documents its own architecture (sort of)
- the basis for most software architecture design patterns

---
## OOP Theory

A class is the blueprint from which individual objects are created.

- classes
 - fields
 - methods 
- objects
---

## Defining A Class

```php
<?php
class FormInputField {
}
```
---

Classes only consist of two types of things...

```php
<?php
class NicePerson {
    private $greeting = 'Hi';
    
    public function sayHi () {
        echo $this->greeting;
    }
}

$ryan = new NicePerson();
$ryan->sayHi();
//Hi!
```

---

## Creating an Object

An object is an instance of a class.

(Tell the interview story... from BSD...)

---

## Object Oriented Thinking

Consider that a house is an instance of a blueprint. Many houses can be made using the same blueprint. A blueprint is useful, but you can't live in one.  An object takes up space and can possibly store and do things.

---

## Fields

AKA: class variables, attributes, data members

Think of fields as storage slots.

```php
<?php
class FormInputField {
    private $tag;
    private $value;
}
```
---

## Two Hard Things in Programming...

```
There are only two hard things in Computer Science: cache invalidation and naming things.
```
-- Phil Karlton

Writing new software is easy and fun... maintaining old software is hard.  

How you name things will make your or someone else's job easier or harder over time.

---

## Methods

Similar to functions. This is where the logic of your class lives.

For the record, the difference between a function and a method is that a function can only operate on data that is passed in. A method can operate on data that is passed in and that is stored in the fields of the class or object it belongs to.

---

```php
<?php
class FormInputField {
    private $tag;
    private $value;
    
    public function __construct ($type, $value=NULL) {
        $this->type = $type;
        $this->value = $value;
    }
    
    public function render () {
        return '<input type="' . $this->type . '" ' . $this->renderValue() . '>';
    }
    
    private function renderValue() {
        if (empty($this->value)) {
            return '';
        }
        return ' value="' . $this->value . '" '; 
    }
}
```

---

## Instantiating an Object

We use the "new" keyword.

This code:

```php
<?php
require 'FormInputField.php';

$textInput = new FormInputField('text', 'Hello');
$submitInput = new FormInputField('submit', 'Submit Form');

echo $textInput->render(), "\n", $submitInput->render();
```

Produces this output:

```html
<input type="text" value="Hello">
<input type="submit" value="Submit Form">
```

---
## the $this Attribute

"$this" is a special predefined variable that is a reference to the object.

It is a shorthand way of expressing the idea "this particular instance".

Use it to internally refer to fields and methods of an object.  

In our example, we have two instances. "$this->type" is going to refer to "text" in the first case, and "submit" in the second use case.

```php
<?php
class FormInputField {
    public function render () {
        return '<input type="' . $this->type . '" ' . $this->renderValue() . '>';
    }
}
```
---
## Creating Constructors

- magic method in PHP
- called when the object is constructed
- usually used for initialization
- extremely important for "dependency injection"

```php
<?php
class FormInputField {
    public function __construct ($type, $value=NULL) {
        $this->type = $type;
        $this->value = $value;
    }
}
```
---
# Chapters 5 of PHP Advanced and Object-Oriented Programming
---
## Advanced Theories

- inheritance
- overriding methods
- access control (visibility)
---
## Inheriting Classes
---
## Inheriting Constructors and Destructors
---
## Overriding Methods
---
## Access Control (visibility)

- public, private, protected
- and API (Application Programmer Interface) is the public methods
- it's about clarifying the intent in terms of who can see / use a method

---

## Access Control Intent

**Public**
Can be called from outside the class

**Private**
Can only be called internally within the object by its own methods, can not be called by child-classes

**Protected**
Can only be called internally within the object by its own methods, but can be called by child-classes

---
## Using the Scope Resolution Operator
---
## Creating Static Members
---
# Fin
