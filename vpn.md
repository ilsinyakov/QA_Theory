# VPN

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
