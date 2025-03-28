# warp-proto-apis

Repository to centralize protobuf-based APIs for Warp services and clients.
Maintains proto definitions alongside generated code for supported clients.

## General structure
```
warp-server-apis/
└── apis/
    └── <api>/
        └── <version>/
            ├── <api>.proto
            └── gen/
                └── <bindings_for_lang>/
```

## Required dependencies
Must have `protoc` installed.

### Go 
From the directory that contains the API's `.proto` file, Go bindings can be generated using:
```
protoc --go_out=gen/go --go_opt=paths=source_relative --go_opt=M<api>.proto=github.com/warp/warp-proto-apis/<api>/v1 <api>.proto 
```

Workflow: https://staging.warp.dev/drive/workflow/Generate-Go-bindings-from-Protocol-Buffers-definition-QndPWGlVfrvukqmBZmBoZ6

### Rust
Generating Rust bindings is a little bit more involved:
1. Install `protoc-gen-prost` and `protoc-gen-prost-crate`. See [here](https://github.com/neoeinstein/protoc-gen-prost/tree/main).
1. Create a bare library crate under `gen/rust`.
1. From the directory that contains the API's `.proto` file, Rust bindings can be generated using:
    ```
    protoc --prost_out=gen/rust/src <proto_file>
    ```
    Workflow: https://staging.warp.dev/drive/workflow/Generate-Rust-bindings-from-Protocol-Buffers-definition-QndPWGlVfrvukqmBZmBoZ6