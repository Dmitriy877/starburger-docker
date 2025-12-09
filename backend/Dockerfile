# Определяем базовый образ для контейнера миграций бэкенда
FROM python:3.10-slim AS backend_migrate
# Задаем переменные окружения
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
# Задаем рабочую директорию
WORKDIR /backend
# Устанавливаем зависимости общие
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential libpq-dev && \
    rm -rf /var/lib/apt/lists/*
# Копируем файл с зависимостями
COPY requirements.txt ./requirements.txt
# Устанавливаем зависимости проекта
RUN pip install -r requirements.txt
# Копируем директорию проекта
COPY . .
# Запускаем миграции
CMD ["python", "manage.py", "migrate", "--noinput"]


# Определяем базовый образ для конетйнера запуска бэкенда
FROM python:3.10-slim AS backend
# Задаем переменные окружения
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
# Задаем рабочую директорию
WORKDIR /backend
# Устанавливаем зависимости общие
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential libpq-dev && \
    rm -rf /var/lib/apt/lists/*

# Копируем файл с зависимостями
COPY requirements.txt ./requirements.txt

# Устанавливаем зависимости проекта
RUN pip install -r requirements.txt
# Копируем директорию проекта
COPY . .
# Заускаем backend
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

