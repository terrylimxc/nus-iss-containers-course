FROM python:3.11

WORKDIR /app

RUN apt update && apt install -y curl

COPY ./ .

# Install dependencies
RUN pip install --no-cache-dir --upgrade pip && \
    pip install -r /app/requirements.txt

ENV PORT=3000
ENV INSTANCE_NAME = ""
ENV INSTANCE_HASH = ""

EXPOSE ${PORT}

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
    CMD curl -s http://localhost:${PORT}/healthz || exit 1

ENTRYPOINT python main.py