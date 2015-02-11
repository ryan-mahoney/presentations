# Chapters 4 of PHP Advanced and Object-Oriented Programming
---
## About Me
Ryan Mahoney

Senior Software Engineer @ BetterLesson.com

(BetterLesson is hiring!)

15 years of software development, database adminstration and software architecture exerperience.

---

## Why is OOP Important?

- popular / universal
- good for building systems
- proven strategy of modularization
- reap the benefits of encapsulation
- mature tooling for automated testing / analysis
- makes libraries and services more "composable"
  - php composer 
- it documents its own architecture (sort of)
  - looking at class names, etc give impression of architecture  
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
class SomeThing {}
```
---

Classes only consist of two types of things...

```php
<?php
class NicePerson {
    private $greeting = 'Hi';
    
    public function sayGreeting () {
        echo $this->greeting;
    }
}

$ryan = new NicePerson();
$ryan->sayGreeting();

//Hi!
```

---

## Creating an Object

An object is an instance of a class.

(Tell the interview story from BSD...)

---

## Object Oriented Thinking

Consider that a house is an instance of a blueprint.

Many houses can be made using the same one blueprint. 

A blueprint is useful description of a house, but you can't live in one.

An object takes up space (memory) and can possibly store (data) and do things (be executed).

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

---

## Fields: Setting Values

- default
- via constuctor
- "reaching into" public fields
- from a method

```php
<?php
class FormInputField {
    public $type = 'input';
    private $value;
    
    public function __construct ($type) {
        $this->type = $type;
    }
    
    public function setValue ($value) {
        $this->value = $value;
    }
}

$input = new FormInputField('submit');
$input->type = 'text';
```
---

## Two Hard Things in Programming...

```
There are only two hard things in Computer Science: cache invalidation and naming things.
```
-- Phil Karlton

Writing new software is easy and fun... maintaining existing software is hard.  

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

- define a base of functionality that can be used by "child" classes
- create new "composite" classes
- controvercial, re: "coupling", see James Gosling
- the purpose of patterns is to avoid coupling and make systems resistant to defects

The "extends" keyrowd

```php
<?php
class Lion {}
class Tiger extends Lion {}
class Liger extends Tiger {}
```

----

## Extends in Detail

```php
<?php
class Lion {
    protected $hasMane = true;
    
    public function speak () {
        return 'Rooooaaaar!!!';
    }
}

class Tiger extends Lion {
    protected $hasStripes = true;
}

class Liger extends Tiger {
    protected $isMythical = true;
    
    public function speak () {
        return 'Vote for Pedro';
    }
    
    public function aboutMe () {
        var_dump($this->hasMane);
        var_dump($this->hasStripes);
        var_dump($this->isMythical);
    }
}

$gus = new Liger();
$gus->aboutMe();
echo $gus->speak();
```

bool(true)

bool(true)

bool(true)

Vote for Pedro

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
