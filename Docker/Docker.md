## Подготавливаем систему к установке Docker

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

## Добавляем GPG ключ репозитория

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## Добавляем репозиторий

```
echo \
 "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
 $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Устанавливаем Docker

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Проверяем состояние службы

```
sudo systemctl status docker
```

## Добавляем текущего пользователя в группу docker

```
sudo systemctl status docker
```

## Запускаем тестовый контейнер
```
docker run hello-world
```

## Основные комманды

Показать список образов:   
```
docker images
```

Показать список запущенных контейнеров:   

```
docker ps
```

Показать список контейреров, которые были запущены на текущий момент и в прошлом:
```
docker ps -a
```

Поиск образа необходимым ПО (например, Apache):
```
docker search apache
```

Скачать образ без запуска
```
docker pull tomcat
```

Запустить контейнер из образа:
```
docker run -it -p 1234:80 apache
```

Где ```-it``` - интерактивный режим, ```-p``` указание на то, что будут перенаправлены порты, т.е порт 1234 будет перенаправлять на 80.   

```
docker run -d -p 8888:80 apche
```
Принцип тот же, с разницей во флаге ```-d```, указывающий на запуск контейнера в фоновом режиме.   


