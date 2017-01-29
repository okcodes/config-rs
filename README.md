# config-rs
[![Build Status](https://travis-ci.org/mehcode/config-rs.svg?branch=master)](https://travis-ci.org/mehcode/config-rs)
> Layered configuration system for Rust applications (with strong support for [12-factor] applications).

[12-factor]: https://12factor.net/config
 
 - Set defaults
 - Set explicit values (to programmatically override)
 - Read from [JSON] and [TOML] files
 - Read from environment
 - Loosely typed — Configuration values may be read in any supported type, as long as there exists a reasonable conversion

[JSON]: https://github.com/serde-rs/json
[TOML]: https://github.com/toml-lang/toml

## Install

```toml
[dependencies]
config = { git = "https://github.com/mehcode/config-rs.git" }
```

#### Features

 - **json** - Adds support for reading JSON files
 - **toml** - Adds support for reading TOML files (included by default)

## Usage

Configuration is gathered by building a `Source` and then merging that source into the 
current state of the configuration.

```rust
// Add environment variables that begin with RUST_
config::merge(config::Environment::new("RUST"));

// Add 'Settings.json'
config::merge(config::File::new("Settings", config::FileFormat::Json));

// Add 'Settings.$(RUST_ENV).json`
let name = format!("Settings.{}", config::get_str("env").unwrap());
config::merge(config::File::new(&name, config::FileFormat::Json));
```

Note that in the above example the calls to `config::merge` could have 
been re-ordered to influence the priority as each successive merge 
is evaluated on top of the previous.

See the [examples](https://github.com/mehcode/config-rs/tree/master/examples) for 
more usage information.

## License

config-rs is primarily distributed under the terms of both the MIT license and the Apache License (Version 2.0).

See LICENSE-APACHE and LICENSE-MIT for details.