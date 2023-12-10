FROM cgr.dev/chainguard/python:latest-dev as builder

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt --user

FROM cgr.dev/chainguard/python:latest

ENV REDIS_HOST="redis-server"

WORKDIR /app

COPY --from=builder /home/nonroot/.local/lib/python3.12/site-packages /home/nonroot/.local/lib/python3.12/site-packages

COPY --from=builder /home/nonroot/.local/bin  /home/nonroot/.local/bin

ENV PATH=$PATH:/home/nonroot/.local/bin

COPY . .

ENTRYPOINT ["flask", "run", "--host=0.0.0.0"]