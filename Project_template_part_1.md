# Решение первой части проектной работы

## Задание 1. Анализ и планирование

Чтобы составить документ с описанием текущей архитектуры приложения, можно часть информации взять из описания компании условия задания. Это нормально.

### 1. Описание функциональности монолитного приложения

**Управление отоплением:**

- Пользователи могут удаленно выключать /выключать реле на отопительном приборе
- Система поддерживает только специальные реле
- Для настройки требуется выезд специалиста

**Мониторинг температуры:**

- Пользователи могут просматриватьтекущее значение датчика температуры через web
- Система поддерживает только специальные датчики
- Для настройки требуется выезд специалиста

### 2. Анализ архитектуры монолитного приложения

Перечислите здесь основные особенности текущего приложения:

- Язык программирования: Java
- База данных: PostgreSQL
- Архитектура: Монолитная, все компоненты системы (обработка запросов, бизнес-логика, работа с данными) находятся в - рамках одного приложения.
- Взаимодействие: Синхронное, запросы обрабатываются последовательно. RESTзапросы
- Масштабируемость: Ограничена, так как монолит сложно масштабировать по частям.
- Развёртывание: Требует остановки всего приложения.

### 3. Определение доменов и границы контекстов

Опишите здесь домены, которые вы выделили.

Взаимодействие с устройствами в доме
   Получение данных
   Отправка команд

Управление и авторизация пользователей
   Регистрация пользователей
   Авторизованный доступ  к своим устройствам

Административный доступ
   Управление учетными запиясми пользователей
   Добавление устройств пользователя
   Мониторинг

### **4. Проблемы монолитного решения**

- Нет возможности маштабировать приложение. При большом числе устройств система не выдержит нагрузки
- Изменения в одной части будут аффектить другие
- Для выпуска новой версии приходится останавливать сервис целиком
- Сбой в одном из элементов, остановит сервис

### 5. Визуализация контекста системы — диаграмма С4

