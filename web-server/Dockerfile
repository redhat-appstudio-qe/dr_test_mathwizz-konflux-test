# MathWizz Web-Server Service
# Go-based API server with database and message queue connections

# Build stage
FROM docker.io/library/golang:1.23-alpine AS builder

WORKDIR /app

# Install build dependencies
RUN apk add --no-cache git

# Copy go mod files
COPY go.mod go.sum ./
RUN go mod download

# Copy source code
COPY *.go ./

# Build the binary
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o web-server .

# Runtime stage
FROM docker.io/library/alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

# Copy the binary from builder
COPY --from=builder /app/web-server .

# Expose HTTP port
EXPOSE 8080

# Health check
HEALTHCHECK --interval=10s --timeout=5s --start-period=10s --retries=3 \
    CMD wget --no-verbose --tries=1 --spider http://localhost:8080/health || exit 1

# Run the binary
CMD ["./web-server"]
# konflux-test trigger run-2f903e02-9f7d-4a1e-a7aa-3345f1dc6e37 1790506007
# konflux-test trigger run-c448ed0e-86ce-490d-901c-ff453b3c963e 1790506286
# konflux-test trigger run-03aa561f-99c8-49dc-bec2-23b2ebdbfdc5 1790681920
