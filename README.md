
# Вступление
Взято с <https://habr.com/ru/post/555768/>

В руководстве описано развёртывание сервера shadowsocks с плагином v2ray на облачном провайдере Heroku. Платформа Heroku позволяет бесплатно разворачивать небольшие веб-приложения, а плагин v2ray позволяет пропускать трафик shadowsocks внутри websocket-соединения, что и позволяет запускать всю конструкцию на Heroku.

В руководстве используется проект готового приложения для Heroku, которое реализует всё необходимое автоматически.

# Шаг 1. Регистрация в сервисе Heroku
Зайти на сайт Heroku, нажать Sign up и заполнить требуемые сведения. Для регистрации нужна только электронная почта.
An email address that can receive verification codes normally (@qq.com, @163.com are not acceptable):
- gmail (Best) 
- Outlook <https://login.live.com/> here.

# Шаг 2. Начало развёртывания
Нажать на эту ссылку:
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/meteoviktor/meteoviktorssoks/tree/main)

# Шаг 3. Конфигурирование
В появившейся форме заменить следующие поля:
- "App Name" и AppName вписать уникальное имя одинаковое в обоих полях. Это имя станет частью доменного имени <appname>.herokuapp.com, по которому станет доступен сервис.
- Задать свой пароль подлиннее и понадёжнее - его не придётся вводить вручную.
- Сменить путь QR на какое-нибудь трудноугадываемое значение.
  
# Шаг 4. Запуск
Нажать Deploy app.
После завершения сборки и запуска QR-код с конфигурацией для мобильных устройств будет доступен по адресу
https://<APPNAME>.herokuapp.com/<QR>/vpn.png

строка с конфигурацией в виде URL доступна по адресу (косая черта на конце обязательна):
https://<APPNAME>.herokuapp.com/<QR>/
где <APPNAME> - выбранное имя, <QR> путь к QR-коду.

# Шаг 5. Настройка мобильного клиента на примере Android
- Установить на устройство [shadowsocks](https://play.google.com/store/apps/details?id=com.github.shadowsocks) и [плагин v2ray к нему](https://play.google.com/store/apps/details?id=com.github.shadowsocks.plugin.v2ray). 
- Запустить приложение и добавьте новый профиль кнопкой с плюсом в правом верхнем углу.
- Выбрать сканирование QR-кода.
- Выбрать созданный профиль касанием.
- Запустить соединение нажатием на круглую кнопку внизу.
- После скачивания qr кода зайти в «Settings» найти там пункт «Config Vars», нажать «Reveal Config Vars», и поменять «QR_Path» на значение «no». После чего доступ к qr коду по ссылке станет недоступен.

# Ограничения для приложений, запущенных на Heroku:
- Временная квота работы приложений при бесплатном уровне использования составляет 550 часов в месяц.
- Контейнер приложения переходит в спящий режим после 30 минут отсутствия запросов к нему. С одной стороны это доставляет неудобства в виде задержек ответа до полминуты после перерыва в активности. С другой стороны, это экономит отведённую временную квоту.
- Квота на передачу данных по сети равна 2 ТБ в месяц. То есть в случае с прокси это даёт чуть меньше 1 ТБ трафика в месяц.
- Heroku может запретили развёртывание этого шаблона. Тогда попытка это сделать закончится ошибкой "We couldn't deploy your app because the source code violates the Salesforce Acceptable Use and External-Facing Services Policy". Решить эту проблему можно развёртыванием из своей копии git-репозитория с изменённым именем.
