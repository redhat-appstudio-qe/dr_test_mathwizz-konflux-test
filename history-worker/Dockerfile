# MathWizz History-Worker Service
# Async worker that processes problem_solved events from NATS

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
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o history-worker .

# Runtime stage
FROM docker.io/library/alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

# Copy the binary from builder
COPY --from=builder /app/history-worker .

# No exposed ports (worker doesn't listen on HTTP)

# Run the binary
CMD ["./history-worker"]
# konflux-test trigger run-2f903e02-9f7d-4a1e-a7aa-3345f1dc6e37 1790506009
# konflux-test trigger run-c448ed0e-86ce-490d-901c-ff453b3c963e 1790506288
# konflux-test trigger run-03aa561f-99c8-49dc-bec2-23b2ebdbfdc5 1790681922
# konflux-test trigger run-6c8f8118-d1d6-4788-b7d1-0f64706a08bb 1790681980
# konflux-test trigger run-f22c1aea-e573-44ea-af9c-5353b9e7db76 1790682221
