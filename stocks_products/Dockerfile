# Dockerfile
FROM python:3.11-slim

WORKDIR /app

# Установка зависимостей системы
RUN apt-get update && apt-get install -y \
    gcc \
    postgresql-client \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Копирование requirements и установка зависимостей Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копирование всего проекта
COPY . .

# Сбор статики (выполнится при запуске)
RUN python manage.py collectstatic --noinput

# Открываем порт
EXPOSE 8000

# Команда запуска через Gunicorn
CMD ["gunicorn", "stocks_products.wsgi:application", "--bind", "0.0.0.0:8000"]