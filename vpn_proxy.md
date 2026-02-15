# VPN

- [Vless / XHTTP / 3x-ui](#vless--xhttp--3x-ui)
  - [Установка 3x-ui](#установка-3x-ui)
  - [Установка сертификата](#установка-сертификата)
  - [Создание подключения. Простой способ. XHTTP Vless Reality](#создание-подключения-простой-способ-xhttp-vless-reality)

## Vless / XHTTP / 3x-ui

### Установка 3x-ui

`curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh | sudo bash`

Сохраняем креды, URL и порт.

x-ui control menu usages (subcommands):

|  x-ui              - Admin Management Script          |  
│  x-ui start        - Start                            │  
│  x-ui stop         - Stop                             │  
│  x-ui restart      - Restart                          │  
│  x-ui status       - Current Status                   │  
│  x-ui settings     - Current Settings                 │  
│  x-ui enable       - Enable Autostart on OS Startup   │  
│  x-ui disable      - Disable Autostart on OS Startup  │  
│  x-ui log          - Check logs                       │  
│  x-ui banlog       - Check Fail2ban ban logs          │  
│  x-ui update       - Update                           │  
│  x-ui legacy       - Legacy version                   │  
│  x-ui install      - Install                          │  
│  x-ui uninstall    - Uninstall                        |

`x-ui`  
Enable BBR - Enable BBR

`sudo ufw allow 39282`

### Установка сертификата

Красная плашка информирует нас о том, что соединение не зашифровано, и надо создать TLS-сертификат. Его можно создать двумя способами: подключить домен и выпустить сертификат через меню x-ui или создать самоподписанный сертификат. Мы создадим самоподписанный сертификат.

Для этого вводим следующие команды:

```sh
mkdir cert
cd cert
wget -qO- https://raw.githubusercontent.com/ServerTechnologies/3x-ui-with-xhttp/refs/heads/main/opensslcert | bash
```

После того как скрипт сработает, вы увидите несколько строчек с адресами файлов сертификатов. Откройте панель, в левом меню выберите **Настройки → Сертификаты**. Вставьте пути до файлов в соответствующие поля. Нажмите "Сохранить" и "Перезапуск панели". Панель перезапустится и вы увидите предупреждение о безопасности. Всё в порядке — браузер ругается, потому что мы используем самоподписанный сертификат. Просто нажимаем соответствующую кнопку и подключаемся к панели.  
При последующем вводе адреса панели в браузер не забывайте менять протокол с `http` на `https`.

### Создание подключения. Простой способ. XHTTP Vless Reality

Технология XHTTP может использоваться как совместно с CDN-сервисами, так и отдельно — примерно так же, как обычный Vless Reality с TLS. Для этого в панели 3x-ui в правом меню выбираем **Инбаунды → Создать инбаунд**:

- Протокол: Vless  
- Порт: 443  
- Транспорт: XHTTP  
- Безопасность: Reality  
- В **Dest** и **SNI** указываем любой незаблокированный иностранный сайт  
- Нажимаем **Get New Cert** и **Get New Seed**  
- Внизу нажимаем "Создать"

Подключение создано. Также создан один клиент. Можно добавить ещё несколько клиентов. Теперь передайте ссылку для подключения на устройство или отсканируйте QR-код — и можно пользоваться.

## 3proxy

### Установка 3proxy

`sudo apt-get install -y build-essential` - инструмент для установки из исходников

Номер последней версии 3proxy можно посмотреть на сайте: <https://3proxy.ru/>

`wget https://github.com/z3APA3A/3proxy/archive/0.9.3.tar.gz` - скачиваем

`tar xzf 0.9.3.tar.gz` - распаковываем

`cd ~/3proxy-0.9.3`  
`sudo make -f Makefile.Linux` - компилируем

`sudo mkdir /etc/3proxy`  
`cd ~/3proxy-0.9.3/bin`  
`sudo cp 3proxy /usr/bin/` - копируем бинарный файл

`command -v 3proxy` - проверить, что терминал понимает команду `3proxy`

`sudo adduser --system --no-create-home --disabled-login --group proxy3` - создаем системного юзера `proxy3`

`id proxy3` - узнать UID и GID

### Конфигурация 3proxy

#### 3proxy.cfg

`sudo nano /etc/3proxy/3proxy.cfg` - создаем конфигурационный файл.

Пример файла:

```bash
# Запускаем сервер от пользователя proxy3
# (возможно в вашей ОС uid и gid пользователя proxy3
# будут другими. Для их определения воспользуйтесь командой id proxy3)
setgid 115
setuid 109
#
# Пропишите правильные серверы имен посмотрев их
# на своем сервере в /etc/resolv.conf
nserver 188.93.16.19
nserver 188.93.17.19
#
# Оставьте размер кэша для запросов DNS по умолчанию
nscache 65536
#
# Равно как и таймауты
timeouts 1 5 30 60 180 1800 15 60
#
# Если несколько IP на одном сервере, указываем тот,
# через который будем ходить во внешний мир.
# Иначе эту строку игнорируем
#external 
# Тоже самое, только указываем IP, который надо слушать
# Если проигнорировать, то прокси слушает все адреса на сервере
#internal 
#
# Указываем на расположение файла с пользователями и паролями
users $/etc/3proxy/.proxyauth
#
# укажите режим запуска как daemon
daemon
#
# путь к логам и формат лога, к имени лога будет добавляться дата создания
log /var/log/3proxy/3proxy.log D
logformat "- +_L%t.%. %N.%p %E %U %C:%c %R:%r %O %I %h %T"
#
# Включаем авторизацию по логинам и паролям
auth cache strong
#
# Конфигурация http(s) proxy
# Запускаем анонимный (-a) HTTP-proxy на порту (-p) 3128 и
# c отключенной NTLM-авторизацией (-n)
proxy -n -p3128 -a
```

#### .proxyauth

`sudo nano /etc/3proxy/.proxyauth` - создаем файл с пользователями и паролями

Формат файла:

```bash
## addusers in this format:
#user:CL:password
##see for documentation: http://www.3proxy.ru/howtoe.asp#USERS
username:CL:strongpassword
```

Где логин username и пароль strongpassword следует изменить на свои. Каждый новый пользователь указывается с новой строки.

### Настройка прав доступа и логирования

`sudo chown proxy3:proxy3 -R /etc/3proxy` - рекурсивно меняем владельца директории с конфигом на пользователя `proxy3` и группу `proxy3`

`sudo chown proxy3:proxy3 /usr/bin/3proxy`

`sudo chmod 444 /etc/3proxy/3proxy.cfg` - только чтение для всех пользователей

`sudo chmod 400 /etc/3proxy/.proxyauth` - только чтение для владельца

`sudo mkdir /var/log/3proxy` - создаем папку для логов  
`sudo chown proxy3:proxy3 /var/log/3proxy`

### Автозагрузка и запуск

`sudo nano /etc/systemd/system/3proxy.service` - создаем файл-инициализации для systemd

`sudo systemctl daemon-reload` - обновляем конфигурацию systemd

`sudo systemctl enable 3proxy` - добавляем в автозагрузку

`sudo systemctl start 3proxy` - запускаем

`systemctl status 3proxy.service` - проверить статус

### Открываем порт

`sudo ufw allow 3128/tcp` - при использовании ufw  
`sudo ufw reload`

### Удаляем временные файлы

`rm ~/0.9.3.tar.gz`

`sudo rm -r ~/3proxy-0.9.3`
