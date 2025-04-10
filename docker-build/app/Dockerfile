FROM python:3.11.12-bullseye AS builder

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

WORKDIR /app

RUN pip install --upgrade pip wheel "poetry==1.8.2" \
 && poetry config virtualenvs.create false

COPY pyproject.toml poetry.lock ./

RUN poetry install --no-dev --no-interaction --no-ansi \
 && rm -rf /root/.cache/pip /root/.cache/pypoetry

FROM python:3.11.12-bullseye

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

RUN useradd -m myuser
USER myuser

WORKDIR /app

COPY --from=builder /app /app

CMD ["python", "main.py"]
