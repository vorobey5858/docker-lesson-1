# Практика: Docker Lesson 1

## Цель

Собрать свой первый образ на базе `nginx`, запустить контейнер и открыть страницу в браузере.

## Структура папки

```text
docker-lesson-1/
  app/
    index.html
  Dockerfile
  .dockerignore
  README.md
```

## Шаг 1. Посмотрите содержимое файлов

Убедитесь, что в папке есть:

- `app/index.html`
- `Dockerfile`

## Шаг 2. Соберите образ

```bash
docker build -t lesson-site:1.0 .
```

Что важно:

- `-t` задает тег образа;
- точка в конце означает текущий контекст сборки.

## Шаг 3. Запустите контейнер

```bash
docker run -d --name lesson-site -p 8080:80 lesson-site:1.0
```

## Шаг 4. Проверьте результат

```bash
docker ps
docker logs lesson-site
```

Откройте в браузере:

`http://localhost:8080`

## Шаг 5. Измените страницу

Измените текст в `app/index.html`, например заголовок страницы.

После этого выполните:

```bash
docker stop lesson-site
docker rm lesson-site
docker build -t lesson-site:1.1 .
docker run -d --name lesson-site-v2 -p 8081:80 lesson-site:1.1
```

Проверьте страницу:

`http://localhost:8081`

## Если что-то не получилось

Проверьте:

- не забыта ли точка в `docker build`;
- не остался ли старый контейнер с тем же именем;
- не открыт ли не тот порт;
- пересобрали ли вы образ после изменения HTML;
- не перепутали ли имя контейнера и тег образа.

## Очистка после практики

```bash
docker stop lesson-site-v2
docker rm lesson-site-v2
```
