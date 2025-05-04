# Use the official Golang image to create a build artifact
FROM golang:1.21-alpine AS builder

# Set environment variables
ENV CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# Create app directory
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy the source code
COPY . .

# Build the Go app
RUN go build -o main .

# Use a minimal final image
FROM alpine:latest

WORKDIR /root/

# Copy binary from build stage
COPY --from=builder /app/main .

# Run the binary
CMD ["./main"]
