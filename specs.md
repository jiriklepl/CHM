# CHM


## Types

- Type constants begin with a capital letter (`Int`, `Char`, `Bool`, etc.).
- Type variables begin with a lower letter.
- Anonymous types are named `_`

**structs** and **unions** are types, equivalent structs and equivalent unions are considered distinct.

### Type categories

**NO REFERENCES**

- primitive types
  - `Int`, `Long`, `Bool`, etc.
  - structs and unions
- pointers: `type*`
- functions: `(par_type1, par_type2, ...) -> return_type`

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

1. This defines a [generic](#generic) function that returns a pointer to an allocated data of `a` type.
