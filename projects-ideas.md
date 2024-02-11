### `[DevOps]` Kube-logging + Minio + Clickhouse

#### Description (ENG):

Write a simple k8s specs that will create a cluster that will generate fake logs, 
send them in the Minio service and aggregate them using Clickhouse 


### `[BACK]` Golang Astrology service (task from BETERA)

#### Description (RUS):

Напишите сервис юного астролога.
Сервис должен выполнять основные функции:
1) При помощи воркера раз в сутки получать метаданные и картинку дня [APOD](https://api.nasa.gov/), сохранять в реализованное любым способом бинарное хранилище;
2) Реализовывать Http API сервер: метод получения всех записей альбома и записи за выбранный день;
3) Сервис должен собираться в docker-образ;

**Технологии**: postgreSQL, docker, docker-compose, makefile

**Примечания:**
- Для конфигурирования проекта используйте переменные ENV;
- Сервис должен создать базу данных и необходимую структуру таблиц при запуске;


### `[BACK]` Telegram bot to store files in cloud

#### Description (ENG):

Write a high-availablity telegram bot that will store files in different formats to the user's specified cloud

**Technologies**: Golang, CockroachDB, Grpc-Gateway, Redis, k8s
