Collections-C
=============

> A library of generic data structures including a list, array, hashtable, deque etc..

[![Build Status](https://travis-ci.org/srdja/Collections-C.svg?branch=master)](https://travis-ci.org/srdja/Collections-C)

## Examples
Check the [documentation page](https://srdja.github.io/Collections-C/) for mode detailed examples. (This is still in progress).
The source of the documentation can be found [here](https://github.com/srdja/cc-doc-slate).

HashTable:
```c

// Crate a new table
HashTable *table
if (hashtable_new(&table) != CC_OK) {
    // something went wrong
    ...
}

// Add key-value pair
if (hashtable_add(table, "some_key", "some_value") != CC_OK) {
    // something went wrong
    ...
}

// Retrieve a value associated with a key
char *value;
if (hashtable_get(table, "some_key", (void*) &value) == CC_OK)
    printf("%s", value);

// Remove a key
hashtable_remove(table, "foo", NULL);

hashtable_destroy(table);
```
Array (dynamic array):
```c
// Create a new array
Array *ar;
if (array_new(&ar) != CC_OK) {
    // something went wrong
    ...
}

// Add an element
enum cc_stat status = array_add(ar, "foo");
if (status == CC_OK) {
    ...
} else if (status == CC_ERR_ALLOC) {
    ...
} else {
    ...
}

// Retrieve a value
char *foo;
array_get_at(ar, 0, (void*) &foo);

// Remove a value
char *removed;
array_remove_at(ar, 0, (void*) &removed);

array_destroy(ar);
```
## Installation

####Dependencies
- gcc
- cmake ( >= 3.6 )

These packages can usually be installed through your distributions package manager.

Building on windows requires [MinGW](http://mingw.org) which provides all the tools needed to build the project.

#### Building the project

Building the library:
```
make build
```

Installing the library:
```
make install
```

The tests can be run by:
```
make test
```
#### Compiling and linking a simple program
- hello.c
```c
#include <stdio.h>
#include <collectc/array.h>

int main(int argc, char **argv) {
    Array *ar;
    array_new(&ar);
    array_add(ar, "Hello World!\n");

    char *str;
    array_get_at(ar, 0, (void*) &str);
    printf("%s", str);

    return 0;
}
```
We can now build and statically link the library to our program:
```
gcc hello.c -I/path/to/library/include/ -static -L/path/to/library/lib/ -lcollectc -o hello
```

## Contributors

All contributions are welcome.

See [CONTRIBUTING.md](https://github.com/srdja/Collections-C/blob/master/CONTRIBUTING.md) for details.
