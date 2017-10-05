---
title: "Использование концентраторов уведомлений с Java"
description: "Узнайте, как использовать центры уведомлений Azure из серверной части Java."
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
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="46959-103">Использование концентраторов уведомлений из Java</span><span class="sxs-lookup"><span data-stu-id="46959-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="46959-104">В этой статье описаны основные функции нового, полностью поддерживаемого официального пакета SDK для Java Центра уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="46959-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="46959-105">Это проект с открытым исходным кодом. Вы можете просматривать весь код пакета SDK в образце [пакета SDK для Java].</span><span class="sxs-lookup"><span data-stu-id="46959-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="46959-106">Вы можете обращаться ко всем функциям центров уведомлений из серверной части Java/PHP/Python/Ruby, используя интерфейс REST в соответствии с описанием в разделе MSDN [Интерфейсы API REST центров уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="46959-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="46959-107">Пакет SDK для Java предоставляет тонкую оболочку для этих интерфейсов REST на Java.</span><span class="sxs-lookup"><span data-stu-id="46959-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="46959-108">В настоящее время пакет SDK поддерживает следующее:</span><span class="sxs-lookup"><span data-stu-id="46959-108">The SDK supports currently:</span></span>

* <span data-ttu-id="46959-109">операции CRUD для центра уведомлений;</span><span class="sxs-lookup"><span data-stu-id="46959-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="46959-110">операции CRUD для регистрации;</span><span class="sxs-lookup"><span data-stu-id="46959-110">CRUD on Registrations</span></span>
* <span data-ttu-id="46959-111">управление установкой;</span><span class="sxs-lookup"><span data-stu-id="46959-111">Installation Management</span></span>
* <span data-ttu-id="46959-112">регистрацию импорта и экспорта;</span><span class="sxs-lookup"><span data-stu-id="46959-112">Import/Export Registrations</span></span>
* <span data-ttu-id="46959-113">обычную отправку;</span><span class="sxs-lookup"><span data-stu-id="46959-113">Regular Sends</span></span>
* <span data-ttu-id="46959-114">запланированную отправку;</span><span class="sxs-lookup"><span data-stu-id="46959-114">Scheduled Sends</span></span>
* <span data-ttu-id="46959-115">асинхронные операции с использованием Java NIO;</span><span class="sxs-lookup"><span data-stu-id="46959-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="46959-116">Поддерживаемые платформы: APNS (iOS), GCM (Android), WNS (приложения для Магазина Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android без служб Google).</span><span class="sxs-lookup"><span data-stu-id="46959-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="46959-117">Использование пакета SDK</span><span class="sxs-lookup"><span data-stu-id="46959-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="46959-118">Компиляция и сборка</span><span class="sxs-lookup"><span data-stu-id="46959-118">Compile and build</span></span>
<span data-ttu-id="46959-119">Использование [Maven]</span><span class="sxs-lookup"><span data-stu-id="46959-119">Use [Maven]</span></span>

<span data-ttu-id="46959-120">для сборки:</span><span class="sxs-lookup"><span data-stu-id="46959-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="46959-121">Код</span><span class="sxs-lookup"><span data-stu-id="46959-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="46959-122">Операции CRUD в центрах уведомлений</span><span class="sxs-lookup"><span data-stu-id="46959-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="46959-123">**Создание NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="46959-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="46959-124">**Создание центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="46959-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="46959-125">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="46959-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="46959-126">**Получение центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="46959-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="46959-127">**Обновление центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="46959-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="46959-128">**Удаление центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="46959-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="46959-129">Операции CRUD для регистрации</span><span class="sxs-lookup"><span data-stu-id="46959-129">Registration CRUDs</span></span>
<span data-ttu-id="46959-130">**Создание клиента центра уведомлений:**</span><span class="sxs-lookup"><span data-stu-id="46959-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="46959-131">**Создание регистрации Windows:**</span><span class="sxs-lookup"><span data-stu-id="46959-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="46959-132">**Создание регистрации iOS:**</span><span class="sxs-lookup"><span data-stu-id="46959-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="46959-133">Аналогичным образом можно создавать регистрации для Android (GCM), Windows Phone (MPNS) и Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="46959-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="46959-134">**Создание регистрации шаблона:**</span><span class="sxs-lookup"><span data-stu-id="46959-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="46959-135">**Создание регистрации с помощью шаблона создания registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="46959-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="46959-136">Этот шаблон позволяет удалить повторы, образовавшиеся из-за потерянных ответов, если в устройстве хранятся идентификаторы регистрации:</span><span class="sxs-lookup"><span data-stu-id="46959-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="46959-137">**Обновление регистраций:**</span><span class="sxs-lookup"><span data-stu-id="46959-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="46959-138">**Удаление регистраций:**</span><span class="sxs-lookup"><span data-stu-id="46959-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="46959-139">**Запрос регистраций:**</span><span class="sxs-lookup"><span data-stu-id="46959-139">**Query registrations:**</span></span>

