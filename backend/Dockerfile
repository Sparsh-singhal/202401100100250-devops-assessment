FROM python:3.9-alpine
WORKDIR /app

RUN adduser -D appuser

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

USER appuser
ARG APP_VERSION=dev
ENV APP_VERSION=${APP_VERSION}

CMD ["python", "app.py"]