# Operations

## Table of Supported Operations

| Operation       | Description                                                | Requirements                           |
| :--             | :-----------------:                                        | -----------:                           |
|  +              | Adds two concealed types together                          | Types must be concealed                |
|  -              | Subtracts two concealed types together                     | Types must be concealed                |
|  *              | Multiplies two concealed types together                    | Types must be concealed                |
|  /              | Divides two concealed types together                       | Types must be concealed                |
|  ^              | XOR two concealed types together                           | Types must be integer                  |
|  &              | AND two concealed types together                           | Types must be integer                  |
|  <              | returns a bool if one value is less than the other             | Upper bound must have a known bit size |
|  <=             | returns a bool if one value is less than or equal to the other | Upper bound must have a known bit size |
|  >              | returns a bool if one value is more than the other             | Upper bound must have a known bit size |
|  >=             | returns a bool if one value is more than or equal to the other | Upper bound must have a known bit size |
|  ==             | returns a bool if one value is equal to the other              | Both types must not be constants       |
|  !=             | returns a bool if one value is not equal to the other          | Both types must not be constants       |

### Predicate Operators

`<,<=, !=, == , >, >=` are known as predicate/comparison operations because they compare two values. This differs from the operations such as `+` where the operands are used in _computation_.

### Bitwise Operations Example

```rust,noplaypen
fn main(x : Field) {
    let y = x as u32;
    let z = y & y;
}
```

`z` is implicitly constrained to be the result of `y & y`. The `&` operand is used to denote bitwise `&`.

> `x & x` would not compile as `x` is a `Field` and not an integer type.

### Logical Operators

Noir has no support for the logical operators `||` and `&&`.
This is because encoding the short-circuiting that these operators require can be inefficient for Noir's backend.
Instead you can use the bitwise operators `|` and `&` which operate indentically for booleans, just without the short-circuiting.

```rust,noplaypen
let my_val = 5;

let mut flag = 1;
if (my_val > 6) | (my_val == 0) {
    flag = 0;
}
constrain flag == 1;

if (my_val != 10) & (my_val < 50) {
    flag = 0;
}
constrain flag == 0;
```