* <span data-ttu-id="46959-140">**Получение одной регистрации:**</span><span class="sxs-lookup"><span data-stu-id="46959-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="46959-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="46959-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="46959-142">**Получение всех регистраций в центре:**</span><span class="sxs-lookup"><span data-stu-id="46959-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="46959-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="46959-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="46959-144">**Получение регистраций с тегом:**</span><span class="sxs-lookup"><span data-stu-id="46959-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="46959-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="46959-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="46959-146">**Получение регистраций по каналу:**</span><span class="sxs-lookup"><span data-stu-id="46959-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="46959-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="46959-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="46959-148">Все запросы коллекций поддерживают маркеры $top и маркеры продолжения.</span><span class="sxs-lookup"><span data-stu-id="46959-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="46959-149">Использование API установки</span><span class="sxs-lookup"><span data-stu-id="46959-149">Installation API usage</span></span>
<span data-ttu-id="46959-150">API установки — это альтернативный механизм управления регистрацией.</span><span class="sxs-lookup"><span data-stu-id="46959-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="46959-151">Вместо поддержки нескольких регистраций, что является непростой задачей, которую зачастую выполняют неправильно или неэффективно, теперь можно использовать ЕДИНЫЙ объект установки.</span><span class="sxs-lookup"><span data-stu-id="46959-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="46959-152">Установка включает в себя все необходимые составляющие: канал отправки (маркер устройства), теги, шаблоны и вспомогательные плитки (для WNS и APNS).</span><span class="sxs-lookup"><span data-stu-id="46959-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="46959-153">Вам больше не нужно вызывать службу, чтобы получить идентификатор. Просто создайте GUID или любой другой идентификатор, сохраните его в устройстве и отправьте в серверную часть вместе с каналом отправки (маркером устройства).</span><span class="sxs-lookup"><span data-stu-id="46959-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="46959-154">На сервере нужно сделать всего один вызов: CreateOrUpdateInstallation. Он является полностью идемпотентным, поэтому при необходимости можно повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="46959-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="46959-155">Пример для Amazon Kindle Fire:</span><span class="sxs-lookup"><span data-stu-id="46959-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="46959-156">Если нужно обновление:</span><span class="sxs-lookup"><span data-stu-id="46959-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="46959-157">Для сложных сценариев можно выполнять частичное обновление, которое позволяет изменять только определенные свойства объекта установки.</span><span class="sxs-lookup"><span data-stu-id="46959-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="46959-158">В сущности, частичное обновление является подмножеством операций исправления JSON, которые можно запустить для объекта установки.</span><span class="sxs-lookup"><span data-stu-id="46959-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="46959-159">Удаление установки:</span><span class="sxs-lookup"><span data-stu-id="46959-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="46959-160">Операции CreateOrUpdate, Patch и Delete окончательно согласованы с операцией Get.</span><span class="sxs-lookup"><span data-stu-id="46959-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="46959-161">Запрошенная операция просто добавляется в системную очередь во время вызова и затем выполняется в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="46959-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="46959-162">Обратите внимание, что операция Get не предназначена для использования в основном сценарии среды выполнения. Она предусмотрена только для отладки и устранения неполадок и строго регулируется службой.</span><span class="sxs-lookup"><span data-stu-id="46959-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="46959-163">Поток отправки для установки аналогичен потоку отправки для регистрации.</span><span class="sxs-lookup"><span data-stu-id="46959-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="46959-164">Мы только что описали вариант направления уведомления к конкретному объекту установки. Для этого необходимо просто использовать тег InstallationId:{desired-id}.</span><span class="sxs-lookup"><span data-stu-id="46959-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="46959-165">Для вышеупомянутых случаев это будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="46959-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="46959-166">Для одного из нескольких шаблонов:</span><span class="sxs-lookup"><span data-stu-id="46959-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="46959-167">Планирование уведомлений (доступно для уровня STANDARD)</span><span class="sxs-lookup"><span data-stu-id="46959-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="46959-168">Такие уведомления отправляются обычным способом с использованием дополнительного параметра — scheduledTime, который определяет, когда нужно доставить уведомление.</span><span class="sxs-lookup"><span data-stu-id="46959-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="46959-169">Для отправки можно указать любое время в диапазоне «теперешнее время-5 минут» и «теперешнее время-7 дней».</span><span class="sxs-lookup"><span data-stu-id="46959-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="46959-170">**Планирование собственных уведомлений Windows:**</span><span class="sxs-lookup"><span data-stu-id="46959-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="46959-171">Импорт или экспорт (доступно для уровня STANDARD)</span><span class="sxs-lookup"><span data-stu-id="46959-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="46959-172">Иногда требуется выполнить массовую операцию регистрации.</span><span class="sxs-lookup"><span data-stu-id="46959-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="46959-173">Обычно это необходимо для интеграции с другой системой или для внесения значительных исправлений, например для обновления тегов.</span><span class="sxs-lookup"><span data-stu-id="46959-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="46959-174">Мы настоятельно рекомендуем не использовать поток Get или Update, если речь идет о тысячах операций регистрации.</span><span class="sxs-lookup"><span data-stu-id="46959-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="46959-175">Возможность импорта или экспорта разработана для поддержки сценария.</span><span class="sxs-lookup"><span data-stu-id="46959-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="46959-176">В сущности, вы предоставляете доступ к определенному контейнеру больших двоичных объектов в вашей учетной записи хранения в качестве источника входящих данных и расположения для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="46959-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="46959-177">**Отправка задания экспорта:**</span><span class="sxs-lookup"><span data-stu-id="46959-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="46959-178">**Отправка задания импорта:**</span><span class="sxs-lookup"><span data-stu-id="46959-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="46959-179">**Ожидание завершения задания:**</span><span class="sxs-lookup"><span data-stu-id="46959-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="46959-180">**Получение всех заданий:**</span><span class="sxs-lookup"><span data-stu-id="46959-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="46959-181">**URI с подписью SAS** — это URL-адрес определенного файла большого двоичного объекта или контейнера больших двоичных объектов в сочетании с набором параметров, таких как разрешения и сроки действия, и подписью всех этих элементов, выполненной с использованием ключа подписанного URL-адреса учетной записи.</span><span class="sxs-lookup"><span data-stu-id="46959-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="46959-182">Пакет SDK для Java для службы хранилища Azure предоставляет широкие возможности, включая создание подобных универсальных кодов ресурса.</span><span class="sxs-lookup"><span data-stu-id="46959-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="46959-183">В качестве простой альтернативы рассмотрим класс теста ImportExportE2E (из расположения github) с базовой компактной реализацией алгоритма подписи.</span><span class="sxs-lookup"><span data-stu-id="46959-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="46959-184">Отправка уведомлений</span><span class="sxs-lookup"><span data-stu-id="46959-184">Send Notifications</span></span>
<span data-ttu-id="46959-185">Объект уведомления — это основной текст с заголовками. С помощью методов, предоставляемых некоторыми служебными программами, можно создать собственные и шаблонные объекты уведомлений.</span><span class="sxs-lookup"><span data-stu-id="46959-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="46959-186">**Магазин Windows и Windows Phone 8.1 (без Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="46959-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="46959-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="46959-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="46959-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="46959-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="46959-189">**Windows Phone 8.0 и 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="46959-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="46959-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="46959-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="46959-191">**Отправка к тегам**</span><span class="sxs-lookup"><span data-stu-id="46959-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="46959-192">**Отправка к выражению тега**</span><span class="sxs-lookup"><span data-stu-id="46959-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="46959-193">**Отправка шаблонного уведомления**</span><span class="sxs-lookup"><span data-stu-id="46959-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="46959-194">После выполнения кода Java на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="46959-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="46959-195"><a name="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46959-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="46959-196">В этом разделе было показано, как создать простой клиент Java REST для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="46959-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="46959-197">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="46959-197">From here you can:</span></span>

