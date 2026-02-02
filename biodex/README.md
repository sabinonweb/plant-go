\# Biodex - Solana Project

Iodex is a Solana-based decentralized application (dApp) written in Rust. This project demonstrates building, deploying, and interacting with Solana programs (smart contracts) using the Solana CLI and optionally Anchor.

\## Table of Contents

\- \[Prerequisites\](#prerequisites)

\- \[Installation\](#installation)

\- \[Building the Program\](#building-the-program)

\- \[Deploying the Program\](#deploying-the-program)

\- \[Running the Program\](#running-the-program)

\- \[Testing\](#testing)

\- \[Project Structure\](#project-structure)

\- \[Troubleshooting\](#troubleshooting)

\---

\## Prerequisites

Before you begin, make sure you have the following installed:

\- Rust (latest stable)

\`\`\`bash

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

rustup update

Solana CLI (v1.14+ recommended)

sh -c "$(curl -sSfL https://release.solana.com/stable/install)"

solana --version

\[Optional\] Anchor (if using Anchor framework)

cargo install --git https://github.com/coral-xyz/anchor avm --locked

avm install latest

avm use latest

anchor --version

Node.js and npm (for frontend integration)

Git

Installation

Clone this repository:

git clone https://github.com/your-username/iodex.git

cd iodex

Set your Solana CLI to devnet for testing:

solana config set --url https://api.devnet.solana.com

Generate a keypair (if you don’t have one):

solana-keygen new --outfile ~/.config/solana/id.json

Check your balance (you can request test SOL from the faucet):

solana airdrop 2

solana balance

Building the Program

Using Cargo

cargo build-sbf

\# or for release build

cargo build-sbf --release

This compiles your Rust program to the SBF (Solana Bytecode Format) target.

Using Anchor (Optional)

anchor build

Compiled artifacts are placed in:

target/deploy/

Deploying the Program

Deploy your program to the Solana cluster:

solana program deploy target/deploy/iodex.so

This will output a program ID, which is needed to interact with your program.

Running the Program

You can interact with your program using:

Solana CLI commands

Custom scripts (Rust, Node.js, or TypeScript)

Anchor tests / scripts (if using Anchor)

Example CLI interaction:

solana program show

solana program close \--recipient

Testing

Run Rust unit tests:

cargo test

If using Anchor:

anchor test

This will spin up a local validator and run your tests automatically.

Project Structure

iodex/

├─ Cargo.toml # Rust dependencies

├─ src/

│ └─ lib.rs # Solana program code

├─ target/deploy/ # Compiled SBF program

├─ tests/ # Unit / integration tests

└─ README.md

src/lib.rs: Main program logic

tests/: Rust integration tests or Anchor tests

target/deploy/: Output of SBF compilation

Troubleshooting

build-sbf not recognized: Use cargo build-sbf instead of solana build-sbf.

Insufficient SOL: Request more from devnet faucet.

Version mismatch: Make sure Solana CLI, Rust, and Anchor (if used) are up-to-date.

Program ID mismatch: Make sure you use the correct deployed program ID when interacting.nstruction Structure:
