ARG PYTHON_VERSION=3.11
FROM python:${PYTHON_VERSION} as builder

# Set the working directory
WORKDIR /app
COPY .. .


FROM python:${PYTHON_VERSION} as run

WORKDIR /app

ENV PYTHONUNBUFFERED=1

COPY --from=builder /app .

RUN pip install --upgrade pip && \
    pip install -r requirements.txt


EXPOSE 8080

# Run database migrations and start the Django application
ENTRYPOINT [ "sh", "-c", "python manage.py migrate && python manage.py runserver 0.0.0.0:8080" ]