[Диаграмма контекста](https://www.plantuml.com/plantuml/png/fPFBQXH158Rt_HJbRCo0oMnSkGe6mOM1e77TLARBJ4DrrL1TdMGG8L4m2uMe289uqRXqqqJ7J2wPWJp1wJVohqenzop4JSzKzVc_S_bFB-UM6rjaChgHggOi4i5QrhRpEus6uTjBcwbj5Hj5BanJAokKNMhghD6MN3dDOcuJcMuqLculhhchnwiF6XdFhJ2uYbUSOiSkjHtz9YiKf1aGpBO4UwAbrDkfscGoLO9nbR29rwd9yKypf6PIDxcK7J26DKxZ8vjQAHXzfrwrLpsdBfrJoIv_qc7rbWPqLhsY4qQ_gK_dbsTHj2PChbLyRySkD8lSwaoOMwn6NwcFqDTqZDyZAZq7vvfxzuxEg0G1DzIjNhBg1L9S8F0NzGEPobezUjH1_rbyLnSguQQpaF5KnPZVrbMABzMULntvvmd3iLljueYdppFP0R8CyBf40D92qwCkBbq4hW7miQWLqRrQ_Md46BkgOC4AAJ9XJSTHtrC9yGN60BblooVeUamFKbOVapg_uumhlkaCSVeVSygWGHZN-B0EG9sY9M9Bf4qHkmqoMdhSltG5sBDeEC_LOLbpCM46OmRp94kLI_e6Be7dua8cLtJVptqkQsGE1CvWs3l9pejsMni_eKy8k02lf3zUVUgfdt7sUrFjkxivJTRg3EsD-iipRcpSql30TuWb6rlUsVPoeN9jWiT0xmzp7qxRN1tCD624v7v1lbq5NpUAK6NqKCYnBsPYnTp7SmhLiLyr94F9euhSai39AS3_huO71Xlcyk30IEmAdEk1nuHDcTt-ZyxR8C72J-v56THZmnXvye5Atq-_scCqc9mGdSnE29hxw-jh0JdJZhVhsYdj1Wz7a6MXaYAJVm40)

## Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

[Диаграмма контейнеров](https://www.plantuml.com/plantuml/png/hPLDJnDV5CRtyodkVrPj0dJpNxaYW8aQI0hKTNFRtfH9vWLcxe34c02-68C9ujA5H8qhDqDbjD0N4Zx1kT_8ysGcaxwCqOKhsfbpd-TtxdCENOwq37NikTP_ZjzsuuuIErhlHlTgjL0UB7KTlHEtuaY5xS3NojTBxS2hxRhInvd5I7TSfrLR_N-nZaUFDzPhdeoq2lbHSvLFICTNuT8kz2rBEzfLWZvHtnoR4qffI8cu-qQVpJdTqi2SqhMWAnhJy6uWAiLniUR8RYYzgcNLLHW5VlF-4rrfnv4EF1Kk29ikQCp7tz9F_jkZ1DhuRkFTUnfGGbTuGgbv9SnpjXrnuNSQvswKsAozVSZWNdCbYFsE30yh7fitkV7zp6EA6YgtveY5Uv2b4RyyiwjFBI54mLqvKAsC8ANBHK9zdwl7z2CxGIa0jvHiQtoW2ov8GGIVJDgSCVE9uDeHhCsHUS4br-POq6rPpu2OObXhLQ8z5-hdb71jWfOJ6h7UgNa9steGwMwejZVNyOs-eYlGmROefVGtXg1PoAyHpncLxmODiCuOf5pNiyKSbH-0QzAG1cpwXj8vmet0xmPhAt_0wsU4DrcRMI9_WLBfg7sdhPeOxp004NtWwb5s2WsNYN3P8xalym63Nn_zOynGGpsaApYcXq735g8gh6UMLKpMXlHbr-DbMh3fo-mSKPhFqSIiouxd-F1wnmv3wgCkPq8EOtC4aX8jC61ig8S32CcUOOayNl_cJi0h3XhiniGUpgCuWMQheZ0jkHrAG4CV-NFEWrIAX0PyudN6Dnjs5MXRofqB9PiMBCjUh2AD4BaiMx2oDnF_7L1JVZUbw3G4PqzW6XbpX5iGuATBt3lMaHCIBFcWqQXlsnCWCz3_tZJpoeS1bcN3EfbtOizm8hqvplceYjqUKWfjXkZR0gkusMY0eomZQ9V5VeDk439TJMaiAx-3tuLV)

**Диаграмма компонентов (Components)**

[Диаграмма контекста](https://www.plantuml.com/plantuml/png/jLR1Rjj64BtpAxOwoK0JNNhgARMTrcxZmhOKv2YifBL4cEIgvCgkKGI87QH5uG16UodGGuEqwAaNnOqGEPPa85ym_AE-0LTUaQ1az11TH2vdtinxEpEx3n8ZOpC80-yJFse7WuuIFMFwoUUrMYoFxtTzqnkq1ecAspeoAZBtspgizGCPiS-zn7G2lrNR-EpUBYyztdbK2sLYL8obveOE-pfYdpxZUyOtWHBqciRfQNf68vhGK7puX_vCVw4RkaxFwKhGMvhHvCErgDvw9sBJbzrOXckUv-sgED5Hy-7tfYexeHzzAYfVyB-Vc5WQ7LUmG7_HJVgCXdH9ruWofJ6DH7fA8onUSd0EKLaJdhUk1r57nYVL98G8pPu6KG3K-KriyPl5cz3KfGVV7pmXn48klZOmtDODjgS_m6wUmNjmfB40mHaeFaz_ccS4B1XC6JXzKLdpdkR8jGU9qQ6A0VSuKHcjNq5d2AyHqqf_5EbppWku_zBCPaP387dr4sn1sBnb5qe_QWBbI37U1ZOore78h9WBa-5LcAcuAlj-zvXrtTqMNqcZZkL9HQmLZ7h-4IkrizTeYFLO7sOfRc5rPo_JWDxGXBbcFC4IhsDi0zBcxOSyCxhY9uWqv6ykYDtuwh5g9RxXE4zKIzJnoD3xIhODFw2IXe0uo-qj52ZawdG0NbFs-rPJiHlh0pzGg0JUJf4BBGUcnnhWpwq2kMZ7dT7iPq05N6V5oI9AqNcpbRadtmKmi5wezlKAl-h4T6DLttl4R_GtbnCN3kYwmg7HlB1UqZlyGqbkBAuFkh9wyczV1PQH2uYCtDSSZnAhfyiaxQWZlwsigflyebRgQkqFOa0vZo_vjQXNYLpMcpEpldVgbPN7PNe1WSQsIrWfD6L99IwHCxs0c4wj0ejSLlIgsEWS_uPBasV1_uhffEUehXsohUHMU5XlmAhulL2KbUMMUIBEijZkX_BWKEBZD_mlDW9C9-vukx2guK5e2ixCcBlVpVxqd3LTNLRjR5IvGjcE41Vjx-k8WrRWNLPbiMehFvjs-_OnNrrVowCiwrVfCvm-azmm5ZHBpqesggI5gpWDGnbrx62rpwMnIew5zzd8HjotWgQbnS7ZJ9Hq89eXqbd5VQjHz8jxigEZhaPNh9uRzan28lJEcboKaUPDAYtxUNpw3Uutx9EUvdIqmxfJMIi7i4MrMfZqVAaqCvR6Gji3oMryQIFQsSXrcbKaJftiH4m6eN9vEfXRagz1xuKL4tXtOZw9-RXosbcohbxACimnByrimPyPbwYtGYuUauDMu2Uz4i3YXX9twij2aLuAAmAdUmsJdscqo5RCOUqbmWwQ9PUofLS13iJmK6RAuGKJepVmcRBAY5cSVZQYKwKuZXPl87nF4_RsWleMVFTY27Vfic0V8-kjHcEtZhGveA-DYrNSo5mlrUuebaK-36rlnmxyTzXERTOuQuftfeN47gYem_Vr_m00)

**Диаграмма кода (Code)**

Регистарция устройства используя логин и пароль пользователя, генерация и выдача идентификатора системой
Приём данных телеметрии от устройства через Broker HiveMQ
Отправка команды от пользователя на устройство через промежуочный Broker Kakfka и конечном итоге на Broker HiveMQ

## Задание 3. Разработка ER-диаграммы

[ER-диаграмма](https://www.plantuml.com/plantuml/png/bP9FQZen5CVtESLZbZ-O2mmYBdwKGZT2wLg22Sp0P1pono9QKBkqTt3H2mn5MwNMNY6vKL-csZ5O5rtvyhxFyFdaJKTfAhKHEG01mWkTwH54TcdtzjqzsJVyVR6LczkrFqT05TmfBc5C0FuPh7ePIy2OZ46hrRrfjx4VnyUme88dCAIodrBfcrpGB0yw9LNgVY1PBwKg3PA-v5HprgCw0OQLpWGd3wI1VBOx--4MTWjsXPoxckvMeC_rGF1ln1IhYuXdU9GnoPNwwGMIMQ7nWYky8AHmCpTtKmJO-WgVQr-3_EV3h7-WOBx-0uSUbKqZqBW0iRGL8bJu86iF0-xnZAeweUfIIGNNnpsMn-CbmaOW80Z-6ae4qP3c9inCoNxTBQa_hiaaZWVZarKcgBZnSbul8armcAojwZ4tG-KLZatjgztuuJfh9aF_y6Qmd-4xkaL4I8SNp8Zy2m00)

**Хранение данных устройств пользователя в MongoDB**

```javascript
{
  "_id": ObjectId("64f8e4b7e4b0a1a2b3c4d5e6"), // Уникальный идентификатор пользователя
  "userId": "f3f2e850-b5d4-11ef-ac7e-96584d5248b2"  
  "smart_homes": [
    {
      "home_id": ObjectId("64f8e4b7e4b0a1a2b3c4d5e7"), // Уникальный идентификатор умного дома
      "name": "Мой дом",
      "address": "Малиновая 10",
      "devices": [
        {
          "device_id": ObjectId("64f8e4b7e4b0a1a2b3c4d5e8"), // Уникальный идентификатор устройства
          "name": "Датчик темепратуры в зале",
          "type": "Sensor",
          "parameters": [
            {
              "parameter_name": "temperature",
              "parameter_value": "22.5",
              "updated_at": ISODate("2023-10-01T12:05:00Z")
            }
          ]
        },
        {
          "device_id": ObjectId("64f8e4b7e4b0a1a2b3c4d5e9"),
          "name": "Свет на кухне",
          "type": "light",
          "parameters": [
            {
              "parameter_name": "state",
              "parameter_value": "ON",
              "updated_at": ISODate("2023-10-01T12:10:00Z")
            }
          ]
        }
      ]
    }
  ]
}
```
