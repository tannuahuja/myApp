# Use a minimal base image
FROM golang:alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the Go module dependency files
COPY go.mod go.sum ./

# Download and install Go dependencies
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN go build -o app

# Command to run the executable
CMD ["./app"]
