## CARGO

`Cargo` is Rustβs build system and package manager.
---

`Cargo` handles a lot of tasks for you. Such as - 
- Building your code.
- Downloading the libraries and their dependencies.
- Building those libraries.

In Rust, `packages` of code are referred to as `crates`.

--------------------------------------------------------

Cargo Commands. 

- `cargo --version`    --->  check version.
- `cargo new <project_name>`  -----> Creating a Project with Cargo
- `cargo build` ----> build a program ποΈ. builds in `target/debug`
- `cargo build --release` ----> Compile with optimizations. builds in `target/release` instead of `target/debug`. LONGER COMPILE TIME BUT FASTER CODE. π₯
- `./target/debug/<program_name>` ---> run a program after `build` π
- `cargo run` ---> compile the code then run. π
- `cargo check` ----> quickly checks your code to make sure it compiles but doesn't produce executable. ββ
- `cargo update` ----> update a crate
-  `cargo doc --open` ---> open docs locally . ππ
