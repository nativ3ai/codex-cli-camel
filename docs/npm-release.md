# npm Release (`codex-camel`)

This fork ships as package name `codex-camel` with global binaries:
- `codex`
- `codex-camel`

## User install

```bash
npm install -g codex-camel
codex --version
codex-camel --version
```

## Maintainer publish flow

1. Build release CLI binary:

```bash
cd codex-rs
cargo build -p codex-cli --release
```

2. Create vendor tree (host target shown for Apple Silicon):

```bash
mkdir -p /tmp/codex-camel-vendor/aarch64-apple-darwin/{codex,path}
cp codex-rs/target/release/codex /tmp/codex-camel-vendor/aarch64-apple-darwin/codex/codex
cp "$(command -v rg)" /tmp/codex-camel-vendor/aarch64-apple-darwin/path/rg
```

3. Stage and pack:

```bash
./codex-cli/scripts/build_npm_package.py \
  --package codex \
  --release-version 0.1.0 \
  --staging-dir /tmp/codex-camel-npm-stage \
  --vendor-src /tmp/codex-camel-vendor \
  --pack-output dist/npm/codex-camel-npm-0.1.0.tgz
```

4. Publish:

```bash
npm publish dist/npm/codex-camel-npm-0.1.0.tgz --access public
```

## Notes

- The package metadata is `name: codex-camel` in `codex-cli/package.json`.
- If publish fails with auth/registry errors, run `npm login` with an account allowed to publish `codex-camel`.
