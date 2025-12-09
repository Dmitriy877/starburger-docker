# Определяем базовый образ
FROM node:16.16.0-slim

# Задаем рабочую директорию
WORKDIR /frontend

# Копируем файлы зависимостей
COPY package-lock.json ./package-lock.json
COPY package.json ./package.json

# Устанавливаем зависимости проекта
RUN npm ci --dev

# Копируем все файлы проекта
COPY . .

# Запускаем сборку проекта
CMD ["./node_modules/.bin/parcel", "watch" "bundles-src/index.js", "--dist-dir", "bundles", "--public-url=./"]

