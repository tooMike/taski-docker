# Описание

Taski – это сервис для создания онлайн заметок. Проект реализован на фреймворке Django.

# Автор проекта

[Mikhail](https://github.com/tooMike)

# Установка и запуск с Docker

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/tooMike/taski-docker
```

```
cd taski-docker
```

Запустить сборку проекта:

```
docker compose up
```

Выполнить сбор статики в контейнере backend:

```
docker compose exec backend python manage.py collectstatic
```

Выполнить миграции в контейнере backend:

```
docker compose exec backend python manage.py migrate
```

Проект будет доступен по адресу

```
http://127.0.0.1:8000/
```

# Добавление тестовых данных в базу данных

Выполнить команду import_data в контейнере backend:

```
docker compose exec backend python manage.py import_data
```

# Основные технические требования

Python==3.9

# Примеры запросов к API

### Регистрация нового пользователя

Описание метода: Подтвердить email для регистрации нового пользователя в сервисе. Права доступа: Доступно без токена.

Тип запроса: `POST`

Эндпоинт: `/api/auth/email_verification/`

Обязательные параметры: `email`

Пример запрос:

```
{
  "email": "vpupkin@yandex.ru",
}
```

Пример успешного ответа:

```
{
  "email": "vpupkin@yandex.ru",
}
```

### Получение списка товаров

Описание метода: Получение списка товаров. Права доступа: Аутентифицированные пользователи.

Тип запроса: `GET`

Эндпоинт: `/api/products/`

Доступен поиск по полю name: `/api/products/?search=name`

Доступна сортировка по полям name, actual_price, rating: `/api/products/?ordering=-actual_price,rating,name`


Пример успешного ответа:

```
{
    "count": 40,
    "next": "http://127.0.0.1:8000/api/products/?page=2",
    "previous": null,
    "results": [
        {
            "name": "Дрель Bosch",
            "price": "5000.00",
            "sale": 10,
            "actual_price": "4500.00",
            "image": "http://127.0.0.1:8000/media/product_images/default_image.png",
            "category": "Дрели",
            "manufacturer": "Bosch",
            "num_shop": 8,
            "num_products": 899,
            "rating": null
        },
        ...

    ]
}
```
