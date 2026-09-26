# Repository instructions

Boa is a Rust JavaScript engine workspace. `core/` owns the engine/parser/AST and related crates, `cli/` the executable, `tests/` shared test tooling, and `docs/` architecture notes. Read `CONTRIBUTING.md` and relevant crate tests before changing language semantics. Preserve ECMAScript behavior and add a focused regression case for fixes.

`Cargo.toml` specifies Rust 1.91.0 minimum and edition 2024; use a compatible toolchain and the checked-in lockfile. From the root, `cargo build` and `cargo test` are the basic commands. Start with `cargo test -p <affected-crate> <test-filter>`. Formatting is `cargo fmt --all --check`; see `make/ci.toml` and `.github/workflows/rust.yml` for the actual Clippy/feature matrix rather than assuming a default-feature test covers CI.

CI also builds/tests with its ci profile and annex-b, intl_bundled, experimental, and embedded_lz4 features, uses cargo-nextest, and runs doc tests and MSRV checks. Run the relevant gates for the change; do not launch the full conformance/benchmark matrix for prose. Test262 uses the separate tester and suite prerequisites documented in CONTRIBUTING; fixture/unit success is not a full conformance result.

Use `cargo run -- <fixture.js>` for a controlled CLI smoke check when behavior warrants it, and inspect output against the intended semantics. No Node application build is implied by the formatting-only package.json. For documentation/instructions, inspect links and run `git diff --check -- <changed-paths>`.

Complete the authorized change through relevant verification and repair of introduced failures. Resolve routine implementation choices directly; ask only for information or decisions that materially affect the result. If blocked, name the affected action and missing prerequisite, continue independent work, and close with changed paths, checks actually run, and unverified behavior.
