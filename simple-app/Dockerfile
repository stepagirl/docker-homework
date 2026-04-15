#FROM  --platform=$BUILDPLATFORM golang:1.23-alpine AS builder
FROM golang:1.23-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .

#ARG TARGETOS
#ARG TARGETARCH
#RUN CGO_ENABLED=0 GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o simple-app .
RUN go build -o simple-app .
FROM alpine:3.21
WORKDIR /app
RUN adduser -S app
COPY --from=builder /app/simple-app /app/simple-app
USER app
EXPOSE 8080
CMD ["/app/simple-app"]