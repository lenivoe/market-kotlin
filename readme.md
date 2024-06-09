 # Описание
Это реализация вступительного задания в летнюю школу бэкенд разработки 2022 от Яндекса.\
Представляет из себя приложение по размещению товаров по категориям. Категории могут быть вложены друг в друга.\
API сервиса описано в файле `openapi.yaml`.

Указанные ниже команды ориентированы на терминал-linux и потребуют небольших правок путей для windows систем.

## Особенности:
1. Проект на Kotlin + Spring Boot, в качестве БД - Postgres.
2. Реализована основаная часть API.
3. Оригинальное API слегка изменено, например убрано слово delete из названия удаляющего http-метода.
4. Несмотря на использование ORM, основные запросы к базе написаны на SQL в целях оптимизации.
5. Присутствуют тесты как для штатных случаев, так и выполнения с ошибками.
6. Приложение можно развернуть или протестировать через Docker.

# Развертывание
Чтобы развернуть приложение, выполните указанную ниже команду из папки с проектом:
```
docker compose -f=./docker/docker-compose.yml up
```
После завершения сборки, будет создано и запущено три контейнера:
- postgres - база данных, порт 5432
- app - само приложение, порт 80
- adminer - web-инструмент для работы с базой данных, порт 7777

Кроме описания API в `openapi.yaml` можно ознакомиться с примерами из тестов:
- Более полные JUnit тесты основной части API `src/test/kotlin/com/levishok/market/MarketApplicationTests.kt`
- Упрощенные тесты всего API, включая дополнительную часть на Python `e2e_tests.py`

# Тестирование
Уже развернутое приложение можно протестировать скриптом `e2e_tests.py`:


Для запуска Junit тестов есть свое окружение, достаточно выполнить команду: 
```
docker compose -f=./docker/docker-compose-testing.yml up
```
Для тестов будет поднят отдельный контейнер с базой, чтобы не портить данные из основной.\
В консольном выводе будут отражены только упавшие тесты, так что в нормальной ситуации вывода будет мало.

Чтобы увидеть полный лог работы тестов, выполните коману:
```
docker compose -f=./docker/docker-compose-testing.yml run --rm app ./gradlew test -i
```
