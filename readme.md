# Avito Bot

Скрипт на python который в соответсвие с настройками каждые несколько секундо проверяет заданные разделы сайта на наличие новых товаров. В случае их обнаружения он отправляет сообщение продавцу. Если сообщение отправить нельзя он бот отправляет сообщение в telegram через alarmer bot. После каждого обновления бот проверяет наличие олтветов на все отправленные ранее сообщения и в случае их обнаружения также шлет уведомления через alarmer bot.

### Настройка

1. Качаем firefix
2. Качаем Linux
3. Настраиваем файл config.conf
    1. Каждый блок состоит из 7 параметров, все названия должны быть уникальными
    2. `url` - ссылка на раздел для поиска
    3. `max_cost` - максиамльная  цена товара при которой присылать уведомление
    4. `min_cost` - минимальная  цена товара при которой присылать уведомление
    5. `mes_cost` - сумма, до которой писать продавцу с прозьбой снизить цену
    6. `model` - модель телефона
    7. `params` - параметры телефона
    8. `message_text` - Текст сообщения, который бот пишет
     продавцу если цена больше `max_cost` и меньше `mes_cost` 
4. Настраиваем бота в файле config.conf в разделе SETTING:
    1. `avito_password` - пароль от аккаунта в авито
    2. `avito_login` - логин от аккаунта в авито
    3. `alamer_key2` - ключь для отправки уведомления в telegram bot, получить можно тут t.me/alarmer_bot: 
5. Запускаем`./bot -c` для очистки кэша
6. Запускаем`./bot -s` для сохранения тякущих товаров чтобы не начать спамить уведомлениями при запуске и не словить фрод
7. Запускаем`./bot -m` для запуска в режиме мониторинга (напр на сервере),без авторизации и отправки сообщений (не требует браузера).
8. Запускаем`./bot` для запуска в обычном режиме работы, требует наличие браузера и **geckodriver** на пути по адресу `/usr/local/bin/geckodriver`.

### Фичи

+ Потдержка авторизации на сайте через подмену cookies
+ Асинхронный парсинг разделов с товарами
+ Вывод капчи при появлении необходимости ее обхода
+ Локальная BD которая сохраняет состояние парсера при перезагрузке
+ Удобная настройка через файл config.conf
+ Использование Alamer Bot в telegram для отправки уведомлений
+ Использование драйверов selenium для управления браузером для обхода фрода avito и рассылки сообщений
+ Проект собран Docker ом

### Технологии

* Selenium
* BeautifulSoup
* Aiohttp и asyncio
* SQL Lite 
* Docker 
* Peewee ORM

#### Фаловая архитектура

dist/bot - собранный бот
bot/bot - код бота
bot/parser - класс для инкапсуляции всех функций работы с сайтом
bot/model - классы моделек для работы с DB
