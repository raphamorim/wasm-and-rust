<h1 align="center">WebAssembly and Rust</h1>
<h3 align="center">~ A Web Love Story ~</h3>

<p align="center">
  <img src="resources/wasm.png" height="100"/>
  <img height="60" src="resources/love-gif.gif" alt="love gif"/>
  <img height="100" src="resources/rustacean.png" alt="Rustacean"/>
</p>


## WebAssembly (WASM)

WebAssembly or WASM is a low-level bytecode format for in-browser client-side scripting, evolved from JavaScript. Its initial aim is to support compilation from C and C++, though other source languages such as [Rust](https://www.rust-lang.org/en-US/) are also supported.

#### C (Input Source)

```c
int factorial(int n) {
  if (n == 0)
    return 1;
  else
    return n * factorial(n-1);
}
```

#### Linear Assembly Bytecode ([IR](https://en.wikipedia.org/wiki/Intermediate_representation))

Data structure used internally by wasm compiler to represent source code.

```
get_local 0
i64.eqz
if i64
    i64.const 1
else
    get_local 0
    get_local 0
    i64.const 1
    i64.sub
    call 0
    i64.mul
end
```

#### WASM binary encoding

In hexadecimal:

```
20 00
50
04 7E
42 01
05
20 00
20 00
42 01
7D
10 00
7E
0B
```

The WASM compiler system internally uses [s-expressions](https://en.wikipedia.org/wiki/S-expression) - notation for nested list (tree-structured) data, invented for and popularized by the programming language [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)), which uses them for source code as well as data - for parsing simplicity as well to handle intermediate code.

An example is shown below:

```lisp
(module
  (type $FUNCSIG$dd (func (param f64) (result f64)))
  (import "global.Math" "exp" (func $exp (param f64) (result f64)))
  (memory 256 256)
  (export "memory" (memory 0))
  (func $doubleExp (param $0 f64) (result f64)
    (f64.mul
      (call $exp
        (get_local $0)
      )
      (f64.const 2)
    )
  )
  (export "doubleExp" (func $doubleExp))
)
```

## Rust Language

Rust is a systems programming language sponsored by Mozilla Research, which describes it as a "safe, concurrent, practical language," supporting functional and imperative-procedural paradigms. Rust is syntactically similar to C++, but its designers intend it to provide better memory safety while maintaining performance.

Rust is an open source programming language. Its designers have refined the language through the experiences of writing the Servo web browser layout engine and the Rust compiler.


## References

- https://en.wikipedia.org/wiki/WebAssembly
- https://en.wikipedia.org/wiki/Rust_(programming_language)
- https://hoverbear.org/2017/04/06/the-path-to-rust-on-the-web/
- http://cultureofdevelopment.com/blog/build-your-first-thing-with-web-assembly/
- https://github.com/mbasso/awesome-wasm
- https://hacks.mozilla.org/2017/02/a-cartoon-intro-to-webassembly/
- https://codelabs.developers.google.com/codelabs/web-assembly-intro/index.html?index=..%2F..%2Findex#0
- https://github.com/mrfr0g/rust-webassembly
- https://internals.rust-lang.org/t/state-of-webassembly-and-rust/6077
