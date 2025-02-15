Это шаблон для решения **первой части** проектной работы. Структура этого файла повторяет структуру заданий. Заполняйте его по мере работы над решением.

# Задание 1. Анализ и планирование

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
 

# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

[Диаграмма контекста](https://www.plantuml.com/plantuml/png/hPLDJnDV5CRtyodkVrPj0dJpNxaYW8aQI0hKTNFRtfH9vWLcxe34c02-68C9ujA5H8qhDqDbjD0N4Zx1kT_8ysGcaxwCqOKhsfbpd-TtxdCENOwq37NikTP_ZjzsuuuIErhlHlTgjL0UB7KTlHEtuaY5xS3NojTBxS2hxRhInvd5I7TSfrLR_N-nZaUFDzPhdeoq2lbHSvLFICTNuT8kz2rBEzfLWZvHtnoR4qffI8cu-qQVpJdTqi2SqhMWAnhJy6uWAiLniUR8RYYzgcNLLHW5VlF-4rrfnv4EF1Kk29ikQCp7tz9F_jkZ1DhuRkFTUnfGGbTuGgbv9SnpjXrnuNSQvswKsAozVSZWNdCbYFsE30yh7fitkV7zp6EA6YgtveY5Uv2b4RyyiwjFBI54mLqvKAsC8ANBHK9zdwl7z2CxGIa0jvHiQtoW2ov8GGIVJDgSCVE9uDeHhCsHUS4br-POq6rPpu2OObXhLQ8z5-hdb71jWfOJ6h7UgNa9steGwMwejZVNyOs-eYlGmROefVGtXg1PoAyHpncLxmODiCuOf5pNiyKSbH-0QzAG1cpwXj8vmet0xmPhAt_0wsU4DrcRMI9_WLBfg7sdhPeOxp004NtWwb5s2WsNYN3P8xalym63Nn_zOynGGpsaApYcXq735g8gh6UMLKpMXlHbr-DbMh3fo-mSKPhFqSIiouxd-F1wnmv3wgCkPq8EOtC4aX8jC61ig8S32CcUOOayNl_cJi0h3XhiniGUpgCuWMQheZ0jkHrAG4CV-NFEWrIAX0PyudN6Dnjs5MXRofqB9PiMBCjUh2AD4BaiMx2oDnF_7L1JVZUbw3G4PqzW6XbpX5iGuATBt3lMaHCIBFcWqQXlsnCWCz3_tZJpoeS1bcN3EfbtOizm8hqvplceYjqUKWfjXkZR0gkusMY0eomZQ9V5VeDk439TJMaiAx-3tuLV)

**Диаграмма компонентов (Components)**

Добавьте диаграмму для каждого из выделенных микросервисов.

**Диаграмма кода (Code)**

Добавьте одну диаграмму или несколько.


# Задание 3. Разработка ER-диаграммы

Добавьте сюда ER-диаграмму. Она должна отражать ключевые сущности системы, их атрибуты и тип связей между ними.


