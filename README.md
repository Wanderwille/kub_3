# Домашнее задание к занятию «Запуск приложений в K8S» - Подус Сергей

### Задание 1. Создать Deployment и обеспечить доступ к репликам приложения из другого Pod

1. Создать Deployment приложения, состоящего из двух контейнеров — nginx и multitool. Решить возникшую ошибку.
2. После запуска увеличить количество реплик работающего приложения до 2.
3. Продемонстрировать количество подов до и после масштабирования.
4. Создать Service, который обеспечит доступ до реплик приложений из п.1.
5. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложений из п.1.

------

### Задание 2. Создать Deployment и обеспечить старт основного контейнера при выполнении условий

1. Создать Deployment приложения nginx и обеспечить старт контейнера только после того, как будет запущен сервис этого приложения.
2. Убедиться, что nginx не стартует. В качестве Init-контейнера взять busybox.
3. Создать и запустить Service. Убедиться, что Init запустился.
4. Продемонстрировать состояние пода до и после запуска сервиса.


## Ответ:

### Задание 1 

1. Файл Deployment приложения находится в папке src: 

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1.png)

![Scrin 2](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-2.png)

Ошибка в том, что порт 80 занят, значит в файл нужно добавить порт

```yaml
containers:
      - name: nginx
        image: nginx:1.19.2
      - name: multitool
        image: wbitt/network-multitool 
        env:
          - name: HTTP_PORT
            value: "81"
```
![Scrin 3](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-3.png)


2. Изменяем в конфигурационном файле ```deploy-nginx.yml``` значение ```replicas: 1``` на значение ```replicas: 2``` 

![Scrin 4](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-4.png)

3. 

### Скриншот до:

![Scrin 5](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1.png)

### Скриншот после:

![Scrin 6](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-4.png)

4. Файл Service находится в папке src:

![Scrin 7](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-5.png)

5. Файл Pod находится в папке src:

![Scrin 8](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-6.png)

![Scrin ](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad1-7.png)

### Задание 2 

1. Файл Deployment приложения находится в папке src: 

![Scrin 9](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad2.png)

3. Файл Service находится в папке src:

![Scrin 10](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad2-1.png)

4. 

Скриншот до:

![Scrin 11](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad2.png)

Скриншот после:

![Scrin 12](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube3/zad2-1.png)



