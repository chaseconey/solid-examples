solid-examples
==============

Examples of SOLID design principles and patterns

## Decorator Pattern

In object-oriented programming, the decorator pattern (also known as Wrapper, an alternative naming shared with the Adapter pattern) is a design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class.

```php
<?php

interface CarService {
    public function getCost();
}

class BasicService implements CarService {

    public function getCost() {
        return 15;
    }
}

class OilChange implements CarServer {

    protected $carService;

    public function __construct(CarService $carService) {
        $this->carService = $carService;
    }

    public function getCost() {
        return 40 + $this->carService->getCost();
    }
}

echo (new OilChange(new BasicService()))->getCost();
```

In my words: you can essentially decorate a base object and inject that instance of the interface you are coding to into all subsequent objects and dynamically add functionality from each class. You just have to code to that interface for methods you with to decorate with.

## Single Responsibility

## Open-Closed Principle

In object-oriented programming, the open/closed principle states "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification"; that is, such an entity can allow its behaviour to be modified without altering its source code.

Just remember: Separate extensible behavior behind an interface and flip the dependencies.


```php
<?php

interface PaymentMethodInterface {
    public function acceptPayment($receipt);
}

class CreditCardPayment implements PaymentMethodInterface {
    public function acceptPayment($receipt) {
        // accept the payment via creditcard
    }
}

class Checkout {
    public function begin(Receipt $receipt, PaymentMethodInterface $payment) {
        $payment->acceptPayment($receipt);
    }
}
```

In my words: now we can easily extend the functionality of the Checkout class, by creating a new class that implements the PaymentMethodInterface. We don't need to have a switch/if in the begin function based on what type of payment it is.

## Liskov Substitution Principle (LSP)

Substitutability is a principle in object-oriented programming. It states that, in a computer program, if S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed, etc.)

In my words: All this principle states is that all inputs and outputs of a class should be the same when related. So if you have:

```php
class A {
    public function check() {}
}

class B extends A {
    public function check() {}
}
```

these classes should be able to be used interchangably in code.

This also ensures that your return types are consistent, so if you use class B instead of A, you should expect that check returns the exact same type of response.

