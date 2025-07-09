# CI / CD

## Jenkins

### Установка плагинов

* **Git Plugin**. Позволяет Jenkins’у работать с Git-репозиториями.
* **GitHub Plugin / GitHub Integration Plugin**. Обеспечивает интеграцию с GitHub и позволяет принимать уведомления от GitHub.

### Добавление SSH-ключей в Credentials

* Настройка_Jenkins / Security / Credentials / System / Global_credentials
* Жмем *Add Credentials*
* В поле *Kind* выберите *SSH Username with private key*
* Заполняем поля:
  * *Scope*: обычно оставляют *Global*
  * *Username*: имя пользователя на вашем удалённом сервере
  * *Private Key*: если у вас уже готов открытый/закрытый ключ, выберите Enter directly и вставьте содержимое вашего приватного ключа
  * *ID* (необязательно): по умолчанию Jenkins присвоит автоматически UUID, но вы можете явно прописать, например, REMOTE_SSH_CRED
  * *Description* - описание
* *ОК*

### Создание пайплайна

* Создаем `Item` типа `Pipeline`
* В настройках в Triggers ставим галочку: *GitHub hook trigger for GITScm polling* - чтобы Jenkins слушал события на эндпоинте github-webhook
* 


### Настройка WebHook в репозитории

* В репозитории GitHub → Settings → Webhooks → Add webhook
* *Payload URL*:  
`https://<JENKINS_URL>/github-webhook/`
* *Content type*:  
`application/json`
* *Which events*: выберите Just the push event
* *Add webhook*
