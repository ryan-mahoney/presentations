# Chapters 4 of PHP Advanced and Object-Oriented Programming
---
## About Me
Ryan Mahoney

Senior Software Engineer @ BetterLesson.com

15 years of software development, database adminstration and software architecture exerperience.

---

## Why is OOP Important?

- popular / universal
- proven strategy of modularization
- benefits of encapsulation
- mature tools for automated testing / analysis
- makes libraries and services more "composable"

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
class FormField {
}
```
---
## Creating an Object

An object is an instance of a class.

Consider that a house is an instance of a blueprint. Many houses can be made using the same blueprint. A blueprint is useful, but you can't live in one.  An object takes up space and can possibly store and do things.

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

$textInput = new FormInputField('text', 'Hello');
$submitInput = new FormInputField('submit', 'Submit Form');
```
---
## the $this Attribute
```php
<?php
class FormField {
}
---
## Creating Constructors
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
