# `NullVoxPopuli/action-setup-pnpm`

Correctly sets up node, pnpm, and cache for pnpm dependencies so that installation can be as fast as it can be.

## Usage:

```yaml 
steps: 
- uses: actions/checkout@v3
- uses: NullVoxPopuli/action-setup-pnpm@v1
```

## Why?

[`pnpm/action-setup`](https://github.com/pnpm/action-setup/) can install dependencies on its own, but then no cache is used from [`actions/setup-node`](https://github.com/actions/setup-node).

[`actions/setup-node`](https://github.com/actions/setup-node) configures node, (and correctly respects `volta` configurations), cache, etc

To set this up on your own, you would required _three_ manual steps in your workflow config file:
```yaml 
steps:
  # ...
  - uses: pnpm/action-setup@v2
    with:
      version: 7 
  - uses: actions/setup-node@v3
    with:
      cache: 'pnpm'
  - run: pnpm install 
```

## Options

### `node-version`

Allows changing the `node-version` passed to `actions/setup-node`.

```yaml 
- uses: NullVoxPopuli/action-setup-pnpm@v1
  with:
    node-version: 18
```

### `pnpm-version`

Allows changing the `pnpm-version` passed to `pnpm/action-setup`.

```yaml 
- uses: NullVoxPopuli/action-setup-pnpm@v1
  with:
    pnpm-version: 7.29.0
```
### `no-lockfile`

Boolean flag useful for tossing out the lockfile for testing if in-range floating dependency changes have accidentally broken things.

```yaml 
- uses: NullVoxPopuli/action-setup-pnpm@v1
  with:
    no-lockfile: true 
```
