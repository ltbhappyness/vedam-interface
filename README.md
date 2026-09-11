# Vedam interface

Public message files for applications that talk to a Vedam node.

## Layout

```
vedam/
  types.proto    Common keys, attribute structures, errors, and the event envelope
  system.proto   System class — Create starts a node instance
```

Further class files will be added here as each slice of the platform is designed.

Compile with the include path set to the repository root:

```bash
protoc -I. --python_out=/tmp vedam/types.proto vedam/system.proto
```

## Plugin names

`System.Update` can ask the node to load or unload an **optional** plugin by **registered identifier** (for example `overlay`), not by a filesystem path. The node maps that identifier to a shared object in its own plugin directory. See comments on `SystemUpdateRequest` in `vedam/system.proto`.

## License

[Apache License 2.0](LICENSE). Applications may generate stubs and speak these messages. Trademark and the word *Vedam* remain with [ltbh.org](https://ltbh.org); see [NOTICE](NOTICE).
