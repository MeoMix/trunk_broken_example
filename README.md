This repo demos a minimal example of Trunk v0.18.0 broken functionality.

Simplest way to run it is through Docker, but a basic Rust development environment should work fine if Docker is unavailable.

Then, execute command: `trunk build`. Observe output error: 

```
root@c1898230ae93:/workspaces/trunk_broken_example# trunk build
2023-12-15T02:10:06.460768Z  INFO 🚀 Starting trunk 0.18.0
2023-12-15T02:10:06.460893Z  INFO 📦 starting build
2023-12-15T02:10:06.461730Z  INFO spawning asset pipelines
2023-12-15T02:10:06.533711Z  INFO building example_pkg
   Compiling example_pkg v0.1.0 (/workspaces/trunk_broken_example)
    Finished dev [unoptimized + debuginfo] target(s) in 0.14s
2023-12-15T02:10:06.720671Z  INFO fetching cargo artifacts
2023-12-15T02:10:06.769479Z ERROR ❌ error
error from build pipeline

Caused by:
    0: error from asset pipeline
    1: found more than one binary crate: ["example_lib", "example_pkg"], consider adding `<link data-trunk rel="rust" data-bin={bin} />` to the index.html
Error: error from build pipeline

Caused by:
    0: error from asset pipeline
    1: found more than one binary crate: ["example_lib", "example_pkg"], consider adding `<link data-trunk rel="rust" data-bin={bin} />` to the index.html
```

Confirm that `index.html` contains:

```
<html>
    <head>
        <link data-trunk rel="rust" data-bin="example_pkg" />
    </head>
</html>
```

You may then edit `data-bin` to an invalid value, i.e. `data-bin="example"`, and observe that invalid value is detected by Trunk. So, the configuraiton is being read, but is insufficient to eliminate error.

Prior to this, in v0.17.x, `cdylib` was not a supported target and so no bin configuration was required.
