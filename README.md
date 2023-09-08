# spicedb-client-rust

Rust client for [SpiceDB](https://github.com/authzed/spicedb), generated from protobuf definitions

## How to build

This package translates protobuf definitions for SpiceDB hosted on
[buf.build](https://buf.build/authzed/api/tree/main/authzed/api) into a Rust gRPC client built with
[tonic](https://docs.rs/tonic/latest/tonic/).

### Prequisites

0. Make sure protoc is installed - https://grpc.io/docs/protoc-installation
1. Install `buf` CLI - https://docs.buf.build/installation
2. Install `cargo-make` - `cargo install cargo-make`

### Regenerating the client

If you need to generate a new version of the client, run

```
cargo make build
```

This will use the `buf` CLI to pull the latest protobuf definitions as well as any dependencies into
the `proto` directory. It will then run a cargo build, generating the needed Rust code which you can
include using [`tonic::include_proto`](https://docs.rs/tonic/latest/tonic/macro.include_proto.html).

### Including in the crate

If you are building because a new version of the SpiceDB API is released, you can use
`tonic::include_proto` to pull in the generated code for the new version's gRPC module and nest it
under the appropriate Rust module name. For example,

```rust
pub mod v1 {
    tonic::include_proto!("authzed.api.v1");
}
```

## How to release

This crate is currently not distributed on crates.io. For now, simply tag the repo with a version
string that matches the version string in Cargo.toml and reference it using a git dependency in your
project.
