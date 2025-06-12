FROM python:3.13-slim AS builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONBUFFERED=1

RUN pip install --upgrade pip

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

FROM python:3.13-slim

RUN useradd -r vision && mkdir /app && chown -R vision /app

COPY --from=builder /usr/local/lib/python3.13/site-packages/ /usr/local/lib/python3.13/site-packages/
COPY --from=builder /usr/local/bin/ /usr/local/bin/

WORKDIR /app

COPY . .

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONBUFFERED=1

USER vision

EXPOSE 8000

CMD ["/usr/local/bin/gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "donationdb.wsgi:application"]
