## Documentation

In this documentation, `$1` represents the first tabbed input, all the way to `$n`. `$0` represents the last place you end up in after you're done tabbing. If there are two `$n`, e.g. `$1 f($1)`, then that means whatever you input will be put in those two places. If you see `${2:$1}` then that means that you can input part of $2 first, in this case $1, and then tab over to the whole expression, which in this case is `$2`.

To activate a snippet just type the trigger and then press tab.

Although the snippets show up as having four spaces in the reference, in the actual snippet it will substitute it with
your preference.

## Table of Contents

- [Loops](#loops)
- [Utilities](#utilities)
- [Conditional Statements](#conditional-statements)
- [Preprocessor](#preprocessor)
- [Classes](#classes)
- [Lambda](#lambda)
- [Functions](#functions)
- [Functors](#functors)
- [Others](#others)

### Loops

A collection of loop auto completions.

**Trigger**: do_

```cpp
do {
    $0
} while ($1);
```

**Trigger**: while

```cpp
while ($1) {
    $0
}
```

**Trigger**: for_

```cpp
for (unsigned $2 = 0; $2 < $1; ${3:++$2}) {
    $0
}
```

**Trigger**: forrange

```cpp
for (auto&& $1 : $2) {
    $0
}
```

### Utilities

Small simple stuff that can help with some typing.

**Trigger**: forw

```cpp
std::forward<$1>($2)
```

**Trigger**: declv

```cpp
std::declval<$1>()
```

**Trigger**: returns

```cpp
-> decltype($1) {
    return $1;
}
```

**Trigger**: name

```cpp
namespace $1 {
$0
} // $1
```

**Trigger**: usingt

```cpp
template<typename $1>
using $2 = $3;
```

**Trigger**: usings

```cpp
using $1 = $2;
```

**Trigger**: tem

```cpp
template<typename $1>
```

**Trigger**: try

```cpp
try {
    $1
}
catch ($2) {
    $0
}
```

**Trigger**: mitl

A snippet that generates an MIT License with input choices for your name and year.

### Conditional Statements

**Trigger**: if_

```cpp
if ($1) {
    $0
}
```

**Trigger**: ifelse

```cpp
if ($1) {
    $2
} else {
    $0
}
```

**Trigger**: ifelif

```cpp
if ($1) {
    $2
} else if($3) {
    $4
} else {
    $0
}
```

### Preprocessor

**Trigger**: ifnd

```cpp
#ifndef $1
#define $1

$0

#endif // $1
```

This snippet defaults to inserting the filename in all caps. e.g. `myheader.hpp` would generate `MYHEADER_HPP`.

**Trigger**: clanggreater

Checks for Clang version definition greater than or equal to version specified (version `$1.$2`).

```cpp
defined(__clang__) && ((__clang_major__ > $1) || (__clang_major__ == $1) && (__clang_minor__ >= $2))
```

**Trigger**: clangless

Checks for Clang version definition less than or equal to version specified (version `$1.$2`).

```cpp
defined(__clang__) && ((__clang_major__ < $1) || (__clang_major__ == $1) && (__clang_minor__ <= $2))
```

**Trigger**: gccgreater

Checks for GCC version definition greater than or equal to version specified (version `$1.$2.0`)

```cpp
defined(__GNUC__) && ((__GNUC__ > $1) || ((__GNUC__ == $1) && (__GNUC_MINOR__ >= $2)))
```

**Trigger**: gccless

Checks for GCC version definition less than or equal to version specified (version `$1.$2.0`)

```cpp
defined(__GNUC__) && ((__GNUC__ < $1) || ((__GNUC__ == $1) && (__GNUC_MINOR__ <= $2)))
```

**Trigger**: ifelifpre

```cpp
#if $1
$2
#elif $3
$4
#else
$0
#endif
```

**Trigger**: ifelsepre

```cpp
#if $1
$2
#else
$0
#endif
```

### Classes

**Trigger**: struct_

```cpp
struct $1
{
    $0
};
```

**Trigger**: structtemp

```cpp
template<typename $1>
struct $2
{
    $0
};
```

**Trigger**: class_

```cpp
class $1
{
private:
    $2
public:
    $1($3) $4
};
```

**Trigger**: classtemp

```cpp
template<typename $1>
class $2
{
private:
    $3
public:
    $2($4) $5
};
```

**Trigger**: excep

Creates an exception derived from an std::exception entity.

```cpp
class $1 : public $2
{
public:
    $1(const std::string& str): $2($3) {}
};
```

### Lambda

Snippets to insert C++11 lambdas of different flavours.

**Trigger**: lamref

```cpp
[&]($1) {
    $2
}
```

**Trigger**: lamval

```cpp
[=]($1) {
    $2
}
```

**Trigger**: lamret

```cpp
[$1]($2) -> $3 {
    $4
}
```

**Trigger**: lammin

```cpp
[$1] {
    $2
}
```

**Trigger**: lamfull

```cpp
[$1]($2) $3 $4 -> $5 {
    $6
}
```

### Functions

#### Regular functions


**Trigger**: funct

```cpp
$1 $2($3)
{
    $0
}
```

There is a `constexpr` variation:

**Trigger**: confunct

```cpp
constexpr $1 $2($3)
{
    return $0;
}
```

#### Templated Functions

**Trigger**: tempfunc

```cpp
template<typename $1>
$2 $3($4) noexcept
{
    $0
}
```

**Trigger**: tempfunca

This snippet doesn't use the same input for the return type and decltype specifier.
If you want that, use `tempcfunc` instead.

```cpp
template<typename $1>
auto $2($3) -> decltype($4)
{
    $0
}
```

**Trigger**: tempcfunc

```cpp
template<typename $1>
constexpr $2 $3($4)
{
    return $5;
}
```

**Trigger**: tempcfunca

```cpp
template<typename $1>
constexpr auto $2($3) noexcept -> decltype($4)
{
    return $4;
}
```

### Functors

**Trigger**: functor

```cpp
struct $1 {
    $2 operator()($3) const noexcept
    {
        $0
    }
};
```

There are also templated variations of functors:

**Trigger**: tempfunctor

```cpp
struct $1 {
    template<typename T>
    constexpr auto operator()(T&& t) const noexcept -> decltype($2)
    {
        return $2;
    }
};
```

**Trigger**: bintempfunctor

```cpp
struct $1 {
    template<typename T, typename U>
    constexpr auto operator()(T&& t, U&& u) const noexcept -> decltype($2)
    {
        return $2;
    }
};
```

###Others:

Add others

**Trigger**: cout

```cpp
std::cout << $1 << std::endl;
```

**Trigger**: constc

```cpp
const_cast<$1>($2)
```

**Trigger**: dynamicc

```cpp
dynamic_cast<$1>($2)
```

**Trigger**: staticc

```cpp
static_cast<$1>($2)
```

**Trigger**: reinterpretc

```cpp
reinterpret_cast<$1>($2)
```

**Trigger**: snprintf

```cpp
snprintf(${1:/*buf*/}, sizeof(${2:/*size*/}), "${3:/*fomart*/}", ${4:/*expression*/});
```

