# Introduction

- [What is Stillat?](#what)
- [What does Stillat do?](#what-it-includes)

<a name="what"></a>
## What is Stillat?

Stillat is a collection of highly-specialized software libraries, APIs and wrapper classes. It is **not** an application framework. We use Laravel 4.2+ for that, and as such, our libraries will be dependent on Laravel 4.2+.

From Laravel:

> Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable, creative experience to be truly fulfilling. Laravel attempts to take the pain out of development by easing common tasks used in the majority of web projects, such as authentication, routing, sessions, and caching.

Stillat strongly supports the core Laravel philosophies: development should be fun, and it should not be a complete pain. Laravel gets us most of the way there, but there are things that Laravel cannot do, and things that Laravel *should not do* in the core. Stillat aims to fill some of those gaps.

<a name="what-it-includes"></a>
## What does Stillat do?

As mentioned, Stillat is not an application framework. It exists as a series of add-on components for Laravel, or packages. There are many different packages that make up what we are 'Stillat'. Each package exists as its own repository and does specific things.

### Stillat/Common

This package contains various things that are *common* to a lot of applications out there. It includes a unified API for sorting algorithms, improvements to arrays and Laravel's `Collection` class as well as set of pre-defined exceptions, such as `ArgumentOutOfRangeException` and `DivideByZeroException`.