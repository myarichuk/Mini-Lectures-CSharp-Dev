# **Docker: Что это, зачем он нужен и как работает?**  

## **Что такое Docker?**  
**Docker** – это библиотека (и инфраструктура), которая помогает запускать программы в **изолированной среде**, называемой **контейнером**.  

Грубо говоря, **контейнер** – это как **"легковесная виртуальная машина"**, но без лишнего мусора. В отличие от полноценных виртуальных машин (VM), **контейнеры используют одну и ту же операционную систему**, а не создают новую копию для каждой программы.  

**Простыми словами:**  
- Контейнер – это **упакованная среда**, которая содержит всё, что нужно для работы приложения.  
- Можно запустить один и тот же контейнер **на любом сервере** (Windows, Mac, Linux, облако) без "оно у меня работает, а у тебя нет".  
- Всё работает одинаково **и в разработке, и в продакшене**.  

---

##  **А нафиг он нужен?**  

### 1. **"Оно у меня работает, а у тебя нет!"**  
Docker **изолирует приложение**, поэтому у всех оно **работает одинаково**, независимо от операционной системы.  

* **Без Docker:**  
> – У меня ошибка в коде! У меня работает, а у тебя нет!  
> – У меня другая версия Python/PHP/Node.  

* **С Docker-ом:**  
> – Запусти контейнер – и всё будет работать **точно так же**, как у меня.  

---

### 2. **Быстрое развертывание среды (продвинутая тема)**  
Если вы делаете сайт, который использует **Node.js, PHP, MySQL, Redis**, то без Docker придётся **устанавливать всё вручную** и настраивать.  

**С Docker-ом** это выглядит так:  
```sh
docker-compose up -d
```  
Всё запускается за 10 секунд, и можно сразу работать!

### 3. Безопасность и Чистота Системы

Docker не засоряет вашу ОС, потому что работает в контейнерах. После работы можно просто удалить контейнер, и он не оставит мусора в системе.

### 4. Гибкость и Масштабируемость

Docker отлично работает в облаке и позволяет легко запускать приложения на любых серверах.
> – Например, ваш сайт можно развернуть на локальной машине, на сервере в офисе и в облаке – и всё будет работать одинаково

### Главные понятия в Docker

1. Образ (Image) – это как "ISO-файл" или "установочный архив" вашего приложения.
2. Контейнер (Container) – это как "запущенная программа", созданная на основе образа.
3. Dockerfile – это "рецепт", который описывает, как создать образ.
4. Docker Hub – это магазин образов, где можно взять готовые образы (например, MySQL, Redis, Nginx).
5️. Docker Compose – это инструмент, который помогает запускать несколько контейнеров сразу (например, сайт + база данных).

## Как установить?

### На Маке
Самый простой способ это через Homebrew
```terminal
brew install --cask docker
```

### Windows
Неплохие инструкции [здесь](https://docs.docker.com/desktop/setup/install/windows-install/)

## Практические примеры для тренировки

### 1. Запуск веб-сервера Nginx

Запустим Nginx без установки на локальный компьютер.

```terminal
docker run -d -p 8080:80 nginx
```
Затем открываем в браузере: http://localhost:8080  

Что здесь происходит?

> - docker run – запустить контейнер
> - -d – фоновый режим
> - -p 8080:80 – перенаправляем 8080 → 80 (порт Nginx)
> - nginx – скачиваем образ Nginx и запускаем его 

### 2. Запуск Python-скрипта в контейнере

Допустим, у нас есть Python-скрипт app.py:
```python
print("Привет из Docker!")
```

Создаём Dockerfile: (файл который так и называется)

FROM python:3.10
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]

Собираем и запускаем контейнер:

```terminal
docker build -t my-python-app .
docker run my-python-app
```

В терминале должно появится: "Привет из Docker!"

### Полезные команды (терминал)

| Команда                      | Описание                           |
|------------------------------|-----------------------------------|
| `docker ps`                  | Показать запущенные контейнеры    |
| `docker images`              | Показать загруженные образы      |
| `docker stop <container_id>` | Остановить контейнер             |
| `docker rm <container_id>`   | Удалить контейнер                |
| `docker rmi <image_id>`      | Удалить образ                    |
| `docker-compose up -d`       | Запустить проект с Docker Compose |
