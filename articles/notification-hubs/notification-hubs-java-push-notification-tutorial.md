---
title: "aaaHow toouse концентраторов уведомлений с помощью Java"
description: "Узнайте, как toouse концентраторов уведомлений Azure из внутренней Java."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>Как toouse концентраторы уведомлений из Java
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

В этом разделе Описание ключевых возможностей hello официальные hello новый полностью поддерживается пакет SDK для Java концентратора уведомлений Azure. Это проекта с открытым кодом и вы можете просмотреть код всего пакета SDK для hello в [Java SDK]. 

В общем случае можно открыть из внутренней Java и PHP и Python и Ruby все функции концентраторов уведомлений с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx). Пакет SDK для Java предоставляет тонкую оболочку для этих интерфейсов REST на Java. 

Hello SDK поддерживает в настоящее время:

* операции CRUD для центра уведомлений; 
* операции CRUD для регистрации;
* управление установкой;
* регистрацию импорта и экспорта;
* обычную отправку;
* запланированную отправку;
* асинхронные операции с использованием Java NIO;
* Поддерживаемые платформы: APNS (iOS), GCM (Android), WNS (приложения для Магазина Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android без служб Google). 

## <a name="sdk-usage"></a>Использование пакета SDK
### <a name="compile-and-build"></a>Компиляция и сборка
Использование [Maven]

toobuild:

    mvn package

## <a name="code"></a>Код
### <a name="notification-hub-cruds"></a>Операции CRUD в центрах уведомлений
**Создание NamespaceManager:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**Создание центра уведомлений:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 ИЛИ

    hub = new NotificationHub("connection string", "hubname");

**Получение центра уведомлений:**

    hub = namespaceManager.getNotificationHub("hubname");

**Обновление центра уведомлений:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**Удаление центра уведомлений:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>Операции CRUD для регистрации
**Создание клиента центра уведомлений:**

    hub = new NotificationHub("connection string", "hubname");

**Создание регистрации Windows:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**Создание регистрации iOS:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

Аналогичным образом можно создавать регистрации для Android (GCM), Windows Phone (MPNS) и Kindle Fire (ADM).

**Создание регистрации шаблона:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**Создание регистрации с помощью шаблона создания registrationid + upsert**

Удаляет дубликаты из-за потери tooany ответы, если для хранения идентификаторов регистрации на устройстве hello:

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**Обновление регистраций:**

    hub.updateRegistration(reg);

**Удаление регистраций:**

    hub.deleteRegistration(regid);

**Запрос регистраций:**

* **Получение одной регистрации:**
  
    hub.getRegistration(regid);
* **Получение всех регистраций в центре:**
  
    hub.getRegistrations();
* **Получение регистраций с тегом:**
  
    hub.getRegistrationsByTag("myTag");
* **Получение регистраций по каналу:**
  
    hub.getRegistrationsByChannel("devicetoken");

Все запросы коллекций поддерживают маркеры $top и маркеры продолжения.

### <a name="installation-api-usage"></a>Использование API установки
API установки — это альтернативный механизм управления регистрацией. Вместо хранения нескольких регистраций, которым является непростой задачей и можно легко сделать неправильно или неэффективно, теперь стало возможно toouse объекта установки. Установка включает в себя все необходимые составляющие: канал отправки (маркер устройства), теги, шаблоны и вспомогательные плитки (для WNS и APNS). Больше не требуется toocall hello службы tooget идентификатор — просто сформировать идентификатор GUID или другие идентификаторы, сохранить его на устройстве и отправьте серверной tooyour вместе с канала push (маркер устройства). На серверной hello следует делать, только один вызов: CreateOrUpdateInstallation, он является полностью идемпотентными, и вы можете бесплатно tooretry при необходимости.

Пример для Amazon Kindle Fire:

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Если необходимо, чтобы tooupdate его: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

Для сложных сценариев, у нас есть возможность частичное обновление, позволяющий toomodify hello объекта установки только определенных свойств. В сущности, частичное обновление является подмножеством операций исправления JSON, которые можно запустить для объекта установки.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

Удаление установки:

    hub.deleteInstallation(installation.getInstallationId());

Операции CreateOrUpdate, Patch и Delete окончательно согласованы с операцией Get. Запрошенную операцию просто перестает toohello системной очереди во время вызова hello и выполняется в фоновом режиме. Обратите внимание, что Get не предназначен для выполнения основных сценария, но только для отладки и устранения неполадок регулируется тесно службой hello.

Поток отправки для установки является hello то же, что для регистрации. Мы только что ввели toohello уведомления tootarget параметр установки - тега, просто воспользуйтесь «InstallationId: {требуемого id}». Для вышеупомянутых случаев это будет выглядеть следующим образом:

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

Для одного из нескольких шаблонов:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>Планирование уведомлений (доступно для уровня STANDARD)
Здравствуйте таким же, как обычный отправка, но один дополнительный параметр - scheduledTime, что когда уведомление должно быть доставлено. Для отправки можно указать любое время в диапазоне «теперешнее время-5 минут» и «теперешнее время-7 дней».

**Планирование собственных уведомлений Windows:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>Импорт или экспорт (доступно для уровня STANDARD)
Иногда бывает требуется tooperform массовой операции для регистрации. Обычно используется для интеграции с другой системой или просто значительных исправление toosay обновления hello теги. Если речь идет об тысячи регистраций toouse Get или обновления потока настоятельно не рекомендуется. Возможность импорта и экспорта встречается спроектированный toocover hello. По сути укажите контейнер больших двоичных объектов toosome доступа под учетной записью хранения как источник входящих данных и расположение для выходных данных.

**Отправка задания экспорта:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**Отправка задания импорта:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**Ожидание завершения задания:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**Получение всех заданий:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**URI с подписью SAS:** это URL-адрес hello некоторые файла BLOB-объект или контейнер больших двоичных объектов, а также набор параметров, таких как разрешения и время истечения срока действия, а также подпись следующие действия, выполненные с помощью ключа SAS для учетной записи. Пакет SDK для Java для службы хранилища Azure предоставляет широкие возможности, включая создание подобных универсальных кодов ресурса. Простой альтернативой рассмотрим ImportExportE2E тестового класса (из расположения github hello) с очень основные и compact реализацию алгоритм подписи.

### <a name="send-notifications"></a>Отправка уведомлений
Hello объекта уведомления является просто текст с заголовками, помочь некоторые вспомогательные методы для построения объектов hello машинного кода и шаблон уведомления.

* **Магазин Windows и Windows Phone 8.1 (без Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Windows Phone 8.0 и 8.1 Silverlight**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **Отправить tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Отправить tootag выражение**       
  
        hub.sendNotification(n, "foo && ! bar");
* **Отправка шаблонного уведомления**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

После выполнения кода Java на целевом устройстве должно отобразиться уведомление.

## <a name="next-steps"></a>Дальнейшие действия
В этом разделе мы показали, как toocreate простой Java REST клиента для концентраторов уведомлений. На данном этапе можно сделать следующее.

* Загрузка полного hello [Java SDK], содержащего hello весь код, пакет SDK. 
* Воспроизведение с образцами hello:
  * [Приступая к работе с центрами уведомлений]
  * [Отправка экстренных новостей]
  * [Отправка локализованных экстренных новостей]
  * [Отправлять уведомления пользователям tooauthenticated]
  * [Отправлять уведомления кросс платформенных tooauthenticated пользователей]

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Приступая к работе с центрами уведомлений]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Отправка экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Отправка локализованных экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Отправлять уведомления пользователям tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Отправлять уведомления кросс платформенных tooauthenticated пользователей]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

