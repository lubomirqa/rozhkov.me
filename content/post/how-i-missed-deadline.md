---
title: "Как я дедлайн продолбал"
date: 2020-03-02T19:24:43+02:00
draft: true
lastmod: 2020-03-02T19:24:43+02:00
tags: ["random"]
---

У одного из заказчиков, с которым я работаю уже несколько лет, каждый год запускается один и тот же проект. Стартует он в октябре и идет примерно полгода. Технически это сайт, чатбот и еще несколько вещей. Каждый год дизайн сайта меняется, добавляется, модифицируется или убирается та или иная функциональность, в общем что-то новое.

Первые три релиза были сделаны на PHP и если вначале их поддерживал кофаундер шлюпки (node.js/PHP программист), то в прошлом году мне пришлось подхачивать проект уже самому. Чатбот был написан для двух мессенджеров, для одного—на node.js, для другого—как часть Rails-приложения, которое живет отдельно и никак не связано с основным проектом. Бот был заскриптован в коде с помощью if-else и switch-case. Один и тот же алгоритм в двух разных местах, да, DRY во все поля.

Каждое лето я знаю что в августе-сентябре надо будет снова переделывать этот проект, и в этот раз я решил все переписать на Rails, потому что поддержка существующего проекта была сущим адом, а чатботов перевести на другой сервис, который я разработал весной, и который позволяет описывать дерево диалогов и действия в виде абстрактного дерева, а дальше движок выполняет его и дает команды на адаптерам мессенджеров. 

Планы были грандиозными. Однако как-то так получилось что ничего из этого я не начинал делать. Параллельно мы начали переверстывать сайт по новому дизайну но делали это на старом PHP-шном решении. Я все прокрастинировал и никак не мог собраться и найти время для того чтобы мигрануть всё на Rails. Завел скелет, а дальше как-то не двигался и думал что за два дня всё успею. 

Вообще я всегда работаю под дедлайн. Если я вдруг почувствую что то, что мне говорят делать, на самом деле не нужно прямо сейчас, мозги включат режим "ага, это никому не нужно" и пойдут заниматься чем-то другим. Не уверен, что это полезное качество, но каким-то образом до сих пор мне удавалось выживать без серьезных просчетов. Когда работа кому-то нужна то тебе моментально начинают давать обратную связь, не работает то или это и в очень сжатые сроки можно свернуть горы и закрыть 80% вопросов. На остальные 20% как правило не хватает уже ни энергии ни мотивации, и переходишь к другому проекту.

И вот значит неделя до старта проекта, а у нас конь не валялся. Фронтендер пилит вёрстку, но там еще работать и работать, а мне же это еще все мигрировать! Созваниваемся с заказчиком, я обещаю что все будет четко, показываем что сделали сейчас, получаем кучу замечаний и как-то дальше разгребаем. Прикол еще и в том что заказчик должен показывать сайт своему заказчику, то есть мы как бы субподрядчики. Ну а то что есть показывать конечно невозможно. В общем мы работаем но к дню показа не успеваем. День показа—четверг, день старта—вторник. В четверг не показали, в пятницу я понимаю всю серьезность ситуации и начинаю кранчить.

Заказчику я не сказал что мы собираемся переписать всё с нуля. Обычно такие вещи пугают нетехнических людей, поэтому надо это как-то аккуратно переформулировать. В этот момент меня начали терзать сомнения правильно ли я сделал, что решил все мигрировать и может быть лучше подпилить слегка то что есть сейчас и выкатить? А то ведь багов непременно понаделаю! 

Но я решил воевать до конца и за выходные кое-как довел всё до ума. Дальше начались свистопляски с фротендом, там были некоторые вещи которые делали на js библиотеках, не обновляемых уже 4 года, но я переписал и все это.

К дате релиза всё сделать я не успел. Основная функциональность работала, но некоторые красивости не жужжали.

Утром во вторник заказчик написал что мы его конкретно подвели (ведь он отчитывался перед своим заказчиком) и что лучше бы было если бы мы просто отказались от работы, тогда бы он нашел других исполнителей, которые бы сделали в срок.

Я ответил что "прошу прощения за такую подставу с нашей стороны", и сказал что "постараемся побыстрее решить все проблемы".

Дальше занялись починкой, еще за пару дней почти всё довели до ума. Я ощутил плоды от миграции на RoR—новую функциональность я добавлял очень быстро и чувствовал полный контроль над ситуацией (в отличие от PHP с которым работать не так приятно и не так удобно). 

После я за полтора дня мигранул чатботов на новую платформу и это тоже принесет свои плоды—потому что текста теперь будут редактировать сами пользователи а не я в коде, и потому что для разных мессенджеров будет работать одна и та же конфигурация.

Какие уроки можно извлечь из этой ситуации? Да никаких! Не хочешь браться за работу—не берись, это и так понятно. Держи заказчика в курсе задержек—тоже понятно, а толку? Делай не под дедлайн а чуть-чуть заранее—пффф...

Получилось довольно неприятно и стрессово. Этого заказчика мы уже давно не подводили (были еще схожие ситуации, но в прошлые годы и попроще), у меня было всё, чтобы сделать работу вовремя, но я не сделал.

> Upd: Пост был написан в октябре 2019, сейчас март 2020. Деньги за проект я все-таки взял, но раза в 4 меньше, чем планировал за то же, но сделанное вовремя.

Сейчас у меня стоит дилемма—брать за проект деньги или не брать (под "не брать" я понимаю сумму условно говоря в 10 раз меньше). Нормальный разработчик взял бы еще и предоплату в размере 70% а потом бы исчез, но я не такой. Я не хочу брать денег за проект, который продолбал, совесть (сверх-я, родительская фигура и все такое) не позволяет.

Я еще не решил окончательно, но сам факт того что я думаю о том что денег на проекте не заработаю, серьезно снижает мою мотивацию по дальнейшей работе. Зачем что-то допиливать если бабло не получишь (точнее, получишь, но очень мало)? Поэтому, несколько косметических вещей на сайте я так до сих пор и не доделал. Хотя пообещал, что приложу к этому все усилия. В общем заказчик просит чтобы мы озвучили сумму, а я, вместо того чтобы взять ответственность и сделать это, прячу голову в песок. Дурацкая и парадоксальная ситуация, не так ли?
