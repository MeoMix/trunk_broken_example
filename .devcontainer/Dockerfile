FROM rust:1.74-bookworm

RUN rustup toolchain install nightly
RUN rustup default nightly
RUN rustup target install wasm32-unknown-unknown

RUN cargo install trunk