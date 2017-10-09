---
title: "aaaConnectors для приложения логики Azure | Документы Microsoft"
description: "Выберите из всех toobuild hello доступных соединителей, управляемая корпорацией Майкрософт и создание приложений логики"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Список соединителей
> [!TIP]
> Hello [полный список A-Z](#az) (в этом разделе) перечисляет все доступные соединители hello можно использовать в приложениях для логики. [Сведений о соединителе](/connectors/) перечисляет все триггеры и действия, определенные в hello swagger, а также любые пределы для каждого соединителя.

Соединители являются неотъемлемой частью при создании приложений логики. С помощью этих соединителей, действительно можно развернуть локальных и облачных приложений toodo разное значение данных, создаваемых и данными, уже имеющихся. соединители Hello доступны следующие категории hello. 

* **Стандартные соединители.** Автоматически доступны при использовании приложений логики. Примеры включают соединители служебной шины, Power BI, Oracle Database, OneDrive и пр.

* **Соединители для учетной записи интеграции.** Доступны при приобретении учетной записи интеграции. С помощью этих соединителей вы можете преобразовать и проверять XML, обрабатывать сообщения типа "бизнес — бизнес" с помощью AS2, X12 или EDIFACT, а также кодировать и декодировать неструктурированные файлы. Если вы работаете с BizTalk Server, затем эти соединители — это хорошо подходит tooexpand рабочие процессы BizTalk в Azure.  

    BizTalk Server также имеет [Logic Apps адаптера](https://msdn.microsoft.com/library/mt787163.aspx) , включает в себя получение из логики приложения и отправку tooa логику приложения.

* **Корпоративные соединители.** Сюда относятся MQ и SAP. Доступны за дополнительную плату. 

[Логика приложения цены](https://azure.microsoft.com/pricing/details/logic-apps/) и [модель ценообразования](../logic-apps/logic-apps-pricing.md) предоставляются дополнительные сведения о hello затраты. 

## <a name="popular-connectors"></a>Популярные соединители
Тысячи приложений и миллионы выполнений успешно обрабатывают данные и сведения с помощью этих соединителей. Привет, в следующей таблице перечислены наиболее популярных hello и некоторые Избранное с нашими:

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Хранилище BLOB-объектов<br/>Azure** ][AzureBlobStoragedoc] | Если вы хотите tooautomate все задачи с вашей учетной записи хранения, должен выглядеть на этот соединитель. Поддерживает выполнение операций CRUD (создание, чтение, обновление и удаление). | [![API Icon][Azure-Functionsicon]<br/>**Функции Azure**][azure-functionsdoc] | Создавайте функции, с помощью которых можно выполнять настраиваемые фрагменты кода C# или Node.js, а затем используйте эти функции в приложении логики.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Одно из hello, задаваемые большинство для соединителей. Он имеет триггеров и действий toohelp автоматизировать рабочие процессы с потенциальными клиентами и многое другое. | [![API Icon][Event-Hubs-icon]<br/>**Концентраторы событий**][event-hubs-doc] | Используйте события и публикуйте их в концентраторе событий. Например можно получить выходные данные из логики приложения с помощью концентраторов событий и отправьте поставщик аналитика в реальном времени tooa вывода hello. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | Если FTP-сервер доступен с hello Интернета, а затем можно автоматизировать toowork рабочих процессов с файлами и папками. <br/><br/>SFTP также доступен соединитель SFTP hello. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Используйте логику приложения toocommunicate с любой конечной точке по протоколу HTTP. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Большое количество триггеров и гораздо больше электронной почты Office 365 toouse действия и события в рабочих процессах. <br/><br/>Этот соединитель включает *утверждения электронной почты* запросы отпуска tooapprove действий, отчеты по расходам и т. д. <br/><br/>Пользователи Office 365 также доступны с соединителем hello пользователей Office 365.| [![API Icon][HTTP-Requesticon]<br/>**Запрос и ответ**][HTTP-Requestdoc] | Этот соединитель предоставляет URL-адрес для протокола HTTPS. Получив URL-адрес запроса toothis логику приложения hello запускает логику приложения hello. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Легко вход в Salesforce учетной записи tooget доступ tooobjects, например руководителей и многое другое. |  [![API Icon][Service-Busicon]<br/>**Служебная шина**][Service-Busdoc] | Наиболее популярные соединителя Hello в пределах логики приложения, включаются триггеры и действия toodo асинхронный обмен сообщениями и публикации или подписки с очередями, подписки и разделы. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Если вы знакомы с SharePoint и заинтересованы в преимуществах автоматизации, мы советуем выбрать именно этот соединитель. Вы можете использовать его с локальным SharePoint и SharePoint Online. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Наиболее используется одна из hello соединителей, возможность подключения tooan локального SQL Server и базы данных SQL Azure. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Выполняйте быстрый вход с помощью учетной записи Twitter и запускайте рабочий процесс после публикации твита. Сохраните эти базы данных SQL tooa твиты или списка SharePoint. | | | 

## <a name="integration-account-connectors"></a>Соединители для учетной записи интеграции 

Hello пакет интеграции Enterprise (EIP) включает соединителей, которые будут хорошо известных toohello сообщества BizTalk Server. При покупке [учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), можно также получить следующие соединители hello: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**Декодирование</br> AS2**][as2decode] | [![API Icon][as2icon]<br/>**Кодирование</br> AS2**][as2encode] | [![API Icon][x12icon]<br/>**Декодирование</br> EDIFACT**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**Кодирование</br> EDIFACT**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Кодирование</br> неструктурированных файлов**][flatfiledoc] | [![API Icon][flatfiledecodeicon]<br/>**Декодирование</br> неструктурированных файлов**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Учетная запись<br/>интеграции**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**Преобразование<br/>XML**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**Декодирование</br> X12**][x12decode] | [![API Icon][x12icon]<br/>**Кодирование</br> X12**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**Проверка <br/>XML**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Корпоративные соединители

Подключение tooyour корпоративных приложений в свои приложения логики.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Полный список

[Сведений о соединителе](/connectors/) список любое триггеров и действий, определенных в hello swagger, а также перечислены все ограничения для каждого соединителя.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>Планирование отправок-прибытий<br/><br/><a name="a"></a>Список<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Cлужба управления Azure API <br/>Службы приложений Azure<br/>Приложение Azure<br/>Служба автоматизации Azure<br/>[Хранилище BLOB-объектов Azure][azureblobstoragedoc]<br/>Озеро данных Azure<br/>Azure DocumentDB (Cosmos DB)<br/>[Функции Azure][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Очереди Azure<br/>Диспетчер ресурсов Azure<br/>[База данных SQL Azure][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Пакетная служба<br/>Электронная почта теста производительности<br/>Поиск Bing<br/>Bitbucket;<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Буфер<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>API компьютерного зрения Cognitive Services<br/>API распознавания лиц Cognitive Services<br/>Cognitive Services LUIS<br/>Текстовая аналитика Cognitive Services<br/>Common Data Service<br/>Преобразование содержимого<br/>Control-Terminate<br/>[Настраиваемые API-интерфейсы и веб-приложения][api/web-appdoc]<br/><br/><a name="d"></a>Операции с данными<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>DropBox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Концентраторы событий][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[Файловая система][filesystemdoc]<br/>[Неструктурированный файл][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>FreshService<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Календарь Google<br/>Контакты Google<br/>Google Диск<br/>Google Таблицы<br/>Google Задачи<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP и Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Учетная запись интеграции<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Средний<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Погода<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Пользователи Office 365<br/>Office 365 Видео<br/>OneDrive<br/>OneDrive для бизнеса<br/>OneNote (Business)<br/>[База данных Oracle][oracle-db-doc]<br/>Outlook Customer Manager<br/>Задачи Outlook<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Запрос и ответ][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[Сервер приложений SAP][sapconnector]<br/>[Сервер сообщений SAP][sapconnector]<br/>[Расписание][recurrencedoc]<br/>Область<br/>SendGrid<br/>Отправка сообщений toobatch<br/>[Служебная шина][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Преобразование XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Переменные<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[Проверка XML][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget работы с приложениями логики Azure перед регистрацией для учетной записи Azure перейдите слишком[Logic Apps повторите](https://tryappservice.azure.com/?appservice=logic). Там вы сможете быстро создать простое кратковременное приложение логики. Никаких кредитных карт и обязательств.

## <a name="connectors-as-triggers-and-actions"></a>Соединители как триггеры и действия

**Триггер** запускает или выполняет экземпляр приложения логики. Некоторые соединители служат триггерами, которые могут уведомлять приложение о возникновении определенных событий. Например, соединитель hello FTP имеет hello `OnUpdatedFile` триггер, который запускает приложение логики, при обновлении файла. 

Логика приложения включают следующие типы триггеров hello:  

* *Опрос триггеры*: эти триггеры опроса новых данных к службе toocheck указанного интервала. 

    При наличии новых данных новый экземпляр логику приложения выполняется с данными hello в качестве входного. 

* *Принудительная триггеры*: эти триггеры прослушивать данные в конечной точке, или для события toohappen, затем запускает новый экземпляр приложения логики.

* *Триггер повторения.* Этот триггер создает экземпляр приложения логики по определенному расписанию.

Соединители также предоставляют **действия**, которые можно использовать в рабочем процессе. Например, приложения логики могут выполнять поиск данных, а затем использовать эти данные позже. В частности можно поиска данных клиента из базы данных SQL и воспользуйтесь toobuild данных этого клиента рабочего процесса. 

> [!TIP]
> Дополнительные сведения о триггерах и действиях см. в [обзоре соединителей](connectors-overview.md). 


## <a name="message-manipulation-actions"></a>Действия управления сообщениями

Приложения логики содержат встроенные действия, с помощью которых можно изменять полезные данные или же управлять ими. встроенные Hello **операций с данными** соединитель включает hello, следующие действия: 

| | |
|---|---|
| **Действие создания** | Сборка или формирования значений или объектов toouse позже в ходе сборки рабочего процесса. Например можно создать объект JSON со значениями из нескольких шагов или вычисления константы tooreference позже в приложении логику выполнения. |
| **Создание таблицы CSV**<br/>**Создание таблицы HTML** | Преобразуйте результирующий набор массива в таблицу CSV или HTML. Например добавить действие «Список записей» CRM hello и Добавление фильтра для записей, добавленных в настоящее время. Отправьте hello результаты как HTML-таблицы в сообщение электронной почты. |
| **Фильтрация массива** (запрос) | Фильтровать записи toohello набор результатов, которые вас интересуют. Например, поиск всех твиты с `#Azure`, и затем «фильтр» hello возвращаются твиты tooonly возвращают результаты, которые являются `Tweeted_by_followers > 50`. |
| **Join** | Объедините массив по определенному разделителю. Например hello операции обнаружения ключевых фраз возвращает массив ключевых фраз. Вы можете объединить их с `,` или другим подобным разделителем. Таким образом, вместо `["Some", "Phrase"]` у вас будет `"Some, Phrase"`. |
| **Анализ JSON** | Синтаксического анализа и доступ к значениям из объекта JSON в конструкторе hello. Например если пользовательская функция Azure возвращает полезные данные JSON, затем вы можете проанализировать его свойства JSON tooaccess hello позже в другом шаге. Действие Hello также проверяет, hello JSON совпадений hello указанной схемы во время выполнения. | 
| **Выбор** | Выберите определенные свойства массива для дальнейшей обработки. Если вы выведете на экран список записей в SQL и получите 15 столбцов, выберите несколько столбцов для дальнейшей обработки. Hello выходные данные — массив, содержащий только свойства hello, выбранные. |

## <a name="custom-connectors-and-azure-certification"></a>Пользовательские соединители и сертификация Azure 

toocall в API-интерфейсы, запускать пользовательский код или недоступны соединителей, можно расширить поддержку платформы логики приложения hello, [Создание приложения API на основе REST пользовательских соединителей](../logic-apps/logic-apps-create-api-app.md). 

Если требуется toomake вашего пользовательского приложения API открытыми и доступными toouse в Azure, затем отправьте вашей заявки toohello [программы Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Получение справки

tooask вопросы, ответы на вопросы и см. какие другие пользователи приложения логики Azure делают, go toohello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики](http://aka.ms/logicapps-wish).

Мы не рассмотрели соединители или не указали какие-то другие сведения, которые вы считаете важными? Если Да, Помогите нам, добавив tooour существующие разделы или написать собственный. Наша документация включает открытый исходный код и размещается на сайте GitHub. Начало работы с нашим [репозиторием GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Дальнейшие действия
* [Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md)
* [Создание настраиваемых API для приложений логики](../logic-apps/logic-apps-create-api-app.md)
* [См. статью Мониторинг приложений логики.](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Интеграция приложений логики с приложениями API службы приложений."
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Управление файлами в контейнере больших двоичных объектов с помощью соединителя хранилища BLOB-объектов Azure"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Интеграция приложений логики с Функциями Azure"
[db2doc]: ./connectors-create-api-db2.md "Подключите tooIBM DB2 в облаке hello или в локальной среде. Обновление строки, таблицы и другие действия"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Подключение tooDynamics CRM Online, чтобы можно было работать с данными CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Подключение концентраторов событий tooAzure. Receive and send events between logic apps and Event Hubs" (Подключение к концентраторам событий Azure. Получение и отправка событий между приложением логики и концентраторами событий)
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Подключение tooan в локальной файловой системе"
[ftpdoc]: ./connectors-create-api-ftp.md "Подключение tooan FTP или FTPS-сервер для FTP задач, например отправка, получение, удаление файлов и многое другое"
[httpdoc]: ./connectors-native-http.md "Выполнение вызовов HTTP с соединителем HTTP hello"
[http-requestdoc]: ./connectors-native-reqres.md "Добавление действий для HTTP запросы и ответы tooyour логику приложений"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Вызовы HTTP с помощью соединителя HTTP + Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Подключите tooInformix в облаке hello или в локальной среде. Чтение строки, hello списка таблиц и многое другое"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Интеграция приложений логики с вложенным рабочим процессом."
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Подключите tooyour Office 365 учетную запись. Отправка и получение сообщений, управление календарем и контактами, а также другие действия"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Подключение tooadd базы данных Oracle tooan, вставки, удаления строк и многое другое"
[mqdoc]: ./connectors-create-api-mq.md "Подключите tooMQ в локальной среде или Azure и отправки и получения сообщений"
[recurrencedoc]:  ./connectors-native-recurrence.md "Активация повторяющихся действий для приложений логики"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Подключение tooyour учетной записи Salesforce. Управление учетными записями, потенциальными клиентами, возможностями и другие действия"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Подключение tooan в локальной системе SAP"
[service-busdoc]: ./connectors-create-api-servicebus.md "Отправка сообщений из очередей и разделов служебной шины, а также получение сообщений из очередей и подписок служебной шины"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Подключите tooSharePoint через Интернет. Управление документами, элементами списка и другие действия"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Подключите tooSharePoint на локальном сервере. Управление документами, элементами списка и другие действия"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Подключите tooAzure базы данных SQL или SQL server. Создание, обновление, получение и удаление записей в таблице базы данных SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Подключите tooTwitter. Получение обновлений, публикация твитов и выполнение других задач"
[webhookdoc]: ./connectors-native-webhook.md "Добавление веб-перехватчика действия и триггеры tooyour логику приложений"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Дополнительные сведения об AS2 в рамках корпоративной интеграции."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Дополнительные сведения об X12 в рамках корпоративной интеграции."
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Дополнительные сведения о неструктурированном файле в рамках корпоративной интеграции."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Дополнительные сведения о неструктурированном файле в рамках корпоративной интеграции."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Дополнительные сведения о проверке XML в рамках корпоративной интеграции."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Дополнительные сведения о преобразованиях в рамках корпоративной интеграции."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Дополнительные сведения о декодировании AS2 в рамках корпоративной интеграции."
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Дополнительные сведения о кодировке AS2 в рамках корпоративной интеграции."
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Дополнительные сведения о декодировании X12 в рамках корпоративной интеграции."
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Дополнительные сведения о кодировке X12 в рамках корпоративной интеграции."
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Дополнительные сведения о декодировании EDIFACT в рамках корпоративной интеграции."
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Дополнительные сведения о кодировке EDIFACT в рамках корпоративной интеграции."
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Поиск схем, карт, партнеров и другого в вашей учетной записи интеграции"


[boxDoc]: ./connectors-create-api-box.md "Подключите панель инструментов. Отправка, получение, удаление файлов, отображение их списка и другие действия"
[delaydoc]: ./connectors-native-delay.md "Выполнение отложенных действий"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Подключите tooDropbox. Отправка, получение, удаление файлов, отображение их списка и другие действия"
[facebookdoc]: ./connectors-create-api-facebook.md "Подключите tooFacebook. Учет tooa временной шкалы, страницы веб-канала и другие"
[githubdoc]: ./connectors-create-api-github.md "Подключение tooGitHub и отслеживания проблем"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Подключение tooGoogleDrive, поэтому можно работать с данными"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Подключение tooGoogle листы можно можно изменять листов"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Подключается tooGoogle задачи, поэтому вы можете управлять задачами"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Подключается tooGoogle календаря и управлять календаря."
[http-responsedoc]: ./connectors-native-reqres.md "Добавление действий для HTTP запросы и ответы tooyour логику приложений"
[instagramdoc]: ./connectors-create-api-instagram.md "Подключите tooInstagram. Активация событий и реакция на них"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Подключение учетной записи MailChimp tooyour. Управление сообщениями электронной почты и их автоматизация"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Подключение tooMandrill для обмена данными"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Подключите tooMicrosoft преобразователь. Перевод текста, обнаружение языков и другие действия" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Получение сведений о видео, списков и каналов видео, а также URL-адресов воспроизведения для видео Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Подключение tooyour личного хранилища OneDrive корпорации Майкрософт. Отправка, удаление, отображение файлов и другие действия"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Подключение business tooyour Microsoft OneDrive. Отправка, удаление, отображение файлов и другие действия"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Подключения почтового ящика tooyour Outlook. Управление электронной почтой, календарями, контактами и другие действия"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Подключите tooMicrosoft Project Online. Управление проектами, задачами, ресурсами и другие действия"
[querydoc]: ./connectors-native-query.md "Выбор и фильтрация массивы с действием запроса hello"
[rssdoc]: ./connectors-create-api-rss.md "Публиковать и извлекать элементы потока данных, вызывать операции, когда новый элемент опубликованного tooan RSS веб-канала."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Подключите tooSendGrid. Отправка электронных сообщений и управление списками получателей"
[sftpdoc]: ./connectors-create-api-sftp.md "Подключите учетную запись tooyour SFTP. Отправка, получение, удаление файлов и другие действия"
[slackdoc]: ./connectors-create-api-slack.md "Подключение tooSlack и помещать сообщения tooSlack каналов"
[smtpdoc]: ./connectors-create-api-smtp.md "Подключения tooa SMTP-серверу и отправки электронной почты с вложениями"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Подключается tooSparkPost для обмена данными"
[trellodoc]: ./connectors-create-api-trello.md "Подключите tooTrello. Управление проектами и организация всего и всех"
[twiliodoc]: ./connectors-create-api-twilio.md "Подключите tooTwilio. Отправка и получение сообщений, получение доступных номеров, управление входящими телефонными номерами и выполнение других задач"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Подключите tooWunderlist. Управление задачами и списками дел и их синхронизация, а также другие действия"
[yammerdoc]: ./connectors-create-api-yammer.md "Подключите tooYammer. Публикация сообщений, получение новых сообщений и другие действия"
[youtubedoc]: ./connectors-create-api-youtube.md "Подключите tooYouTube. Управление видео и каналами"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
