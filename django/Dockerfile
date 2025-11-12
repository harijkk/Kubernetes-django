FROM python:3.10-slim

WORKDIR /app
# Install system dependencies (recommended for psycopg2 and other libs)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*


COPY requirements.txt .


# Ensure gunicorn is installed (if it's not already in requirements.txt)
RUN pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir gunicorn

RUN pip install --no-cache-dir -r requirements.txt

COPY notes /app
ENV PYTHONUNBUFFERED=1
CMD ["gunicorn", "notes.wsgi:application", "--bind", "0.0.0.0:8000"]
