# pod-typeinfo

[![Build Status](https://travis-ci.org/aldanor/pod-typeinfo.svg?branch=master)](https://travis-ci.org/aldanor/pod-typeinfo)
[![Build Status](https://ci.appveyor.com/api/projects/status/uh34kafh5qs458ue/branch/master?svg=true)](https://ci.appveyor.com/project/aldanor/pod-typeinfo)

[Documentation](http://ivansmirnov.io/pod-typeinfo/pod_typeinfo/index.html)

The `pod-typeinfo` crate provides access to type information for POD (*plain old data*)
types at runtime.

## Examples

Defining reflectable struct types only requires wrapping the struct definition in
`def!` macro (see the docs for more details):

```rust
#[use_macro]
extern crate pod_typeinfo;
use pod_typeinfo::TypeInfo;

def! {
    #[derive(Debug)]
    pub struct Color { r: u16, g: u16, b: u16, }

    #[derive(Debug)]
    #[repr(packed)]
    pub struct Palette {
        monochrome: bool,
        colors: [Color; 16]
    }
}

fn main() {
    println!("{:#?}", Palette::type_info());
}
```

Output (whitespace formatted):

```rust
Compound([
    Field { ty: Bool, name: "monochrome", offset: 0 },
    Field {
        ty: Array(
                Compound([
                    Field { ty: UInt16, name: "r", offset: 0 },
                    Field { ty: UInt16, name: "g", offset: 2 },
                    Field { ty: UInt16, name: "b", offset: 4 }
                ], 6),
            16),
        name: "colors",
        offset: 1
    }
], 97)
```

## License

`pod-typeinfo` is primarily distributed under the terms of both the MIT license and
the Apache License (Version 2.0), with portions covered by various BSD-like
licenses.

See LICENSE-APACHE, and LICENSE-MIT for details.
