# # FROM golang:1.17
# FROM golang:1.23

# WORKDIR /go/src/app

# COPY *.go .

# # RUN go mod init dispatch && go get
# # RUN go install
# RUN go mod init dispatch && go mod tidy
# RUN go build -o dispatch .

# # CMD dispatch

# CMD ["/dispatch"]

FROM golang:1.23 AS builder

WORKDIR /go/src/app
COPY *.go .
RUN go mod init dispatch && go mod tidy
RUN CGO_ENABLED=0 GOOS=linux go build -o /dispatch .

FROM debian:11-slim
COPY --from=builder /dispatch /dispatch
RUN chmod +x /dispatch

CMD ["/dispatch"]