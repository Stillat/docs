# Exceptions & Expectations

The Common library provides a generalized exception hierarchy; it is used internally by the library itself. Feel free to use the exceptions in your own application if you find them useful. The Common library also contains an "expectations" framework to make throwing common exceptions even easier.

## Exceptions

The Common exceptions are contained within the `Stillat\Common\Exceptions` namespace. The most common exceptions are (within the exception namespace):

~~~
Exception
    Argument\ArgumentException
        ArgumentNullException
        InvalidArgumentException
        MissingArgumentException
    Arithmetic\ArithmeticException
        DivideByZeroException
        NotFiniteNumberException
~~~

You catch Common exceptions just like regular PHP exceptions:

~~~
<?php

use Stillat\Common\Math\ExpressionEngines\NativeExpressionEngine;
use Stillat\Common\Math\Calculator;
use Stillat\Common\Exceptions\Arithmetic\DivideByZeroException;

// Create a new Calculator instance.
$calc = new Calculator(new NativeExpressionEngine);

try {
	$calc->divide(10, 0);
} catch (DivideByZeroException $e) {
	// Thrown when you attempt to divide by 0.
}
~~~

## Expectations

The Common library contains an "expectations" utility to make it easier to throw common exceptions under common scenarios. The expectations utility is implemented as a trait, and is therefor an "opt-in" feature.

To use the expectations in your own classes, simply "use" the `Expectations` trait:

~~~
<?php

use Stillat\Common\Traits\Expectations;

use Stillat\Common\Traits\Expectations;

class MyClass
{
    use Expectations;

    public function divide($numberOne, $numberTwo)
    {
        // Don't allow $numberTwo to be zero.
        $this->expectNumberNotZeroForDivision($numberTwo);

        return $numberOne / $numberTwo;
    }

}
~~~

Each expectation also allows you to provide an optional message that will be used in the thrown exceptions:

~~~
$this->expectNumberNotZeroForDivision($numberTwo, 'Divisor cannot be zero');
~~~

### Available Expectations

The following expectations are available for your own use. The thrown exceptions will also be listed for your reference.

#### `expectValuesWhenNotNull($checkValue, array $values, $message = '')`

This expectation checks to see if the `$checkValue` is not null. If the `$checkValue` is not null, then it makes sure that all the values in the `$values` array are also not null. If any values are null, an instance of `\Stillat\Common\Exceptions\Argument\MissingArgumentException` will be thrown.

#### `expectValidNumber($number, $message = '')`

This expectation ensures that the `$number` provided is a valid number. Specifically, it makes sure that the `$number` is an actual number and not infinity. If this expectation fails, an instance of `\Stillat\Common\Exceptions\Arithmetic\NotFiniteNumberException` will be thrown.

#### `expectNumberNotZeroForDivision($number, $message = '')`

This expectation makes sure that the provided `$number` is not `0`. If will also internally make a call to `expectValidNumber`. If this expectation fails, it may throw a new instance of either of the following:


* `\Stillat\Common\Exceptions\Arithmetic\DivideByZeroException`
* `\Stillat\Common\Exceptions\Arithmetic\NotFiniteNumberException`