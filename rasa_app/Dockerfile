FROM python:3.9-slim-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends curl ca-certificates && \
    curl -fsSL https://astral.sh/uv/0.6.6/install.sh -o /uv-installer.sh && \
    sh /uv-installer.sh && rm /uv-installer.sh && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

ENV PATH="/root/.local/bin:$PATH"

WORKDIR /app

COPY . /app

RUN uv venv --python 3.9 && \
    . .venv/bin/activate && \
    uv pip -r requirements.txt

CMD ["/app/.venv/bin/rasa", "run", "--cors", "*", "--enable-api", "--log-file", "rasa_debug.log", "-vv"]

