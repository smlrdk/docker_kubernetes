# Базовый image
FROM python:3.10-alpine

# Переменные для создания окружения
ARG USER=app 
ARG UID=1001
ARG GID=1001

# Создание пользователя ОС и каталога
RUN addgroup -g ${GID} -S ${USER} \
   && adduser -u ${UID} -S ${USER} -G ${USER} \
   && mkdir -p /app \
   && chown -R ${USER}:${USER} /app
USER ${USER}

# Копирование файла, необходимых для работы приложения
COPY --chown=$USER:$USER hello.html /app

# Рабочий каталог, где будет запущено приложение
WORKDIR /app

# Порт web-сервера, который будет открыт в контейнере
EXPOSE 8000

# Команда запуска web-сервера
CMD ["python3", "-m", "http.server", "8000"]