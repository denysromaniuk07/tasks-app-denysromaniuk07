FROM python:3.12-slim

# Pick up the Debian security fix for zlib1g (CVE-2026-85091) that the base image does not have yet
RUN apt-get update \
    && apt-get install -y --no-install-recommends --only-upgrade zlib1g \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app ./app

RUN useradd --create-home appuser
USER appuser

EXPOSE 5001

CMD ["flask", "--app", "app:create_app", "run", "--host=0.0.0.0", "--port=5001"]