#bach

Classes for zepto\*!

They're really minimal. But inheritance is supported!

\* sort of.

## Installation

```
zeps install hellerve/bach
```

## Usage

There are two macros you can make use of, `class` and `inherits`.

A class could look like so:

```racket
(load "bach/bach")

(class Person
  (properties
    :name
    (:age :default 0))

  (functions
    (->string (lambda (self) (++ (Person:get-name self) ", age " (->string (Person:get-age self)))))))
```

This will generate the following functions:

```racket
(define joe (Person :name "Joe" :age 24))
(Person:get-name joe) ; => "Joe"
(Person:get-age joe) ; => 24
(Person:->string joe) ; => "Joe, age 24"
(Person:->string (Person:set-name joe "Tina")) ; => "Tina, age 24"
(Person:->string (Person:set-age joe 30)) ; => "Joe, age 30"
(Person? joe) ; => true
(Person:get-properties) ; => [:name, :age]
```

You can also inherit methods (but not properties!) from other classes:

```racket
(class Employee
  (properties
    :name
    (:age :default 0)
    (:job :default "Programming Grunt"))

  (functions
    (->string-with-job (lambda (self) (++ (Employee:->string self) " (" (Employee:get-job self) ")")))))

(inherits Employee Person)

(define my-grunt (Employee :name "Alyssa" :age 35))
(Employee:->string-with-job my-grunt) ; => "Alyssa, age 35 (Programming Grunt)"
```

And that's about it. Check out [the examples](https://github.com/hellerve/bach/tree/master/examples)!

## Advanced Information

### Inheritance resolution

The inheritance is resolved on a "first statement wins" basis, which means that
if `Duck` and `Bird` both implement a method called `fly` and `Ostrich` inherits
first from `Duck`, then from `Bird`, the `fly` method as implemented in `Duck` will
be used, whether it was inherited or not.

### Typing Information

Under the hood, all the classes are hashmaps. No fancy magic involved. They do not
carry their functions around, so they're not classes, but rather prototype-ish.

## FAQ

**Q: Is this a serious project?**

**A:** Not really, no. I have none of those.

**Q: Is this ready for production?**

**A:** Is zepto? If you answer that with yes, then sure, go ahead and use this library.
YMMV.

**Q: Why bach?**

**A:** Because (1) I like to listen to the music the family Bach composed and, (2) they
are the epitome of *class*ical music. Geddit? As if programming did not have enough
terrible puns yet.

<hr/>

Have fun!
