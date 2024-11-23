
FROM python:3.10-slim

WORKDIR /backend

RUN apt-get update && apt-get install -y \
    curl \
    bash \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*


RUN curl -sSL https://install.python-poetry.org | python3 - \
    && export PATH="/root/.local/bin:$PATH"


ENV PATH="/root/.local/bin:$PATH"


ENV PYTHONUNBUFFERED=1 \
    POETRY_VIRTUALENVS_IN_PROJECT=true \
    PYTHONPATH="/backend/app" \
    ENV_FILE_LOCATION="/app/.env"


COPY . /backend

RUN poetry install --no-dev

# RUN chmod +x /backend/prestart.sh

# RUN poetry run bash /backend/prestart.sh

EXPOSE 8000

CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]