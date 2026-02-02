# Counter Program

A simple Solana counter program built with Anchor framework.

## Prerequisites

- [Rust](https://rustup.rs/)
- [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)
- [Anchor CLI](https://www.anchor-lang.com/docs/installation)
- [Docker](https://docs.docker.com/engine/install/) (for verified builds)
- solana-verify CLI: `cargo install solana-verify`

## Build

```bash
anchor build
```

## Deploy

```bash
anchor deploy
```

## Verified Build and Deploy

Verified builds ensure reproducibility across different systems using Docker.

### Build

```bash
solana-verify build --library-name counter
```

### Get Executable Hash

```bash
solana-verify get-executable-hash target/deploy/counter.so
```

### Deploy

```bash
solana program deploy -u <NETWORK_URL> target/deploy/counter.so \
  --program-id <PROGRAM_ID> \
  --with-compute-unit-price 50000 \
  --max-sign-attempts 100 \
  --use-rpc
```

### Verify On-chain Program

```bash
# Get on-chain program hash
solana-verify get-program-hash -u <NETWORK_URL> <PROGRAM_ID>

# Verify against repository
solana-verify verify-from-repo -u <NETWORK_URL> \
  --program-id <PROGRAM_ID> \
  https://github.com/<REPO_PATH> \
  --commit-hash <COMMIT_HASH> \
  --library-name counter
```

## IDL Management

### Build IDL

```bash
anchor idl build
```

### Initialize IDL (first time)

```bash
anchor idl init -f target/idl/counter.json <PROGRAM_ID>
```

### Upgrade IDL (subsequent updates)

```bash
anchor idl upgrade <PROGRAM_ID> -f target/idl/counter.json
```

### Fetch IDL from Chain

```bash
anchor idl fetch <PROGRAM_ID>
```

### Check IDL Authority

```bash
anchor idl authority <PROGRAM_ID>
```

### Transfer IDL Authority

```bash
anchor idl set-authority -n <NEW_AUTHORITY> -p <PROGRAM_ID>
```

### Make IDL Immutable

```bash
anchor idl erase-authority -p <PROGRAM_ID>
```

## Program Instructions

```
initialize - Create a new counter account (PDA with seed "counter")
increment  - Increase counter by 1
decrement  - Decrease counter by 1
```
