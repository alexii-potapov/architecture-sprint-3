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

Добавьте сюда диаграмму контекста в модели C4.

Устройства
Дом

Юзер

Основной сервер

Адмнистратор

Монтажник

[Диаграмма контекста](https://www.plantuml.com/plantuml/png/fPFBQXH158Rt_HJbRCo0oMnSkGe6mOM1e77TLARBJ4DrrL1TdMGG8L4m2uMe289uqRXqqqJ7J2wPWJp1wJVohqenzop4JSzKzVc_S_bFB-UM6rjaChgHggOi4i5QrhRpEus6uTjBcwbj5Hj5BanJAokKNMhghD6MN3dDOcuJcMuqLculhhchnwiF6XdFhJ2uYbUSOiSkjHtz9YiKf1aGpBO4UwAbrDkfscGoLO9nbR29rwd9yKypf6PIDxcK7J26DKxZ8vjQAHXzfrwrLpsdBfrJoIv_qc7rbWPqLhsY4qQ_gK_dbsTHj2PChbLyRySkD8lSwaoOMwn6NwcFqDTqZDyZAZq7vvfxzuxEg0G1DzIjNhBg1L9S8F0NzGEPobezUjH1_rbyLnSguQQpaF5KnPZVrbMABzMULntvvmd3iLljueYdppFP0R8CyBf40D92qwCkBbq4hW7miQWLqRrQ_Md46BkgOC4AAJ9XJSTHtrC9yGN60BblooVeUamFKbOVapg_uumhlkaCSVeVSygWGHZN-B0EG9sY9M9Bf4qHkmqoMdhSltG5sBDeEC_LOLbpCM46OmRp94kLI_e6Be7dua8cLtJVptqkQsGE1CvWs3l9pejsMni_eKy8k02lf3zUVUgfdt7sUrFjkxivJTRg3EsD-iipRcpSql30TuWb6rlUsVPoeN9jWiT0xmzp7qxRN1tCD624v7v1lbq5NpUAK6NqKCYnBsPYnTp7SmhLiLyr94F9euhSai39AS3_huO71Xlcyk30IEmAdEk1nuHDcTt-ZyxR8C72J-v56THZmnXvye5Atq-_scCqc9mGdSnE29hxw-jh0JdJZhVhsYdj1Wz7a6MXaYAJVm40)

[Диаграмма контекста](https://www.plantuml.com/plantuml/png/fPFFQzHG4CVl-IkUkTW5sxruybGitYmKnND8a-TkuFrOafUsYmXT1JqeL4KGH2tgqKkihkwFDWlz2-RzHywRNTOaneC8ItRVotm_C_ETsUtCXAd9fV2k92eIUSnPtvX1TgFRJSF3hLvY-lb-dl4qqifmPROYBRi34IgdsSnCB9BzxixrpJrtTM_tTbU6cU4fNWKxJd5ajWQEVfNb2gKI4SpqERklXT27YUenaIZEGXMpskiapV2NPfYQ2Hs5GWoHiQwnYVTCOWHdy14cTcGVmHZEeM2NN-2JVGaBcDjdC6Nm7KeulvnxtXvFCws2MqTc8yepeoLFhp4VJg74qEVm4x_Fe20EddttxXNCeK02ti3OFc7sCQQumC1lKAx8KFWTx-uG-vV1JPshE4o76p9CL83-7InJVB0ZKftHSyhmEBR7UCIdozFe0BCiy7M10PWMDHCOuwMBm6i4K2pMYj4Jl_F0OumjAzWmN739JJfSKhz2QOyPB50qWm9RB8WszLcd8dAJ3cIemfuRXLD-RYc0A6XCpQOJAg56Y_a1Jo8UkDr9jI3Sl_I3i8ShGsbMcSHT3VeQgoIMcq1bikJVQrUGVOhW6KmOVf1BCyFPh8Uok-wmjQALaPKj2MEPA8T_WQcmD1UtB9hwBsbuhQprX9s0gkmqs5a-6EYKp7w70HV8A-07gMT4VOzdMhvbMor--Hs6JddU7Iug2rtRWDFwuEq9cbQngdIGXlv_nqUyTNjjEEpijzQLrzeROLOJ-7D1tv9d974xMVUxMAahLZIMw0qKr5DfHot_Zh-PrEobIMtngRg8srp5kHI_0000)

# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

Добавьте диаграмму.

**Диаграмма компонентов (Components)**

Добавьте диаграмму для каждого из выделенных микросервисов.

**Диаграмма кода (Code)**

Добавьте одну диаграмму или несколько.

# Задание 3. Разработка ER-диаграммы

Добавьте сюда ER-диаграмму. Она должна отражать ключевые сущности системы, их атрибуты и тип связей между ними.


