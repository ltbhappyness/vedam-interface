# Vedam interface

These files are the messages an application speaks when it calls a Vedam node. The same message is the request and the response.

## One call

`vedam/types.proto` defines `Message`. Its file option `namespace_uuid` is the 16-byte Vedam namespace those vertical ids are hashed under. A vertical’s own enums live in that vertical’s file, not in `types.proto`.

- `key` is the object key. A singleton such as system leaves it empty.
- `attrs` is the attribute list, in the caller’s order. Each attribute has an id, a value, and its own status.
- `status` is the overall result. The node walks every attribute. The overall code is success when every attribute succeeded. Otherwise it is the first failure.

## Verticals

Each other file is one vertical. The comment at the top is how to fill `Message`. The attribute enum in that file is the set of ids a caller puts in `Attr.id`. The service option `vertical_uuid` is that vertical’s id.

Get, Subscribe, and Unsubscribe each take `Message` and return one `Message`. Subscribe registers a watch. Notify returns the stream of later changes for that watch. Unsubscribe removes a watch.

```
vedam/types.proto       Shared message, attribute, and status types
vedam/system.proto      Node instance
vedam/identity.proto    Identity objects, addressed by key
vedam/storage.proto     Storage objects, addressed by key
vedam/security.proto    Security singleton
vedam/wasm.proto        WebAssembly configuration singleton
```

## Compile

Set the include path to the repository root:

```bash
protoc -I. --python_out=/tmp vedam/types.proto vedam/system.proto \
  vedam/identity.proto vedam/storage.proto vedam/security.proto \
  vedam/wasm.proto
```

## License

[GNU AGPL version 3](LICENSE), with the additional permission and the name term in that file. An application may compile these messages and speak them. A changed copy is not called Vedam.
