# Stage 1: Build the Go binary
FROM golang:1.23-alpine AS builder

WORKDIR /app

# Download Go modules
COPY go.mod go.sum ./
RUN go mod download

# Copy source code and build the application
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o stat-service main.go

# Stage 2: Create a minimal runtime image
FROM alpine:latest

WORKDIR /root/

# Copy the binary from the builder stage
COPY --from=builder /app/stat-service .

CMD ["./stat-service"]
