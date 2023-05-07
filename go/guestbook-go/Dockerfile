FROM golang:1.10.0 # Определение базового образа Golang версии 1.10.0

RUN go get github.com/codegangsta/negroni \ # Установка зависимостей приложения
           github.com/gorilla/mux \
           github.com/xyproto/simpleredis
           
WORKDIR /app # Установка рабочей директории приложения
ADD ./main.go . # Добавление исходного кода приложения в директорию приложения
RUN CGO_ENABLED=0 GOOS=linux go build -o main . # Компиляция приложения в бинарный файл
FROM scratch # Определение нового образа на основе scratch, для уменьшения размера образа
WORKDIR /app # Установка рабочей директории приложения
COPY --from=0 /app/main . # Копирование скомпилированного бинарного файла из предыдущего образа в новый образ

COPY ./public/index.html public/index.html # Копирование файлов статических ресурсов в директорию public приложения
COPY ./public/script.js public/script.js
COPY ./public/style.css public/style.css

CMD ["/app/main"] # Задание команды, которая будет выполнена при запуске контейнера
EXPOSE 3001 # Открытие порта 3001 на контейнере

