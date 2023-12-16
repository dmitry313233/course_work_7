AtomicHabits

В 2018 году Джеймс Клир написал книгу «Атомные привычки», которая посвящена приобретению новых полезных привычек и искоренению старых плохих привычек. Данное приложение предназначено для создания напоминаний о нужных привычках и их отправке пользователю через telegram. Приложение реализует механизм CRUD для сущности "Привычка", позволяет регистрировать пользователей и отправлять напоминания в telegram.

Сервис использует PostgreSQL в качестве основной базы данных для проекта, Celery для выполнения различных периодических задач (таких как отслеживание напоминаний, требующих отправки), а также Redis - NoSQL базу данных для обеспечения работы Celery с периодическими задачами.

Для использования приложения следует выполнить ряд инструкций:

Клонировать проект
Проверить наличие и установить при необходимости программы PostgreSQL, Celery и Redis
Установить и активировать виртуальное окружение для проекта
Установить зависимости из файла requirements.txt или pyproject.toml
Создать базу данных в postgres и внести требуемые настройки в файл .env (пример оформления и наполнения такого файла находится в корне проекта и называется .env.sample)
Создать своего телеграм-бота (для этого нужно перейти по ссылке) или использовать уже имеющегося
Записать токен своего бота в файл .env
Провести миграции python manage.py migrate
Создать суперюзера для возможности администрирования при помощи команды python manage.py create_superuser
Запустить сервер python manage.py runserver
Запустить в консоли обработчика задач (worker) и планировщика задач:
    celery -A config worker --loglevel=info
    celery -A config beat --loglevel=info

Для того, чтобы пользователь смог получать уведомления в telegram, он должен начать диалог с созданным ботом через команду /start в соответствующем чате. После этого он может создавать привычки с требуемой периодичностью напоминания и получать уведомления, когда придет время выполнить действие.
