# Debug

Tutti i tipi che vogliono utilizzare la formattazione `std::fmt` richiedono un'implementazione
per essere stampati. Le implementazioni automatiche sono fornite solo
per tipi come quelli della libreria `std`. Tutti gli altri *devono* essere implementati manualmente
in qualche modo.

Il `trait` `fmt::Debug` rende questo molto semplice. *Tutti* i tipi possono
`implementare` (creare automaticamente) l'implementazione di `fmt::Debug`. Questo non è
non è vero per `fmt::Display`, che deve essere implementato manualmente.

```rust
// This structure cannot be printed either with `fmt::Display` or
// with `fmt::Debug`.
struct UnPrintable(i32);

// The `derive` attribute automatically creates the implementation
// required to make this `struct` printable with `fmt::Debug`.
#[derive(Debug)]
struct DebugPrintable(i32);
```

All `std` library types are automatically printable with `{:?}` too:

```rust,editable
// Derive the `fmt::Debug` implementation for `Structure`. `Structure`
// is a structure which contains a single `i32`.
#[derive(Debug)]
struct Structure(i32);

// Put a `Structure` inside of the structure `Deep`. Make it printable
// also.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Printing with `{:?}` is similar to with `{}`.
    println!("{:?} months in a year.", 12);
    println!("{1:?} {0:?} is the {actor:?} name.",
             "Slater",
             "Christian",
             actor="actor's");

    // `Structure` is printable!
    println!("Now {:?} will print!", Structure(3));

    // The problem with `derive` is there is no control over how
    // the results look. What if I want this to just show a `7`?
    println!("Now {:?} will print!", Deep(Structure(7)));
}
```

So `fmt::Debug` definitely makes this printable but sacrifices some elegance.
Rust also provides "pretty printing" with `{:#?}`.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Pretty print
    println!("{:#?}", peter);
}
```

One can manually implement `fmt::Display` to control the display.

### See also:

[`attributes`][attributes], [`derive`][derive], [`std::fmt`][fmt],
and [`struct`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md

