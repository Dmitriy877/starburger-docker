# Определяем базовый образ с установленными зависмостями
FROM python:3.10-slim AS base-image

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
RUN pip install --no-cache-dir -r requirements.txt
# Копируем директорию проекта
COPY . .


# Определяем базовый образ для контейнера миграций бэкенда
FROM base-image AS backend_migrate
# Запускаем миграции
CMD ["python", "manage.py", "migrate", "--noinput"]

# Определяем базовый образ для контейнера сбора статики+
FROM base-image AS backend_collectstatic
# Задаем переменные окружения
CMD [ "sh", "-lc", "python", "manage.py", "collectstatic", "--noinput"]


# Определяем базовый образ для конетйнера запуска бэкенда
FROM base-image AS backend
# Заускаем backend
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

