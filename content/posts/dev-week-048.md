+++
tags = ['Developer Log', 'C', 'Python', 'AI']
title = 'Developer Week 048'
date = 2025-06-16T09:05:07+01:00
draft = false
+++

![Developer Week 048](https://pbrazeale.github.io/images/devweek048.jpg)

## Courses

### Boot.Dev Back-end Developer Career Path (~53.52%) (📈 +0.48%)

The course added a new Module 8, to build an AI Agent, replacing the Maze Solver. For tracking purposes I added the lesson count to total, which is why the week's increase in percentage complete was so small.

#### New 8. Build an AI Agent in Python (7/18)

##### new 8.1.3 Google Gemini

Ran into the following error when trying to use my API key:

> ValueError: Missing key inputs argument! To use the Google AI API, provide (`api_key`) arguments. To use the Google Cloud API, provide (`vertexai`, `project` & `location`) arguments.

[https://googleapis.github.io/python-genai/#create-a-client](https://googleapis.github.io/python-genai/#create-a-client)

LOL it was error cased by naming my `gemini_key.env` instead of just `.env`

- **That's a lesson I won't forget anytime soon!**

#### 11. Learn Memory Management (56/101)

##### 11.2.5

Assuming `char` is 1 byte, `int` is 4 bytes, and `double` is 8 bytes, the memory layout for `human_t` might look like this:

![Human Struct](https://storage.googleapis.com/qvault-webapp-dynamic-assets/course_assets/2hAib4n.png)

Wait! What is that `padding` doing here?

It turns out that CPUs don't like accessing data that isn't [aligned](https://en.wikipedia.org/wiki/Data_structure_alignment) (incredible oversimplification alert, since obviously CPUs don't have feelings (yet)), so C inserts padding to maintain alignment (e.g. every 4 bytes in this example).

##### 11.3.1

> Variables are human readable names that refer to some data in memory.

> Memory is a big array of bytes, and data is stored in the array.

A variable is a human readable name that refers to an address in memory, which is an index into the big array of bytes. Here's a diagram:

![memory diagram](https://storage.googleapis.com/qvault-webapp-dynamic-assets/course_assets/YZPw0el.png)

In C, you can print the address of a variable by using the address-of-operator: `&`. Here's an example:

```c
#include <stdio.h>

int main() {
  int age = 37;
  printf("The address of age is: %p\n", &age);
  return 0;
}

// The address of age is: 0xfff8
```

##### 11.3.6 Pointer Basics

```c
int *pointer_to_something; // declares `pointer_to_something` as a pointer to an int
```

```c
int meaning_of_life = 42;
int *pointer_to_mol = &meaning_of_life;
// pointer_to_mol now holds the address of meaning_of_life
```

```c
int meaning_of_life = 42;
int *pointer_to_mol = &meaning_of_life;
int value_at_pointer = *pointer_to_mol;
// value_at_pointer = 42
```

##### 11.3.9 Arrays as Pointers in C

```c
#include <stdio.h>

int main() {
  int numbers[5] = {1, 2, 3, 4, 5};

  // Accessing elements using array indexing
  printf("numbers[2] = %d\n", numbers[2]);  // Output: 3

  // Accessing elements using pointers
  printf("*(numbers + 2) = %d\n", *(numbers + 2));  // Output: 3

  // Pointer arithmetic
  int *ptr = numbers;
  printf("Pointer ptr points to numbers[0]: %d\n", *ptr);  // Output: 1
  ptr += 2;
  printf("Pointer ptr points to numbers[2]: %d\n", *ptr);  // Output: 3

  return 0;
}
```

##### 11.3.12 Pointer Size

In C, pointers are always the same size because they just represent memory addresses. The size of a pointer is determined by the architecture of the system (e.g., 32-bit or 64-bit)

> Boot.dev runs C in the browser using [WASM](https://webassembly.org/), which is typically a 32-bit system. If you run this code on a 64-bit system, the size of the pointers will be 8 bytes.

The size of an array depends on both the number of elements and the size of each element. An array is a contiguous block of memory where each element has a specific type, and therefore, a specific size.

##### 11.3.13 Arrays Decay to Pointers

```C
int arr[5];
int *ptr = arr;          // 'arr' decays to 'int*'
int value = *(arr + 2);  // 'arr' decays to 'int*'
```

##### When Arrays Don't Decay

- **`sizeof` Operator**: Returns the size of the entire array (e.g., sizeof(arr)), not just the size of a pointer.
- **`&` Operator** Taking the address of an array with `&arr` gives you a pointer to the whole array, not just the first element. The type of `&arr` is a pointer to the array type, e.g., `int (*)[5]` for an `int` array with 5 elements.
- **Initialization**: When an array is declared and initialized, it is fully allocated in memory and does not decay to a pointer.

##### 11.3.14 C Strings

- Unlike other programming languages, C strings do *not* store their length.
- The length of a C string is determined by the position of the null terminator (`'\0'`).
- Functions like [`strlen`](https://en.cppreference.com/w/c/string/byte/strlen) calculate the length of a string by iterating through the characters until the null terminator is encountered.
- This lack of length storage requires careful management to avoid issues such as buffer overflows and off-by-one errors during string operations.

##### 11.3.16 Forward Declaration

```c
typedef struct SnekObject snekobject_t;
```

This line is a **forward declaration**. Think of it like telling the compiler, "Hey, there's a structure named `SnekObject` that I'll define later, and I want to use the shorter name `snekobject_t` for it." This is crucial because the `SnekObject` structure needs to refer to itself (or rather, pointers to itself) inside its own definition. Without this forward declaration, the compiler wouldn't know what `snekobject_t` is when it encounters it inside the `struct SnekObject` definition.

```c
typedef struct SnekObject {
  char *name;
  snekobject_t *child;
} snekobject_t;
```

This is the actual definition of the `SnekObject` structure.

- `typedef struct SnekObject` means we are defining a structure named `SnekObject` and immediately creating a type alias for it.
- `{ ... }` encloses the members of the structure.
- `char *name;` declares a member named `name` which is a pointer to a character (commonly used for strings).
- `snekobject_t *child;` declares a member named `child` which is a pointer to another `snekobject_t`. This is where the forward declaration comes into play – we can declare a pointer to `snekobject_t` even though the full definition of `snekobject_t` is still in progress.
- `} snekobject_t;` finishes the structure definition and the `typedef`, making `snekobject_t` a synonym for `struct SnekObject`.

```c
snekobject_t new_node(char *name);
```

This line is a **function prototype**. It tells the compiler that there's a function named `new_node` that will be defined elsewhere.

- `snekobject_t` is the return type of the function. It means this function will create and return a `snekobject_t` structure.
- `new_node` is the name of the function.
- `(char *name)` specifies that the function takes one argument, which

##### 11.4.3 Switch Case

`return a hard-coded string (char *)` mean I can `return "desired string"` directly. There is no need to hard card a `char *variable` for C.
