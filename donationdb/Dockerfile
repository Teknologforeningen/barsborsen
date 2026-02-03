FROM python:3.14-slim AS builder
COPY --from=ghcr.io/astral-sh/uv:0.9.28 /uv /uvx /bin/

ENV UV_COMPILE_BYTECODE=1
ENV UV_LINK_MODE=copy
ENV UV_NO_DEV=1
ENV UV_PYTHON_DOWNLOADS=0

WORKDIR /app

RUN --mount=type=cache,target=/root/.cache/uv \
    --mount=type=bind,source=uv.lock,target=uv.lock \
    --mount=type=bind,source=pyproject.toml,target=pyproject.toml \
    uv sync --locked --no-install-project

COPY . /app

RUN --mount=type=cache,target=/root/.cache/uv \
    uv sync --locked

FROM python:3.14-slim

RUN groupadd --system --gid 999 vision \
 && useradd --system --gid 999 --uid 999 --create-home vision

COPY --from=builder --chown=vision:vision /app /app

ENV PATH="/app/.venv/bin:$PATH"

USER vision

WORKDIR /app

EXPOSE 8000

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "--workers", "3", "donationdb.wsgi:application"]
