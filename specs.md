# CHM

CHM is a programming language based on procedural paradigm and Hindley-Milner type system.

## Types

- Type constants begin with a capital letter (`Int`, `Char`, `Bool`, etc.).
- Type variables begin with a lower letter.
- Anonymous types are named `_`

**structs** and **unions** are types, equivalent structs and equivalent unions are considered distinct.

### Type categories

**NO REFERENCES** that would have implicit pointer semantics.

- primitive types
  - numeric types: `Int`, `Long`, `Bool`, etc.
  - structs and unions
- pointers: `type*`
- functions: `(par_type1, par_type2, ...) -> return_type`

### Numeric types

Those are the types that can appear as arguments of basic arithmetic [operators](#operators).

- `Bool`
- `I8`, `I16`, `I32`, `I64` (, etc.)
  - `Char` is an alias for `I8`
  - `Short` is an alias for `I16`
  - `Int` is an alias for `I32`
  - `Long` is an alias for `I64`
- `U0`, `U8`, `U16`, `U32`, `U64` (, etc.)
  - `Void` is an alias for `U0`
  - `Byte` is an alias for `U8`
  - `UShort` is an alias for `U16`
  - `UInt` is an alias for `U32`
  - `ULong` is an alias for `U64`
- `F32`, `F64`
  - `Float` is an alias for `F32`
  - `Double` is an alias for `F64`

All numeric values except `Bool` and `Void` are in `Num` [class](#classes).

### Pointers

Each Pointer type is uniquely derived from a certain base type. A variable of the pointer type can be derefernced to get the value it points to which is of the base type.

### Functions

#### Declaration and definition

```
1:  (parameter_list) -> type name;
2:  (parameter_list) -> type name {...}
```

1. basic function declaration
2. basic function definition

#### Example

```
1:  () -> a* new { return (a*)malloc(sizeof(a)); }
```

1. This defines a [generic](#generics) function that returns a pointer to allocated data of `a` type.

#### `pass` value and `return` statement

- `pass = value` sets the return value of the function to `value`.
- `return value` sets the return value of the function to `value` and returns the control to the caller.
- `return` returns the control to the caller without setting the return value.

#### Member accessors

Member accessors return reference to struct/union members (of the same name), they are syntactically a special function that takes one argument from left separated by a dot symbol:

```
object.member // returns the reference to the member in the object
```

##### `this` specifier

One function argument (has to be of a pointer type) can be given `this` specifier to allow use of member accessors without the arrow symbol:

```
struct Dog {
  String name;
}

(this Dog *rex) -> String get_name {
  return name; // same as rex->name
}
```

It also also allows for using the functions via the OO `object.function` syntax the same way accessors are given their arguments. The function, while normally taking `n` arguments, now takes the `this` argument which precedes the dot symbol and the other `n-1` arguments in the parentheses (the same way OO calls usually works).

## Variables

Variables are declared by specifying the type (can be anonymous `_`), preceded by an optional `const` specifier and followed by the variable's name.

### `const`

The `const` specifier signifies the variable is constant, this also applies to all expresions the variable appears in.


## Statements

### Assignment statements

### Control statements

```
1:  if    [name] (condition) statement
2:  else                     statement
3:  while [name] (condition) statement
4:  else                     statement
5:  do    [name]             statement [while(condition)]
```

1. The usual if statement (can be named)
2. The else branch
3. The usual while statement (can be named)
4. The else branch of the while statement (happens if the condition fails: not if the loop is broken)
5. The usual do (while) statement

#### `break` and `break name` statements

There is no `continue`, only `break`s.

- `break`: breaks the most nested control flow block (`if`, `while`, `do`).
- `break name`: breaks the control flow block named `name`.

## Classes

### Built-in classes

`Num` is an builtin type class which cannot have any user-defined instances. All [arithmetic operators](arithmetic operators) are it's methods.

### `Default` class

TODO

### User-defined classes

### Methods

#### Access modifiers

```
1:  public
2:  protected
3:  private
```

1. public methods are accessible anywhere (*default*).
2. protected methods are accessible from any method of any subclass of the class the method is defined in.
3. private methods are accessible only from methods defined in the same class.

Access modifiers can be used to avoid name collisions.

## Operators

### Arithmetic operators

All C arithmetic operators, with expected semantics.

### Logic operators

All C logic operators (but acting on `Bool`) with expected semantics.

### Assignment operators

All C assignment operators, semantically equivalent to what they are shorthands for (e.g. `a += b` is a shorthand for `a = (a+b)`).

### Dereference operators

The dot operator either accesses a member of a struct/union or calls a function with a `this` argument by passing the address of the struct/union as the `this` argument.

### User-definable operators

All operator sequences enclosed in **angle brackets** (`<` and `>`) are user-definable, and overloadable if defined in a type [class](classes).

#### Example

An example of a user-defined operator `<+>` is the following:

```
class CustomAdd {
  (a left, a right) -> a operator<+>;
  // ^ a is the type of the parameters and the return type
}
```
