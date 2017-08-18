# static-print

### Changelog

* 4/7/17 - Fixed issue which prevented the compiler from compiling during second stage (bootstrapping).

## What is it
This is a patch to the GCC 7.1 source which *adds a "static_print" statement to C++*.

The static_print statement can be used wherever static_assert can be used, and its effect is to **print a formatted message at compile time**.

static_print can receive any no. of arguments, each argument being either *a string literal* (which is printed out), or *any "template-argument" expression* (anything that could be a template argument - types, constant expressions, template names, etc..), which is resolved at compile time and pretty-printed.

Unlike static_assert, static_print also *behaves correctly with if constexpr*! (nothing will be printed if the condition does not apply).

### Example
```
template<typename T, int s>
struct test
{
    static_print("The template ", ::test, " has been instantiated as ", test, ". By the way, s + 1 is ", s + 1);
};

int main() {
    test<int, 3> y;
    return 0;
}
```

Compiling the above program prints out (at compile time):
`The template test has been instantiated as  test<int, 3>. By the way, s + 1 is 4`

## How to use
Download the GCC 7.1 sources, apply the patch and build GCC for your platform of choice