* <span data-ttu-id="46959-198">Скачайте полный [пакета SDK для Java], содержащий весь код пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="46959-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="46959-199">Попробуйте разные примеры:</span><span class="sxs-lookup"><span data-stu-id="46959-199">Play with the samples:</span></span>
  * <span data-ttu-id="46959-200">[Приступая к работе с центрами уведомлений]</span><span class="sxs-lookup"><span data-stu-id="46959-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="46959-201">[Отправка экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="46959-201">[Send breaking news]</span></span>
  * <span data-ttu-id="46959-202">[Отправка локализованных экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="46959-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="46959-203">[Отправка уведомлений проверенным пользователям]</span><span class="sxs-lookup"><span data-stu-id="46959-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="46959-204">[Отправка кроссплатформенных уведомлений проверенным пользователям]</span><span class="sxs-lookup"><span data-stu-id="46959-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="46959-205">[пакета SDK для Java]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="46959-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="46959-206">[Приступая к работе с центрами уведомлений]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="46959-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="46959-207">[Отправка экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="46959-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="46959-208">[Отправка локализованных экстренных новостей]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="46959-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="46959-209">[Отправка уведомлений проверенным пользователям]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="46959-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="46959-210">[Отправка кроссплатформенных уведомлений проверенным пользователям]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="46959-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="46959-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="46959-211">[Maven]: http://maven.apache.org/</span></span>

