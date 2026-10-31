# Logbook

A standalone digital observation log with tags, search, editing, browser sessions and durable sharded storage.

## Install and run

Tested with Homebrew FP-RISC 0.12.0 on macOS ARM64.

```sh
brew install hyperswine/tap/fprisc
git clone https://github.com/hyperswine/logbook.git
cd logbook
sol project.sol build
sol project.sol run --port=6700
```

Open http://127.0.0.1:6700/. Data defaults to `data/logbook.kvlog` plus its sibling `.store` directory. Use `--store=PATH`, `--address=ADDRESS`, `--dev` or `--replay` as in the upstream example.

## Test

```sh
sol project.sol test
```

Native tests cover tags, legacy parsing, store roundtrips/deletion, search and ID reservation. The Sol integration test starts a real server on an ephemeral loopback port and checks its HTTP response/title, then cleans up the owned process.

Builds can take several minutes for the larger applications. Build/test commands have explicit deadlines and return a failure when a child process fails. Generated binaries, caches, data, keys and raw logs are excluded from Git.

## Build tools

All project orchestration and test scripts are **Sol**. There are no Makefiles, Python or Node scripts.

The application is built directly with `fpr build`; its ordinary native executable runs without Sol. Sol drives builds, tests and the optional launcher. Native builds still need Xcode Command Line Tools; standard filesystem utilities are used to prepare directories. Test HTTP requests use Sol's linked libcurl backend, with no curl executable.

## Source and license

Extracted from [hyperswine/fprisc](https://github.com/hyperswine/fprisc/tree/8a25e670b5a7edf52f1286d294b0d14d053d98dc) at `8a25e670b5a7edf52f1286d294b0d14d053d98dc`. See [ORIGIN.md](ORIGIN.md) for the source map and local changes, and [LICENSE](LICENSE) for the upstream MIT license. No existing application data, private credentials, deployed host configuration or original source checkout is required.
