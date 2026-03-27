# Repository Guidelines

## Project Structure & Module Organization
`src/` contains the library crate: parsing in `src/parser.rs`, formatting in `src/formatter.rs`, shared content and option types in `src/content.rs` and `src/options.rs`, and public exports in `src/lib.rs`. Integration coverage lives in `tests/lib.rs`. The bundled CLI example is `examples/formatjson5.rs`. Fuzzing targets are isolated under `fuzz/`, and regression inputs live in `samples/fuzz_fails_fixed/`.

## Build, Test, and Development Commands
Use Cargo for all local work:

- `cargo build` builds the library crate.
- `cargo build --example formatjson5` builds the sample CLI formatter.
- `cargo test` runs unit and integration tests.
- `cargo fmt` applies the repository `rustfmt.toml` style.
- `cargo fmt -- --check` verifies formatting in CI-friendly mode.
- `cargo clippy --all-targets --all-features -- -D warnings` treats lint warnings as failures.

Run commands from the repository root.

## Coding Style & Naming Conventions
This project uses Rust 2018 with `rustfmt` configured for Unix newlines and relaxed line-splitting heuristics. Follow the existing style: 4-space indentation, snake_case for functions and modules, CamelCase for types, and ALL_CAPS for constants. Keep modules focused; prefer adding logic to the existing parser/formatter/options split instead of creating vague utility files.

## Testing Guidelines
Add or update tests in `tests/lib.rs` for externally visible behavior changes. Use descriptive `test_*` function names that describe the formatting or parsing case being covered, for example `test_format_simple_objects`. Preserve regression inputs for parser edge cases in `samples/fuzz_fails_fixed/` when a bug came from fuzzing. Before opening a PR, run `cargo test`, `cargo fmt -- --check`, and `cargo clippy --all-targets --all-features -- -D warnings`.

## Commit & Pull Request Guidelines
Recent history uses short, imperative commit subjects such as `Fix parsing fraction with exponent` and `Apply clippy fixes`. Keep commits narrowly scoped and readable. Pull requests should describe the behavior change, note test coverage, and link the relevant issue when one exists. If user-visible CLI behavior changes, include a short example invocation or output snippet.

## Security & Contribution Notes
Do not commit secrets, generated artifacts, or local build output such as `target/`. This repository follows Google’s contribution process; contributors may need a signed CLA and all changes go through GitHub pull request review.
