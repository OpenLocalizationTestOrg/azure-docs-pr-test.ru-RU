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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="df1b2-103">Как toouse концентраторы уведомлений из Java</span><span class="sxs-lookup"><span data-stu-id="df1b2-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="df1b2-104">В этом разделе Описание ключевых возможностей hello официальные hello новый полностью поддерживается пакет SDK для Java концентратора уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="df1b2-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="df1b2-105">Это проекта с открытым кодом и вы можете просмотреть код всего пакета SDK для hello в [Java SDK].</span><span class="sxs-lookup"><span data-stu-id="df1b2-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="df1b2-106">В общем случае можно открыть из внутренней Java и PHP и Python и Ruby все функции концентраторов уведомлений с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="df1b2-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="df1b2-107">Пакет SDK для Java предоставляет тонкую оболочку для этих интерфейсов REST на Java.</span><span class="sxs-lookup"><span data-stu-id="df1b2-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="df1b2-108">Hello SDK поддерживает в настоящее время:</span><span class="sxs-lookup"><span data-stu-id="df1b2-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="df1b2-109">операции CRUD для центра уведомлений;</span><span class="sxs-lookup"><span data-stu-id="df1b2-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="df1b2-110">операции CRUD для регистрации;</span><span class="sxs-lookup"><span data-stu-id="df1b2-110">CRUD on Registrations</span></span>
* <span data-ttu-id="df1b2-111">управление установкой;</span><span class="sxs-lookup"><span data-stu-id="df1b2-111">Installation Management</span></span>
* <span data-ttu-id="df1b2-112">регистрацию импорта и экспорта;</span><span class="sxs-lookup"><span data-stu-id="df1b2-112">Import/Export Registrations</span></span>
* <span data-ttu-id="df1b2-113">обычную отправку;</span><span class="sxs-lookup"><span data-stu-id="df1b2-113">Regular Sends</span></span>
* <span data-ttu-id="df1b2-114">запланированную отправку;</span><span class="sxs-lookup"><span data-stu-id="df1b2-114">Scheduled Sends</span></span>
* <span data-ttu-id="df1b2-115">асинхронные операции с использованием Java NIO;</span><span class="sxs-lookup"><span data-stu-id="df1b2-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="df1b2-116">Поддерживаемые платформы: APNS (iOS), GCM (Android), WNS (приложения для Магазина Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android без служб Google).</span><span class="sxs-lookup"><span data-stu-id="df1b2-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="df1b2-117">Использование пакета SDK</span><span class="sxs-lookup"><span data-stu-id="df1b2-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="df1b2-118">Компиляция и сборка</span><span class="sxs-lookup"><span data-stu-id="df1b2-118">Compile and build</span></span>
<span data-ttu-id="df1b2-119">Использование [Maven]</span><span class="sxs-lookup"><span data-stu-id="df1b2-119">Use [Maven]</span></span>

<span data-ttu-id="df1b2-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="df1b2-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="df1b2-121">Код</span><span class="sxs-lookup"><span data-stu-id="df1b2-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="df1b2-122">Операции CRUD в центрах уведомлений</span><span class="sxs-lookup"><span data-stu-id="df1b2-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="df1b2-123">**Создание NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="df1b2-124">**Создание центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="df1b2-125">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="df1b2-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="df1b2-126">**Получение центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="df1b2-127">**Обновление центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="df1b2-128">**Удаление центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="df1b2-129">Операции CRUD для регистрации</span><span class="sxs-lookup"><span data-stu-id="df1b2-129">Registration CRUDs</span></span>
<span data-ttu-id="df1b2-130">**Создание клиента центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="df1b2-131">**Создание регистрации Windows:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="df1b2-132">**Создание регистрации iOS:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="df1b2-133">Аналогичным образом можно создавать регистрации для Android (GCM), Windows Phone (MPNS) и Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="df1b2-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="df1b2-134">**Создание регистрации шаблона:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="df1b2-135">**Создание регистрации с помощью шаблона создания registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="df1b2-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="df1b2-136">Удаляет дубликаты из-за потери tooany ответы, если для хранения идентификаторов регистрации на устройстве hello:</span><span class="sxs-lookup"><span data-stu-id="df1b2-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="df1b2-137">**Обновление регистраций:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="df1b2-138">**Удаление регистраций:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="df1b2-139">**Запрос регистраций:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-139">**Query registrations:**</span></span>

