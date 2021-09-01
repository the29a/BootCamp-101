# Подготавливаем систему к установке Docker

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

# Добавляем GPG ключ репозитория

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

# Добавляем репозиторий

```
echo \
 "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
 $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

# Устанавливаем Docker

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

# Проверяем состояние службы

```
sudo systemctl status docker
```

# Добавляем текущего пользователя в группу docker

```
sudo systemctl status docker
```

