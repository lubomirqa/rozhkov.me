---
title: "Экономия на спичках"
date: 2020-05-05T15:51:32+03:00
lastmod: 2020-05-05T15:51:32+03:00
tags: ["work"]
---

Экономия на спичках

На прошлой неделе один из клиентов попросил посмотреть, что можно делать со стоимостью инфраструктуры. Счет за AWS уже перевалил за 200 баксов в месяц (при том что там крутится небольшая часть инфраструктуры) и клиент хотел сократить затраты.

Я пошел смотреть за что с нас берут деньги и заодно посмотрел и другие сервисы. После непродолжительного изучения счетов и биллинг историй я подсчитал, что всего на инфру тратится 550$. Из них 220$ на амазон, 300$ на jelastic и 30$ на heroku. 

Цена за Jelastic меня немного удивила, поэтому я пошел копать детальнее и обнаружил интересную вещь—если держать окружение выключенным, до деньги за использование cpu/ram не будут списываться, а вот за диск—будут. У нас висело несколько бекапов баз, которые кушали прилично места. Еще несколько серверов не использовались или были deprecated, и просто ели деньги не принося взамен большой ценности. Я убрал все что было и так выключено, удалил пару старых серверов, что в сумме, по моим прикидкам, дало экономию в 90$. Посмотрев на остальные траты и оценив стоимость сервера к мощностям которые он предоставляет я подумал что надо бы паковать все микросервисы в nomad/k8s и съезжать на три сервера средней толщины на каком-нибудь yandex cloud — можно будет сэкономить еще 100$ точно. Но это потом. Вся работа заняла максимум час.

С Heroku все понятно, там оптимизировать нечего, нужное и так крутится на free/hobby dynos которые 7$ стоят и не несут критической нагрузки.

С AWS пришлось немного повозиться. По какой-то причине я не мог получить доступ к детализированному счету (с указанием ресурсов) и пришлось работать с тем что есть. 80$ ушло на S3, а точнее на хранение примерно 3TB данных накопленных за 4 года работы различных продуктов. Большая часть из них—изображения, которые уже потеряли свою актуальность (все метаданные из них вытащены и находятся в базе). Удалять все подряд или использовать Lifecycle Rule для того, чтобы удалить данные старше года я не стал, вместо этого за пару часов напилил функциональность, которая позволяет пользователям помечать устаревшие "аккаунты" (к которым принадлежат данные) и система потихоньку сама почистит все объекты на S3. Оказалось так же что в CloudWatch можно смотреть метрики по размеру бакетов (я про это раньше не знал). Так что теперь буду мониторить размер. Ну и заодно поудалял данные совсем уж неактуальных проектов, гигабайт 200 наверное.

Сумма в 550$ большинству из инфраструктурщиков тут покажется смехотворной. Действительно, в одном из стартапов, где я работал, за месяц платили около 10 000$. Но там ехал микросервис в двух регионах через динамодб на пяти энвайронментах, что поделать.

Моя позиция состоит в том, что даже маленький кост надо оптимизировать. Я ожидаю удешевления инфраструктуры на 150$ в месяц. Теперь считаем—за год это будет 1800$ экономии. Это уже неплохие деньги, то есть даже на спичках есть смысл экономить. На все про все у меня ушло 3 часа работы. Сколько взять денег с клиента за эту задачу и как обосновать её стоимость я предполагаю пытливому читателю подумать самому.

p.s.: если сумма кажется вам смехотворной, но позовите меня в свою контору—я срежу вам косты (пусть даже на 50$ в месяц), а вы мне половину сэкономленной суммы за год за это заплатите. Какая разница кому давать бабки—амазону или мне?

p.p.s.: некто Corey Quinn на этом делает целый бизнес. Приходит к людям, [настраивает им vpc эндпоинты для s3 за полчаса](https://www.lastweekinaws.com/blog/an-aws-bill-analysis-changelogs-md/) чтоб трафик экономить и лупит пару тыщ баксов за это. 
