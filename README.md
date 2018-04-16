# Chat Wars telethon bot 
Скрипт для автоматизации игры в Chat Wars 

## Установка:
1. Для начала идём на https://my.telegram.org и авторизуемся. Там создаём новое приложение. От него нам нужен api id  и hash.

2. Для работы скрипта нужен терминал/консоль, python3, и 2 пакета из файла requirements.txt - pytz и telethon. 
Если этот пункт не понятен, он будет разжёван поподробнее отдельно.

3. Копируем файлики себе командой: git clone https://github.com/goodronoid/CWtelethonbot.git

4. В файле username_tg_connect.json вбиваем свои данные полученные в п. 1.
Все значения должны быть в кавычках, кроме номера API_ID.

5. Сам файл username_tg_connect.json переименовываем. Вместо "username" пишем свой юзернейм. Должно получиться что-то типа koltsov_tg_connect.json.

6. Всё готово для запуска. Запускаем командой: 
python3 cw_telethonbot.py -u username -a admin_username -o order_username1,order_username2 -n name_of_group

Объясню:
-u или --username - юзернейм. Всё тот же что и в пунктах 4 и 5.
Этот аргумент обязателен. Остальные можно и не указывать.
-a или --admin - юзернейм, который будет изменять настройки боту. Если у тебя всего один акк - указывай EchoBot. И будешь сам себе команды отправлять через него. Если у тебя бездонная ботоферма - указывай свою основу.
-o или --order - юзернеймы тех, кто присылает пины на атаку. Указываются через запятую без пробелов.
-n или --group_name - имя чятика, куда бот будет отвечать на изменение настроек админом и куда будет скидывать ссылки /fight_. Если не указано - всё это будет слать в ЛС админу.

7. При первом запуске попросит авторизоваться в Телеграме. После успешной авторизации создаст в папочке файл username.session. Этот файлик будет использоваться для авторизации и его можно переносить между устройствами.

8. При первом запуске создаст файл настроек username.cfg. Запишет туда значения по умолчанию. При изменении настроек админом - записывает их в этот файл. При следующих запусках будет брать настройки из него.

#### Важные замечания:
- при потере инета скрипт реконнектится сам с интервалом 3 секунды. По этой причине его не остановить нажатием Ctrl+C. Юзай Ctrl+Z.

### Функционал бота:
- стройка/ремонт если есть голда в казне 
    - по дефолту включено /repair_wall
    - вкл/выкл командами #enable_build #disable_build
    - цель указываем командой #build_target repair_wall
- стопим грабителей корованов 
    - вкл/выкл командами #enable_corovan, #disable_corovan. 
    - по умолчанию включено
- арена 
    - вкл/выкл командами #enable_arena, #disable_arena
    - по умолчанию включено
- квесты 
    - Лес (включён по дефолту): #enable_les, #disable_les; 
    - Пещера: #enable_peshera, #disable_peshera; 
    - Побережье: #enable_more, #disable_more; 
- помощь с мобами на квестах 
    - смотрит все чаты в которых сидит на наличие сообщений с "/fight"
    - запрос помощи у отряда (форвардит в РКБ)
    - запрос помощи у админа или в группе (см. п. 6, аргумент --group_name)
    - вкл/выкл командами #enable_quest_fight, #disable_quest_fight
- атака по пинам
    - вкл/выкл командами #enable_order, #disable_order
- выход с арены и включение защиты перед битвой
    - вкл/выкл командами #enable_auto_def, #disable_auto_def
- донат перед битвой
    - вкл/выкл командами #enable_donate, #disable_donate
- лвлапе автовыбор Атака+1 или Защита+1
    - ничего не качать (по умолчанию) - #lvl_off
    - выбирать Атака+1 - #lvl_atk
    - выбирать Защита+1 - #lvl_def
- если пригласили в термы - автостоп бота и форвард сообщения с капчей админу бота
- вкл/выкл бота командами #enable_bot #disable_bot
- текущее состояние настроек можно узнать командой #status
- справку по командам можно получить, отправив #help

### Если у тебя Андроид

1. Ставим Termux из маркета.
2. Запускаем.
3. Устанавливаем git (инструмент работы с репозиториями): apt install git
4. Вводим команду git clone https://github.com/goodronoid/CWtelethonbot.git
5. Установим две библиотеки для работы скрипта: pip3 install -r ./CWtelethonbot/pip3.txt
6. Редактируем файл настроек подключения к Телеграму:
- nano ./CWtelethonbot/username_tg_connect.json
- значения по умолчанию меняем на свои: api и hash полученные на https://my.telegram.org, номер телефона, юзернейм
- закрываем файл нажатием VolumeDown+X
- на вопрос "Сохранить?" жмём Y
- на вопрос "Под каким именем?" пишем username_tg_connect.json, где вместо "username" пишем свой юзернейм
- жмём Enter
6. Создадим файлик для быстрого старта бота: echo python ./CWteletonbot/cw_telethonbot.py -a admin_username -o order_username1,order_username2 -n name_of_group -u username > username_startbot
В этой команде заменяем всё как написано в пункте 6 основной инструкции по установке.
7. Запускаем бота командой ". username_startbot"