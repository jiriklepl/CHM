# CHM


## Types

- Type constants begin with a capital letter (`Int`, `Char`, `Bool`, etc.).
- Type variables begin with a lower letter.
- Anonymous types are named `_`

**structs** and **unions** are types, equivalent structs and equivalent unions are considered distinct.

### Type categories

**NO REFERENCES** that would have implicit pointer semantics.

- primitive types
  - `Int`, `Long`, `Bool`, etc.
  - structs and unions
- pointers: `type*`
- functions: `(par_type1, par_type2, ...) -> return_type`

### Numeric types

Those are the types that can appear as arguments of basic arithmetic [operators](operators).

- `Bool`
- `I8`, `I16`, `I32`, `I64` (, etc.)
  - `Char` is an alias for `I8`
  - `Short` is an alias for `I16`
  - `Int` is an alias for `I32`
  - `Long` is an alias for `I64`
- `U0`, `U8`, `U16`, `U32`, `U64` (, etc.)
  - `Void` is an alias for `U0`
  - `UChar` is an alias for `U8`
  - `UShort` is an alias for `U16`
  - `UInt` is an alias for `U32`
  - `ULong` is an alias for `U64`
- `F32`, `F64`
  - `Float` is an alias for `F32`
  - `Double` is an alias for `F64`

All numeric values but `Bool` and `U8` are in `Num` [class](#classes).

## Functions

### Declaration and definition

```
1:  (parameter_list) -> noptr-declarator;
2:  (parameter_list) -> noptr-declarator {...}
```

1. basic function declaration
2. basic function definition

### Example

```
1:  () -> a* new { return (a*)malloc(sizeof(a)); }
```

1. This defines a [generic](#generic) function that returns a pointer to allocated data of `a` type.

### `pass` value and `return` statement

- `pass = value` sets the return value of the function to `value`.
- `return value` sets the return value of the function to `value` and returns the control to the caller.
- `return` returns the control to the caller without setting the return value.

## Pointers

## Classes

## Operators

### Arithmetic operators
### Logic operators
### Assignment operators

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
