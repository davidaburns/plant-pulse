FROM golang:1.21-alpine AS builder

WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download && go mod verify

COPY . .
RUN CGO_ENABLED=0 go build -o service ./cmd/service/main.go

FROM gcr.io/distroless/base-debian11
WORKDIR /app
COPY --from=builder /app/service /app/service

EXPOSE 8080
CMD ["/app/service"]