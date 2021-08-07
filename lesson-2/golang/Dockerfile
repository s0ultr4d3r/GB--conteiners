FROM golang as builder

RUN mkdir /app

COPY . /app

WORKDIR /app
COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o server .


FROM scratch

COPY --from=builder /app/server /

EXPOSE 8080
CMD ["/server"]