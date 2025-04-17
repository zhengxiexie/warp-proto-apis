# warp-proto-apis

Repository to centralize protobuf-based APIs for Warp services and clients.
Maintains proto definitions alongside generated code for supported clients.

## General structure
```
warp-server-apis/
└── apis/
    └── <api>/
        └── <version>/
            ├── <api>.proto // or could be broken down into multiple .proto files
            └── gen/
                └── <bindings_for_lang>/
```

## Initial setup

Run `./script/bootstrap` to install proto compiler dependencies.

## Updating generated bindings

When updating the proto definitions, you will need to run the `./script/generate` script.  This will automatically update bindings for all supported languages.

For example, to update the `multi_agent` API:
```bash
./script/generate -a multi_agent -v v1
```

## Required dependencies
Must have `protoc` installed. See here on how to install for your platform: https://protobuf.dev/installation/.

### Go
Requires the `protoc-gen-go` plugin: `go install google.golang.org/protobuf/cmd/protoc-gen-go@latest`.

This is installed by the bootstrap script.

### Rust
Requires `protoc-gen-prost` and `protoc-gen-prost-crate`: `cargo install protoc-gen-prost protoc-gen-prost-crate`. 

This is installed by the bootstrap script.

## Language-specific quirks

### Rust

When adding a new API, you will need to create a bare library crate under `gen/rust` before generating bindings.