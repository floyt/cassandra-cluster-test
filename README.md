# README: Cassandra Cluster Deployment with Docker Compose

## Цель
Развернуть кластер из трех узлов Cassandra с помощью Docker Compose. Каждый узел должен быть доступен в локальной сети по отдельному IP-адресу.

---

## Шаги настройки

### 1. **Подготовка окружения на машине А (192.168.1.197)**

1. Убедитесь, что установлен Docker и Docker Compose:
    ```bash
    sudo apt update
    sudo apt install docker.io docker-compose -y
    ```
2. Проверьте версии Docker:
    ```bash
    docker --version
    docker-compose --version
    ```
3. Создайте папку для проекта и переместитесь в неё:
    ```bash
    mkdir cassandra-cluster && cd cassandra-cluster
    ```
4. Создайте файл `docker-compose.yml` с содержимым из данного проекта.

### 2. **Запуск кластера Cassandra**

1. Поднимите кластер:
    ```bash
    docker-compose up -d
    ```
2. Проверьте статус контейнеров:
    ```bash
    docker ps
    ```
   Вы должны увидеть три контейнера (cassandra1, cassandra2, cassandra3), работающих на IP-адресах `192.168.1.200`, `192.168.1.201`, и `192.168.1.202`.

---

## Подключение к кластеру с машины Б (192.168.1.198)

1. Убедитесь, что на машине Б установлен `cqlsh`. Если его нет, установите Cassandra tools:
    ```bash
    sudo apt install cassandra-tools -y
    ```
2. Подключитесь к каждому узлу через `cqlsh`:
    ```bash
    cqlsh 192.168.1.200
    cqlsh 192.168.1.201
    cqlsh 192.168.1.202
    ```
---

## Проверка результатов
![cassandra1](https://github.com/user-attachments/assets/f0ada3ec-32ac-4812-86b8-57f8bda67735)
![cassandra2](https://github.com/user-attachments/assets/c50c681d-c7ae-4b3d-a238-504bdb428404)
![cassandra3](https://github.com/user-attachments/assets/0b5a2ed1-9799-44cd-b468-221553db840f)


---

## Завершение работы

1. Остановите кластер:
    ```bash
    docker-compose down
    ```
2. Убедитесь, что все контейнеры остановлены:
    ```bash
    docker ps -a
    ```

---

## Примечания

- Используйте одинаковую версию Docker и Docker Compose на всех машинах для исключения ошибок совместимости.
- Убедитесь, что выбранный диапазон IP-адресов (`192.168.1.200-202`) не конфликтует с другими устройствами в сети.

