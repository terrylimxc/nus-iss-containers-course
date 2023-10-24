FROM golang:1.21-bookworm AS builder

WORKDIR /app

COPY go.mod .
COPY go.sum .
COPY main.go .

RUN CGO_ENABLED=true go build -o main ./...

FROM debian:bookworm

RUN apt update && apt install -y curl

WORKDIR /app

COPY public public
COPY templates templates

COPY --from=builder /app/main .

ENV PORT=3000 INSTANCE_NAME="Go Dev Bear" INSTANCE_HASH=abc123

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
    CMD curl -s http://localhost:${PORT}/healthz || exit 1

ENTRYPOINT ./main