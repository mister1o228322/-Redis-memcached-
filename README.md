# Задание 1. Кеширование
Кеширование решает широкий спектр проблем, связанных с производительностью и нагрузкой на инфраструктуру. Вот основные примеры:

Снижение нагрузки на базы данных: Это самая частая задача. Вместо того чтобы выполнять один и тот же сложный SQL-запрос (например, для получения списка последних статей или профиля пользователя) при каждом обращении, результат сохраняется в кеше. Последующие запросы обслуживаются из кеша, что многократно снижает количество операций чтения с диском и нагрузку на процессор базы данных.

Ускорение отрисовки динамических страниц (кэширование фрагментов): Веб-страницы часто содержат блоки, которые генерируются долго, но не меняются для каждого пользователя (например, меню категорий товара или "шапка" сайта). Результат генерации такого фрагмента можно сохранить в кеше и подставлять в страницу, не выполняя тяжелый код каждый раз.

Сохранение результатов вызовов внешних API: Если ваше приложение обращается к внешнему сервису (погода, курс валют, данные из стороннего сервиса), ответ от этого сервиса можно закешировать. Это не только ускоряет работу приложения, но и делает его более устойчивым: если внешний сервис временно недоступен, приложение может отдать данные из кеша.

Управление пользовательскими сессиями: В распределенных системах (когда приложение работает на нескольких серверах) необходимо хранить сессии пользователей в общем хранилище. Memcached и Redis отлично подходят для этой цели, так как хранят данные в памяти и обеспечивают быстрый доступ с любого сервера.

# Задание 2. Memcached
Выполненные действия:
* Обновление списка пакетов:

sudo apt update

* Установка Memcached:

sudo apt install memcached -y

* Проверка статуса службы:

sudo systemctl status memcached

Результат: Memcached успешно установлен и запущен

<img width="1172" height="949" alt="image" src="https://github.com/user-attachments/assets/64b53604-8d1c-4002-90f7-205b8f9acc83" />

<img width="1080" height="274" alt="image" src="https://github.com/user-attachments/assets/edc2c663-31ff-4ec3-a936-b686322e6650" />

<img width="1166" height="185" alt="image" src="https://github.com/user-attachments/assets/7d06a2d8-4eeb-4f79-a9d5-e13c991fa980" />

# Задание 3

Выполненные действия:
* Установка netcat для взаимодействия с Memcached:

sudo apt install netcat-openbsd -y

* Создание ключей с временем жизни 5 секунд:

printf "add key1 0 5 6\r\nvalue1\r\n" | nc 127.0.0.1 11211
printf "add key2 0 5 8\r\nvalue2!!\r\n" | nc 127.0.0.1 11211
printf "add key3 0 5 5\r\nvalue3\r\n" | nc 127.0.0.1 11211
Подтверждение: STORED для каждого ключа

* Первая проверка наличия ключей:

printf "get key1 key2 key3\r\n" | nc 127.0.0.1 11211
Результат: все три ключа отображаются с их значениями

Ожидание 5 секунд

* Вторая проверка:

printf "get key1 key2 key3\r\n" | nc 127.0.0.1 11211
Результат: только END, ключи удалились по истечении TTL

<img width="814" height="252" alt="image" src="https://github.com/user-attachments/assets/5e9081c0-e5a1-4ce8-bfd6-52c1b25574f0" />

<img width="1038" height="630" alt="image" src="https://github.com/user-attachments/assets/4fe9a35a-78eb-43bf-b61d-1aa8d44e5afd" />

<img width="596" height="263" alt="image" src="https://github.com/user-attachments/assets/f1c82340-6b8c-443a-8841-03f31024ac4b" />

# Задание 4

Выполненные действия:

* Установка Redis:

sudo apt update
sudo apt install redis-server -y

* Проверка работы Redis:

sudo systemctl status redis-server

* Вход в интерфейс Redis CLI:

redis-cli

* Создание ключей с различными значениями:


SET user:1 "Иван Петров"
SET user:2 "Мария Смирнова"
SET city:moscow "Москва"
SET counter 100
SET last_login "2026-02-18"
Подтверждение: OK после каждой команды

* Просмотр всех созданных ключей:

KEYS *
Вывод: список всех ключей

* Получение значений ключей:

MGET user:1 user:2 city:moscow counter last_login
Вывод: все значения ключей одной командой

* Выход из Redis:

text
exit

Результат: На скриншоте видно создание ключей и успешное получение всех записанных значений из базы Redis.

<img width="1030" height="637" alt="image" src="https://github.com/user-attachments/assets/db98539c-787b-49a3-812c-dbb096caa1bf" />

<img width="832" height="638" alt="image" src="https://github.com/user-attachments/assets/f9f75d2d-300e-4b19-8481-0c3dc5b98f78" />

<img width="950" height="185" alt="image" src="https://github.com/user-attachments/assets/fbdb13dd-04c8-4e0b-afd8-658b5a0ee2f7" />

<img width="206" height="94" alt="image" src="https://github.com/user-attachments/assets/18a59b4b-3865-4cdd-94ca-36682d20693e" />

<img width="925" height="471" alt="image" src="https://github.com/user-attachments/assets/66a46eb9-f9f8-4f61-9684-d3783b91759d" />









