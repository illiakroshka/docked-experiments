# Docker experiments

## Python 

Checkout directory `python -> lab-03-starter-project-python` and run build image: 

```bash
docker build -t python-labs .
```

Running container:

```bash
docker run -p 8080:8080 python-labs
```

Dockerfile:

```Dockerfile
FROM python:3.10-alpine


WORKDIR /app


COPY requirements.lock /app/


RUN pip install -r requirements.lock


COPY . /app


CMD ["uvicorn", "spaceship.main:app", "--host=0.0.0.0", "--port=8080"]
```

## Go 

Checkout directory `go -> lab-03-starter-project-golang` and run build image: 

```bash
docker build -t go-labs .
```

Running container:

```bash
docker run -p 8080:8080 go-labs
```

Dockerfile:

```Dockerfile

ROM golang:alpine AS builder


WORKDIR /app


COPY go.mod go.sum ./


RUN go mod download && \
go mod verify


COPY . .


RUN go build -o fizzbuzz


FROM gcr.io/distroless/base-debian12


WORKDIR /app


COPY --from=builder /app/fizzbuzz .
COPY --from=builder /app/templates/index.html templates/


EXPOSE 8080


CMD ["./fizzbuzz", "serve"]
```

## Node.js

Checkout directory `nodejs -> WordCraft`, set .evn file in config directory and run build image: 

```bash
docker build -t tg-bot .
```

Running container:

```bash
docker run --env-file ./config/.env tg-bot
```

Dockerfile:

```Dockerfile
FROM node:lts-alpine


COPY package.json ./
RUN npm install


COPY . .


EXPOSE 3000


CMD ["npm","run","start"]
```