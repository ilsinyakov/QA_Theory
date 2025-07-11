# Релизы

## Содержание

* [Жизненный цикл выпуска программного обеспечения (SRLC)](#жизненный-цикл-выпуска-программного-обеспечения-srlc)
  * [До начала основной разработки: POC](#до-начала-основной-разработки-poc)
  * [До начала основной разработки: MVP](#до-начала-основной-разработки-mvp)
  * [Стадия Pre-Alpha](#стадия-pre-alpha)
  * [Стадия Alpha (Альфа версия)](https://github.com/ilsinyakov/QA_Theory/blob/main/release.md#стадия-alpha-альфа-версия)
  * [Beta версия](#beta-версия)
  * [Release Candidate - предварительная версия](#release-candidate---предварительная-версия)
  * [Выпуск (Release)](#выпуск-release)
  * [Стадия технической поддержки (Maintenance)](#стадия-технической-поддержки-maintenance)
* [Этапы разработки новой версии программы](#этапы-разработки-новой-версии-программы)
  * [Заморозка функциональности (Feature freeze)](#заморозка-функциональности-feature-freeze)
  * [Заморозка кода (Code freeze)](#заморозка-кода-code-freeze)
  * [Отрезание веток релиза (Release branch cut)](#отрезание-веток-релиза-release-branch-cut)
* [Среды окружения (Environments)](#среды-окружения-environments)
  * [Среды разработки и тестирования](#среды-разработки-и-тестирования)
  * [Staging и Live](#staging-и-live)

## Жизненный цикл выпуска программного обеспечения (SRLC)

Как живое существо, программное обеспечение проходит определенные стадии жизни. Разработка начинается с POC (доказательство осуществимости концепции), затем MVP (Минимально жизнеспособный продукт), Pre-alpha, Alpha (Альфа-версия), Beta (Бета-версия), Release-candidate (предварительная версия), Production release (Выпуск) и Maintenance (Стадия поддержки).

### До начала основной разработки: POC

**POC (Proof of concept)** — доказательство осуществимости концепции.

Любое приложение начинается с идеи, как сделать мир лучше или хотя бы, как сделать создателей богаче.

Прежде чем приступить к разработке, идею необходимо проверить и продемонстрировать фокус-группе, собрать и проанализировать отзывы, порадовать инвесторов радужными перспективами продукта.

Чтобы сделать это реальным, но не тратить на реализацию десятки миллионов долларов, разрабатывается специальная начальная версия приложения. Она называется POC (proof of concept) и представляет собой очень усеченную версию, иногда с неприглядным пользовательским интерфейсом, но способную выполнять некоторые потрясающе функциональные действия, которые призваны полностью изменить рынок. Сам рынок, скорее всего, никогда не увидит эту версию, но ее увидят инвесторы или потенциальные пользователи. Демонстрация версии часто сопровождается подробными пояснениями, презентациями, требованиями, полученными от фокус-групп.

От этого этапа во многом зависит будущее финансирование реализации приложения. Способность продемонстрировать возможности и ярко рассказать о них определяет все будущие состояния жизненного цикла ПО.

### До начала основной разработки: MVP

**MVP (Minimal Viable Product)** - минимально жизнеспособный продукт.  Это работоспособное приложение, которое уже может быть кому-то полезно на рынке. Оно включает в себя основную для пользователей функциональность и графический интерфейс, позволяющий пользователю управлять приложением.

### Стадия Pre-Alpha

На этом этапе команда еще анализирует рынок и принимает решение о будущих возможностях приложения, но уже ведется планирование предстоящих релизов, таких как Alpha, Beta и т.д. Все этапы жизненного цикла разработки, такие как планирование, проектирование, реализация и даже тестирование, уже реализованы, Agile-процесс настроен и применяется, а команда сформирована.

Это самое подходящее время, чтобы узнать скорость работы команды и уточнить оценки и прогнозы.

Бэклог наполняется историями, обсуждается и разрабатывается архитектура будущего приложения.

Другими словами, эта фаза очень важна для планирования будущих релизов. Ошибки в архитектуре, которые могут быть допущены на этой фазе, могут стоить очень дорого, поэтому участие команды тестирования в этой фазе очень важно.

### Стадия Alpha (Альфа версия)

По сути, это внутренняя версия продукта до его выхода на рынок. Здесь нет пользователей, а все операции выполняются внутренними специалистами.

Это этап активной разработки, жестких сроков и борьбы за качество продукта. Одновременно реализуется много функциональности, возможен взрывной рост команды. "Молодая развивающаяся перспективная компания" - это, как правило, про стадию альфа.

Здесь присутствует вся пирамида тестирования - от юнит-тестирования до приемочного тестирования, причем в приемочном тестировании участвуют представители заказчика.

Понимание потребностей на этом этапе основывается на обратной связи с пользователями, полученной во время прохождения стадий POC и MVP.

### Beta версия

На этом этапе приложение наконец-то демонстрируется конечным пользователям (все слышали фразу "бета-тестер", это как раз про этап бета-версии). Продукт еще не завершен, но основная функциональность реализована и могут быть проверены.

Команда концентрируется на исправлении ошибок и изменении функциональности в соответствии с отзывами новых пользователей. Начинает расти роль проверки удобства использования, может начаться тестирование конфигурации и автоматизация для новых устройств. Может оказаться, что значительное количество людей использует устройство, не предусмотренное требованиями, и некоторая функциональность на нем работают плохо.

Время от времени приходится сталкиваться с архитектурными дефектами, возникающими в результате ошибок на предыдущих этапах.

Многие руководители считают этот этап критическим, но многие разработчики его игнорируют. Успех продукта во многом зависит от этого этапа и результатов бета-тестирования, а также от способности команды реагировать на мнение пользователей и перестраиваться как можно быстрее.

### Release Candidate - предварительная версия

Release Candidate (Стадия-кандидат) - это последняя версия перед выходом продукта на рынок. Она должна обладать всей заявленной для релиза функциональностью, работать в среде, аналогичной производственной, в идеале не содержать критических ошибок и учитывать все отзывы пользователей предыдущей (бета) версии.

Таких кандидатов может быть несколько.

Основная задача тестировщиков в этот момент  - обеспечить обратную связь с системного и приемочного уровней. Для окончательной оценки качества этой версии в тестировании участвуют и представители заказчика.

### Выпуск (Release)

Релиз продукта - это версия, которая выходит в свет, видна всему миру, может быть установлена или просмотрена через Интернет, и является воплощением напряженной работы вашей команды. Безусловно, эта версия должна быть достаточно стабильной, всесторонне протестированной и принятой представителями заказчика.

С этого момента ваше приложение делится на "живую" версию и "рабочую".

### Стадия технической поддержки (Maintenance)

Последний этап жизни приложения - техническая поддержка (Maintenance).  

Если версия заморожена и по каким-то причинам больше не разрабатывается (топ-менеджеры решили разрабатывать другой продукт, рынку он не нужен, конкуренты победили и т.д.), то реализация новых возможностей прекращается, но поддержка по-прежнему необходима.

В данном случае под поддержкой понимается исправление ошибок для пользователей, поддержка клиентов и, возможно, некоторый рефакторинг кода.

Тестирование ПО на этом этапе сводится к проверке правильности исправления дефектов и регрессионным прогонам. Никакой новой функциональности, никаких новых испытаний. Работа становится немного скучной, но для молодых специалистов или уставших от напряженной работы инженеров проект на стадии поддержки может стать хорошим местом для обучения или отдыха.

## Этапы разработки новой версии программы

Рассмотрим ситуацию, когда внутренняя версия выходит раз в две недели, одновременно с окончанием SCRUM-спринта.

Функциональность релиза известна в начале спринта, и работы планируются соответствующим образом. Неопределенные истории согласовываются, и начинается их реализация.  

Параллельно проводится тестирование, ручное и автоматизированное.

### Заморозка функциональности (Feature freeze)

За несколько дней до релиза происходит замораживание функциональности. Это означает, что разработчики не имеют права добавлять новые возможности в выпускаемый код, а должны сосредоточиться на исправлении ошибок и реализации некоторых критических замечаний из отзывов пользователей.

К моменту замораживания должно быть завершено тестирование всей новой функциональности.  

Руководитель группы тестирования должен спланировать работу команды таким образом, чтобы циклы регрессионного тестирования были пройдены, а результаты задокументированы. Дефекты, обнаруженные в ходе "заморозки", должны стать основными приоритетными задачами разработчиков после "заморозки".  

### Заморозка кода (Code freeze)

Замораживание кода - это следующий этап подготовки релиза. Если после замораживания функциональности разработчики не могут добавлять новый функционал, то после замораживания кода они вообще не должны прикасаться к коду. Все изменения должны быть сделаны перед этим, или отложены. Единственным исключением может быть случайно обнаруженный критический дефект или блокировка, препятствующая выпуску.

Все дефекты (кроме критических), обнаруженные после заморозки кода, должны быть исправлены в следующем релизе. Регрессионное тестирование в этот период не имеет особого смысла, поэтому время лучше посвятить написанию новых тестовых случаев и обновлению тестовой модели.

В реальной жизни и замораживание функциональности и замораживание кода, к сожалению, часто игнорируются разработчиками, чьи навыки планирования могут быть не идеальны. Часто они не могут успеть со своим кодом к этим критическим точкам.

В случае зрелого процесса "замораживание" функциональности и кода должно неукоснительно соблюдаться всеми членами команды.

### Отрезание веток релиза (Release branch cut)

В репозитории кода (в системе контроля версий (VCS), например, Git) ветвление может выглядеть следующим образом:

![branch](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/release_branch.jpg)

Разработчики и автоматические тестировщики на протяжении всего спринта делают коммиты в master, dev или другую общую ветку. В конце двухнедельного спринта (напомню, что мы рассматриваем случай, когда релиз выходит раз в две недели) создается релизная ветка со всеми изменениями, сделанными для данного конкретного релиза, и отрезается. Теперь никто не имеет доступа к этой ветке и не может модифицировать ее с учетом изменений. Выполнено замораживание кода.

## Среды окружения (Environments)

Как разработка, так и тестирование релизов редко выполняются на локальных машинах. Единственное исключение - подготовка кода или автоматизированных тестов перед отправкой в репозиторий. Все результаты новой версии, даже промежуточные, должны быть получены в специально настроенных средах, и, что важно, с заранее известной конфигурацией. В противном случае процент возможных ошибок в конфигурации может быть очень велик.

Количество сред окружения может быть различным для разных проектов и зависеть от целей проекта, размера команды, планируемых мероприятий по разработке и тестированию, и даже финансирования компании. Это может быть отдельный локальный сервер или облачный сервер. Иногда роль среды играет часть физического или облачного сервера.

### Среды разработки и тестирования

1. **Среда разработки (Development environment)**. Специальная среда для выполнения модульных тестов и проверки последних изменений в продукте. Доступна для команды разработчиков, но время от времени разработчики могут просить команду тестирования проверить что-то там, прежде чем фиксировать изменения в тестовой среде.
2. **Среда интеграционного тестирования (Integration testing environment)**. Для того чтобы процессы в системе были наглядными, должна быть создана специальная конфигурация с доступом к бэкенду и базам данных, протоколированием на максимальных уровнях и, возможно, дополнительной обработкой ошибок.
3. **Среда тестирования системы (System testing environment)**.  Здесь не требуется столь глубокого тестирования, а конфигурация может быть аналогична будущему продукту. Но версия продукта там - не та, которая выпускается, а та, над которой работает команда разработчиков.
4. **Среда нагрузочного тестирования (Load testing environment)**. Это специальная среда для команды тестирования производительности. Оборудование здесь должно быть более быстрым и мощным, может потребоваться специальная конфигурация. Версия продукта здесь является копией выпускаемой.
5. **Среда пользовательского приемочного тестирования (User Acceptance testing UAT)**. Среда пользовательского приемочного тестирования (UAT). Это копия производственной среды, то есть данные и конфигурация должны быть такими же, как при использовании продукта. При этом версия продукта может быть любой.

### Staging и Live

1. **Среда Staging или просто Staging**. Это полная копия производственной среды, включая версию продукта. Эта среда необходима для проверки производственных дефектов пользователей и финального тестирования перед выпуском релиза (обычно Smoke).
2. **Live или Производственная среда или Production**. Среда, в которой установлена и настроена "живая" версия, в которой запускаются реальные пользователи, иными словами, та версия, которая "на первом плане".