* <span data-ttu-id="df1b2-140">**Получение одной регистрации:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="df1b2-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="df1b2-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="df1b2-142">**Получение всех регистраций в центре:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="df1b2-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="df1b2-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="df1b2-144">**Получение регистраций с тегом:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="df1b2-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="df1b2-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="df1b2-146">**Получение регистраций по каналу:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="df1b2-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="df1b2-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="df1b2-148">Все запросы коллекций поддерживают маркеры $top и маркеры продолжения.</span><span class="sxs-lookup"><span data-stu-id="df1b2-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="df1b2-149">Использование API установки</span><span class="sxs-lookup"><span data-stu-id="df1b2-149">Installation API usage</span></span>
<span data-ttu-id="df1b2-150">API установки — это альтернативный механизм управления регистрацией.</span><span class="sxs-lookup"><span data-stu-id="df1b2-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="df1b2-151">Вместо хранения нескольких регистраций, которым является непростой задачей и можно легко сделать неправильно или неэффективно, теперь стало возможно toouse объекта установки.</span><span class="sxs-lookup"><span data-stu-id="df1b2-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="df1b2-152">Установка включает в себя все необходимые составляющие: канал отправки (маркер устройства), теги, шаблоны и вспомогательные плитки (для WNS и APNS).</span><span class="sxs-lookup"><span data-stu-id="df1b2-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="df1b2-153">Больше не требуется toocall hello службы tooget идентификатор — просто сформировать идентификатор GUID или другие идентификаторы, сохранить его на устройстве и отправьте серверной tooyour вместе с канала push (маркер устройства).</span><span class="sxs-lookup"><span data-stu-id="df1b2-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="df1b2-154">На серверной hello следует делать, только один вызов: CreateOrUpdateInstallation, он является полностью идемпотентными, и вы можете бесплатно tooretry при необходимости.</span><span class="sxs-lookup"><span data-stu-id="df1b2-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="df1b2-155">Пример для Amazon Kindle Fire:</span><span class="sxs-lookup"><span data-stu-id="df1b2-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="df1b2-156">Если необходимо, чтобы tooupdate его:</span><span class="sxs-lookup"><span data-stu-id="df1b2-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="df1b2-157">Для сложных сценариев, у нас есть возможность частичное обновление, позволяющий toomodify hello объекта установки только определенных свойств.</span><span class="sxs-lookup"><span data-stu-id="df1b2-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="df1b2-158">В сущности, частичное обновление является подмножеством операций исправления JSON, которые можно запустить для объекта установки.</span><span class="sxs-lookup"><span data-stu-id="df1b2-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="df1b2-159">Удаление установки:</span><span class="sxs-lookup"><span data-stu-id="df1b2-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="df1b2-160">Операции CreateOrUpdate, Patch и Delete окончательно согласованы с операцией Get.</span><span class="sxs-lookup"><span data-stu-id="df1b2-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="df1b2-161">Запрошенную операцию просто перестает toohello системной очереди во время вызова hello и выполняется в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="df1b2-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="df1b2-162">Обратите внимание, что Get не предназначен для выполнения основных сценария, но только для отладки и устранения неполадок регулируется тесно службой hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="df1b2-163">Поток отправки для установки является hello то же, что для регистрации.</span><span class="sxs-lookup"><span data-stu-id="df1b2-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="df1b2-164">Мы только что ввели toohello уведомления tootarget параметр установки - тега, просто воспользуйтесь «InstallationId: {требуемого id}».</span><span class="sxs-lookup"><span data-stu-id="df1b2-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="df1b2-165">Для вышеупомянутых случаев это будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="df1b2-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="df1b2-166">Для одного из нескольких шаблонов:</span><span class="sxs-lookup"><span data-stu-id="df1b2-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="df1b2-167">Планирование уведомлений (доступно для уровня STANDARD)</span><span class="sxs-lookup"><span data-stu-id="df1b2-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="df1b2-168">Здравствуйте таким же, как обычный отправка, но один дополнительный параметр - scheduledTime, что когда уведомление должно быть доставлено.</span><span class="sxs-lookup"><span data-stu-id="df1b2-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="df1b2-169">Для отправки можно указать любое время в диапазоне «теперешнее время-5 минут» и «теперешнее время-7 дней».</span><span class="sxs-lookup"><span data-stu-id="df1b2-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="df1b2-170">**Планирование собственных уведомлений Windows:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="df1b2-171">Импорт или экспорт (доступно для уровня STANDARD)</span><span class="sxs-lookup"><span data-stu-id="df1b2-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="df1b2-172">Иногда бывает требуется tooperform массовой операции для регистрации.</span><span class="sxs-lookup"><span data-stu-id="df1b2-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="df1b2-173">Обычно используется для интеграции с другой системой или просто значительных исправление toosay обновления hello теги.</span><span class="sxs-lookup"><span data-stu-id="df1b2-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="df1b2-174">Если речь идет об тысячи регистраций toouse Get или обновления потока настоятельно не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="df1b2-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="df1b2-175">Возможность импорта и экспорта встречается спроектированный toocover hello.</span><span class="sxs-lookup"><span data-stu-id="df1b2-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="df1b2-176">По сути укажите контейнер больших двоичных объектов toosome доступа под учетной записью хранения как источник входящих данных и расположение для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="df1b2-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="df1b2-177">**Отправка задания экспорта:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="df1b2-178">**Отправка задания импорта:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="df1b2-179">**Ожидание завершения задания:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="df1b2-180">**Получение всех заданий:**</span><span class="sxs-lookup"><span data-stu-id="df1b2-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="df1b2-181">**URI с подписью SAS:** это URL-адрес hello некоторые файла BLOB-объект или контейнер больших двоичных объектов, а также набор параметров, таких как разрешения и время истечения срока действия, а также подпись следующие действия, выполненные с помощью ключа SAS для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="df1b2-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="df1b2-182">Пакет SDK для Java для службы хранилища Azure предоставляет широкие возможности, включая создание подобных универсальных кодов ресурса.</span><span class="sxs-lookup"><span data-stu-id="df1b2-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="df1b2-183">Простой альтернативой рассмотрим ImportExportE2E тестового класса (из расположения github hello) с очень основные и compact реализацию алгоритм подписи.</span><span class="sxs-lookup"><span data-stu-id="df1b2-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="df1b2-184">Отправка уведомлений</span><span class="sxs-lookup"><span data-stu-id="df1b2-184">Send Notifications</span></span>
<span data-ttu-id="df1b2-185">Hello объекта уведомления является просто текст с заголовками, помочь некоторые вспомогательные методы для построения объектов hello машинного кода и шаблон уведомления.</span><span class="sxs-lookup"><span data-stu-id="df1b2-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="df1b2-186">**Магазин Windows и Windows Phone 8.1 (без Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="df1b2-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="df1b2-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="df1b2-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="df1b2-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="df1b2-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="df1b2-189">**Windows Phone 8.0 и 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="df1b2-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="df1b2-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="df1b2-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="df1b2-191">**Отправить tooTags**</span><span class="sxs-lookup"><span data-stu-id="df1b2-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="df1b2-192">**Отправить tootag выражение**</span><span class="sxs-lookup"><span data-stu-id="df1b2-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="df1b2-193">**Отправка шаблонного уведомления**</span><span class="sxs-lookup"><span data-stu-id="df1b2-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="df1b2-194">После выполнения кода Java на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="df1b2-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="df1b2-195"><a name="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df1b2-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="df1b2-196">В этом разделе мы показали, как toocreate простой Java REST клиента для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="df1b2-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="df1b2-197">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="df1b2-197">From here you can:</span></span>

* <span data-ttu-id="df1b2-198">Загрузка полного hello [Java SDK], содержащего hello весь код, пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="df1b2-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="df1b2-199">Воспроизведение с образцами hello:</span><span class="sxs-lookup"><span data-stu-id="df1b2-199">Play with hello samples:</span></span>
  * <span data-ttu-id="df1b2-200">[Приступая к работе с центрами уведомлений]</span><span class="sxs-lookup"><span data-stu-id="df1b2-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="df1b2-201">[Отправка экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="df1b2-201">[Send breaking news]</span></span>
  * <span data-ttu-id="df1b2-202">[Отправка локализованных экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="df1b2-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="df1b2-203">[Отправлять уведомления пользователям tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="df1b2-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="df1b2-204">[Отправлять уведомления кросс платформенных tooauthenticated пользователей]</span><span class="sxs-lookup"><span data-stu-id="df1b2-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Приступая к работе с центрами уведомлений]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Отправка экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Отправка локализованных экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Отправлять уведомления пользователям tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Отправлять уведомления кросс платформенных tooauthenticated пользователей]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

