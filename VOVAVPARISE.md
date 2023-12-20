## 1. Установка кластера с одной управляющей и двумя рабочими нодами   

Для установки Docker Swarm кластера выполните следующие шаги:   

На управляющей ноде:   
```sh 
docker swarm init --advertise-addr <IP-адрес-управляющей-ноды>
```

На рабочих нодах:   
```sh
docker swarm join --token <токен> <IP-адрес-управляющей-ноды>:<порт>
```

## 2. Удаление и повторное добавление рабочей ноды в кластер
```sh
--На управляющей ноде выполняем   
docker node rm <ID-рабочей-ноды>   

--После этого повторно добавляем ноду (как указано в первом пункте)   
```
## 3. Создание Docker образа с метаданными узла
Dockerfile    
```sh
FROM python:3.8

-- Установка Flask   
RUN pip install Flask

-- Копирование приложения   
COPY app.py /app/app.py

-- Открываем порт   
EXPOSE 5000

-- Команда для запуска Flask-приложения   
CMD ["python", "/app/app.py"]
```

app.py
```sh
from flask import Flask
import socket

app = Flask(__name__)

@app.route('/')
def hello():
    # Получаем IP-адрес текущего узла
    ip_address = socket.gethostbyname(socket.gethostname())
    return f'Node IP Address: {ip_address}'

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)

```
## 4. Разворачивание сервиса с 3 репликами
```sh
docker service create --replicas 3 --name my-service -p 5000:5000 ваше_имя_образа
```

## 5. Пересборка образа с дополнительной информацией о разработчике
Dockerfile (обновленный)
```
FROM python:3.8

# Установка Flask
RUN pip install Flask

# Копирование приложения
COPY app.py /app/app.py

# Открываем порт
EXPOSE 5000

# Дополнительная информация о разработчике
LABEL maintainer="Ваше Имя <ваш_email>"

# Команда для запуска Flask-приложения
CMD ["python", "/app/app.py"]
```
## 6. Обновление приложения с использованием docker service update
```sh
# Пересоздаем сервис с новой версией образа
docker service update --image ваше_имя_образа:новая_версия my-service
```

