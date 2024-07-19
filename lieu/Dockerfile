# Use the official Go image as the base image
FROM golang:1.20

# Set the working directory inside the container
WORKDIR /app

# Copy the Go modules manifests
COPY go.mod go.sum ./

# Download Go modules
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application with FTS5 tag
RUN go build --tags "fts5" -o lieu

# Create the data directory
RUN mkdir -p data

# Run the necessary commands to scrape links, crawl, and create the database
RUN ./lieu precrawl > data/webring.txt && \
    ./lieu crawl > data/crawled.txt && \
    ./lieu ingest

# Expose the application on port 10001
EXPOSE 10001

# Run the application
CMD ["./lieu", "host"]
