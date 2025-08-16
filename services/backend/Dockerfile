# Stage 1: build
FROM rust:1.71-slim AS builder
WORKDIR /app
COPY Cargo.toml Cargo.lock ./
RUN mkdir src && echo "fn main() {}" > src/main.rs
RUN cargo build --release
COPY ./src ./src
RUN cargo build --release

# Stage 2: runtime
FROM debian:buster-slim
WORKDIR /app
COPY --from=builder /app/target/release/backend .
CMD ["./backend"]