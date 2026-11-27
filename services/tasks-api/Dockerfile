FROM python:3.12-slim@sha256:5e2bdb1b0d542d5039cffb8181c65930093949194a65c365dfb1b0fe13a4fa5b

# Pick up Debian security fixes the base image does not have yet: zlib1g (CVE-2026-85091), libzstd1 (CVE-2026-124851)
RUN apt-get update \
    && apt-get install -y --no-install-recommends --only-upgrade zlib1g libzstd1 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app ./app

RUN useradd --create-home appuser
USER appuser

EXPOSE 5000

CMD ["flask", "--app", "app:create_app", "run", "--host=0.0.0.0", "--port=5000"]