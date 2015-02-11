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
- classes
 - fields
 - methods 
- objects
---
## Defining A Class

A class is the blueprint from which individual objects are created.

```php
<?php
class FormInputField {
}
```
---

## Creating an Object

An object is an instance of a class.

---

## Object Oriented Thinking

Consider that a house is an instance of a blueprint. Many houses can be made using the same blueprint. A blueprint is useful, but you can't live in one.  An object takes up space and can possibly store and do things.

---

## Fields

AKA: class variables, attributes, data members

Storage slots.

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

Writing new software is easy and fun... maintaining old software is hard.  How you name things will make your or someone else's job easier or harder over time.

---

## Methods

Similar to functions. This is where the logic of your class lives.

For the record, the different between a function and a method is that a function can only operate on data that is passed in. A method can operate on data that is passed in and that is stored in the fields of the class or object it belongs to.

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

```php
$textInput = new FormInputField('text', 'Hello');
$submitInput = new FormInputField('submit', 'Submit Form');

echo $textInput->render(), "\n", $submitInput->render();
```

```html
<input type="text" value="Hello">
<input type="submit" value="Submit Form">
```

---
## the $this Attribute

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
## Designing Classes with UML
---
# Chapters 5 of PHP Advanced and Object-Oriented Programming
---
## Advanced Theories
---
## Inheriting Classes
---
## Inheriting Constructors and Destructors
---
## Overriding Methods
---
## Access Control
---
## Using the Scope Resolution Operator
---
## Creating Static Members
---
# Fin
