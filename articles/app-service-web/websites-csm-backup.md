---
title: "aaaUse REST tooback копирование и восстановление приложения служб приложений"
description: "Узнайте, как toouse RESTful API вызывает tooback и восстановление приложения в службе приложений Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="e3439-103">Использование REST tooback и восстановление приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="e3439-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3439-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3439-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="e3439-105">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="e3439-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="e3439-106">[приложений службы приложений](https://azure.microsoft.com/services/app-service/web/) можно создавать резервную копию в виде больших двоичных объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="e3439-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="e3439-107">резервное копирование Hello также может содержать приложение hello баз данных.</span><span class="sxs-lookup"><span data-stu-id="e3439-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="e3439-108">Если приложение hello-либо случайно удален, или если toobe потребностей приложения hello восстановлен tooa предыдущей версии, его можно восстановить из любой предыдущей резервной копии.</span><span class="sxs-lookup"><span data-stu-id="e3439-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="e3439-109">Резервное копирование может выполняться по запросу в любое время или по расписанию с нужными интервалами.</span><span class="sxs-lookup"><span data-stu-id="e3439-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="e3439-110">В этой статье объясняется, как toobackup и восстановление приложения с помощью RESTful API запросов.</span><span class="sxs-lookup"><span data-stu-id="e3439-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="e3439-111">Если бы как toocreate и управлять резервными копиями приложения графически через hello портал Azure, см. раздел [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="e3439-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="e3439-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="e3439-112">Getting Started</span></span>
<span data-ttu-id="e3439-113">запрашивает toosend REST, необходимо tooknow приложения **имя**, **группы ресурсов**, и **идентификатор подписки**. Эти сведения можно найти, щелкнув приложение hello **службы приложений** колонке hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3439-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e3439-114">Примеры hello в этой статье, настраиваете веб-сайт hello **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="e3439-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="e3439-115">Он хранится в группе ресурсов по умолчанию-Web-WestUS hello и работает на подписку с Идентификатором 00001111-2222-3333-4444-555566667777 hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Пример информации о веб-сайте][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="e3439-117">REST API архивации и восстановления</span><span class="sxs-lookup"><span data-stu-id="e3439-117">Backup and restore REST API</span></span>
<span data-ttu-id="e3439-118">Теперь мы рассмотрим несколько примеров того, как toouse hello toobackup API-Интерфейс REST и восстановить приложение.</span><span class="sxs-lookup"><span data-stu-id="e3439-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="e3439-119">Каждый пример содержит URL-адрес и текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="e3439-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="e3439-120">URL-адрес образца Hello содержит заполнители, заключенного в фигурные скобки, например {код_подписки}.</span><span class="sxs-lookup"><span data-stu-id="e3439-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="e3439-121">Замените заполнители hello hello соответствующие сведения для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e3439-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="e3439-122">Для ссылки здесь приведено пояснение для каждого заполнитель, который отображается в URL-адресах пример hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="e3439-123">Подписка id — идентификатор содержащего приложения hello hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="e3439-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="e3439-124">Resource-group-name — имя содержащего приложение hello hello ресурсов группы</span><span class="sxs-lookup"><span data-stu-id="e3439-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="e3439-125">имя — имя приложения hello</span><span class="sxs-lookup"><span data-stu-id="e3439-125">name – Name of hello app</span></span>
* <span data-ttu-id="e3439-126">резервное копирование id — идентификатор копии приложения hello</span><span class="sxs-lookup"><span data-stu-id="e3439-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="e3439-127">Hello полную документацию по hello API, включая несколько необязательных параметров, которые могут быть включены в запрос hello HTTP см. в hello [обозревателя ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e3439-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="e3439-128">Резервное копирование приложения по требованию</span><span class="sxs-lookup"><span data-stu-id="e3439-128">Backup an app on demand</span></span>
<span data-ttu-id="e3439-129">tooback копирование приложение немедленно, отправить **POST** запроса слишком**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ резервного копирования или**.</span><span class="sxs-lookup"><span data-stu-id="e3439-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="e3439-130">Здесь будет hello URL-адрес выглядеть наш пример веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="e3439-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="e3439-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="e3439-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="e3439-132">Укажите объект JSON в тексте hello toospecify ваш запрос, какие toostore toouse учетной записи хранилища hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e3439-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="e3439-133">Hello объекта JSON должен иметь свойство с именем **storageAccountUrl**, который содержит [URL-адрес SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) предоставление доступа на запись toohello хранилища Azure контейнер, хранящий hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="e3439-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="e3439-134">Если требуется tooback копии баз данных, необходимо также указать список, содержащий hello имена, типы и строки подключения из toobe hello баз данных, резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="e3439-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="e3439-135">Резервная копия приложение hello начинается немедленно при получении запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="e3439-136">Hello резервного копирования может занять длительное время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e3439-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="e3439-137">Hello HTTP-ответа содержит идентификатор, который можно использовать в другой запрос toosee hello состояние hello операции резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e3439-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="e3439-138">Ниже приведен пример текста hello hello HTTP-ответа tooour резервного копирования запроса.</span><span class="sxs-lookup"><span data-stu-id="e3439-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="e3439-139">Сообщения об ошибках можно найти в свойстве журнала hello hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="e3439-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="e3439-140">Планирование автоматического резервного копирования</span><span class="sxs-lookup"><span data-stu-id="e3439-140">Schedule automatic backups</span></span>
<span data-ttu-id="e3439-141">В добавление toobacking копии приложения по требованию можно также запланировать резервного копирования toohappen автоматически.</span><span class="sxs-lookup"><span data-stu-id="e3439-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="e3439-142">Создание расписания автоматического резервного копирования</span><span class="sxs-lookup"><span data-stu-id="e3439-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="e3439-143">Отправить tooset расписание резервного копирования, **ПОМЕСТИТЬ** запроса слишком**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config и резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="e3439-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="e3439-144">Вот, как выглядит hello URL-адрес для наших пример веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e3439-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="e3439-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="e3439-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="e3439-146">Hello текст запроса должен иметь объект JSON, который указывает hello конфигурации резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e3439-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="e3439-147">Ниже приведен пример со всеми параметрами необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="e3439-148">В этом примере настраивается toobe приложения hello, автоматическое резервное копирование каждые семь дней.</span><span class="sxs-lookup"><span data-stu-id="e3439-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="e3439-149">Здравствуйте, параметры **frequencyInterval** и **frequencyUnit** вместе определяют, как часто hello резервное копирование осуществляется.</span><span class="sxs-lookup"><span data-stu-id="e3439-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="e3439-150">Допустимые значения для **frequencyUnit** — **hour** (час) и **day** (день).</span><span class="sxs-lookup"><span data-stu-id="e3439-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="e3439-151">Например tooback копии приложения через каждые 12 часов, задайте frequencyInterval too12 и frequencyUnit toohour.</span><span class="sxs-lookup"><span data-stu-id="e3439-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="e3439-152">Старые резервные копии, автоматически удаляются из учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="e3439-153">Можно управлять как старый hello резервных копий может быть с помощью параметра hello **retentionPeriodInDays** параметра.</span><span class="sxs-lookup"><span data-stu-id="e3439-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="e3439-154">Если требуется tooalways иметь хотя бы один архив сохранен, независимо от того, как старый установлено **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="e3439-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="e3439-155">Получить hello автоматической архивации по расписанию</span><span class="sxs-lookup"><span data-stu-id="e3439-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="e3439-156">tooget приложения резервное копирование конфигурации, отправить **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ узлы / {имя} / config/резервной копии или списка**.</span><span class="sxs-lookup"><span data-stu-id="e3439-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="e3439-157">Hello URL-адрес сайта нашем примере — **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="e3439-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="e3439-158">Получить состояние hello резервной копии</span><span class="sxs-lookup"><span data-stu-id="e3439-158">Get hello status of a backup</span></span>
<span data-ttu-id="e3439-159">В зависимости от размера приложения hello является, резервной копии может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e3439-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="e3439-160">Более того, процесс копирования может завершиться ошибкой, прекратиться по истечении времени ожидания или оказаться частично выполненным.</span><span class="sxs-lookup"><span data-stu-id="e3439-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="e3439-161">Отправить состояние hello toosee копий приложения **получить** toohello URL-адрес запроса **/providers/ https://management.azure.com/subscriptions/ {код_подписки} /resourceGroups/ {resource-group-name} Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="e3439-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="e3439-162">состояние hello toosee заданной резервной копии, отправить запрос GET toohello URL-адрес **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { резервное копирование id}**.</span><span class="sxs-lookup"><span data-stu-id="e3439-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="e3439-163">Вот, как выглядит hello URL-адрес для наших пример веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e3439-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="e3439-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="e3439-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="e3439-165">текст ответа Hello содержит объект JSON аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="e3439-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="e3439-166">Перечислимый тип находится в состоянии Hello резервной копии.</span><span class="sxs-lookup"><span data-stu-id="e3439-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="e3439-167">Вот все возможные значения состояния:</span><span class="sxs-lookup"><span data-stu-id="e3439-167">Here is every possible state.</span></span>

* <span data-ttu-id="e3439-168">0 — InProgress: hello резервное копирование было начато, но еще не завершено.</span><span class="sxs-lookup"><span data-stu-id="e3439-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="e3439-169">1 — окончился неудачей: hello Архивация завершилась со сбоем.</span><span class="sxs-lookup"><span data-stu-id="e3439-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="e3439-170">2 — успешно выполнено: hello Архивация выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="e3439-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="e3439-171">3 — TimedOut: hello резервная копия не была завершена в момент и была отменена.</span><span class="sxs-lookup"><span data-stu-id="e3439-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="e3439-172">4 — созданы: hello резервного копирования запрос помещается в очередь, но не была запущена.</span><span class="sxs-lookup"><span data-stu-id="e3439-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="e3439-173">5 — пропущено: hello резервной копии не удастся из-за tooa расписание запуска слишком много резервных копий.</span><span class="sxs-lookup"><span data-stu-id="e3439-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="e3439-174">6 — PartiallySucceeded: hello резервное копирование выполнено успешно, но некоторые файлы не были сохранены, так как они не удалось прочитать.</span><span class="sxs-lookup"><span data-stu-id="e3439-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="e3439-175">Обычно это происходит, поскольку монопольная блокировка была размещена на файлы hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="e3439-176">7 – DeleteInProgress: hello резервная копия была запрошенный toobe удалены, но еще не было удалено.</span><span class="sxs-lookup"><span data-stu-id="e3439-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="e3439-177">8 – DeleteFailed: не удалось удалить hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="e3439-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="e3439-178">Это может произойти, поскольку истек срок действия hello URL-адрес SAS, резервного копирования используется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="e3439-179">9 — удалены: hello резервного копирования успешно удален.</span><span class="sxs-lookup"><span data-stu-id="e3439-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="e3439-180">Восстановление приложения из резервной копии</span><span class="sxs-lookup"><span data-stu-id="e3439-180">Restore an app from a backup</span></span>
<span data-ttu-id="e3439-181">Если приложения была удалена, или если требуется toorevert tooa предыдущую версию приложения, приложение hello можно восстановить из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="e3439-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="e3439-182">Отправить tooinvoke восстановления **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ резервное копирование / {backup-id} / restore**.</span><span class="sxs-lookup"><span data-stu-id="e3439-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="e3439-183">Вот, как выглядит hello URL-адрес для наших пример веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e3439-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="e3439-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="e3439-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="e3439-185">В тексте запроса hello отправьте объект JSON, содержащий свойства hello для операции восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="e3439-186">Вот пример, содержащий все обязательные свойства:</span><span class="sxs-lookup"><span data-stu-id="e3439-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="e3439-187">Восстановление tooa нового приложения</span><span class="sxs-lookup"><span data-stu-id="e3439-187">Restore tooa new app</span></span>
<span data-ttu-id="e3439-188">Иногда возникает необходимость toocreate новое приложение при восстановлении резервной копии, вместо перезаписи уже существующего приложения.</span><span class="sxs-lookup"><span data-stu-id="e3439-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="e3439-189">toodo, изменение запроса URL-адрес toopoint toohello новое приложение hello toocreate и изменить hello **перезаписать** свойство в hello JSON слишком**false**.</span><span class="sxs-lookup"><span data-stu-id="e3439-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="e3439-190">Удаление резервной копии приложения</span><span class="sxs-lookup"><span data-stu-id="e3439-190">Delete an app backup</span></span>
<span data-ttu-id="e3439-191">При желании toodelete резервной копии отправки **удаление** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ узлы / {имя} {backup-id} /backups/**.</span><span class="sxs-lookup"><span data-stu-id="e3439-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="e3439-192">Вот, как выглядит hello URL-адрес для наших пример веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e3439-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="e3439-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="e3439-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="e3439-194">Управление URL-адресом SAS резервной копии</span><span class="sxs-lookup"><span data-stu-id="e3439-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="e3439-195">Служба приложений Azure попытается toodelete резервную копию в хранилище Azure с помощью URL-адрес, предоставленный при создании резервной копии hello hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="e3439-196">Если этот URL-адрес SAS больше не является допустимым, нельзя удалить hello резервного копирования через hello REST API.</span><span class="sxs-lookup"><span data-stu-id="e3439-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="e3439-197">Тем не менее, можно обновить URL-адрес SAS связанные с резервным копированием, отправляя hello **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {код_подписки} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="e3439-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="e3439-198">Вот, как выглядит hello URL-адрес для наших пример веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e3439-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="e3439-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="e3439-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="e3439-200">В тексте запроса hello отправьте объект JSON, содержащий hello новый URL-адрес SAS.</span><span class="sxs-lookup"><span data-stu-id="e3439-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="e3439-201">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="e3439-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="e3439-202">По соображениям безопасности hello URL-адрес SAS, связанного с помощью резервной копии не возвращается при отправке запроса GET для заданной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="e3439-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="e3439-203">Hello tooview URL-адрес SAS связанные с резервным копированием, отправьте запрос POST toohello же URL-адрес выше.</span><span class="sxs-lookup"><span data-stu-id="e3439-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="e3439-204">Включите пустой объект JSON в теле запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e3439-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="e3439-205">Hello ответа от сервера hello содержит все сведения этой резервной копии, включая его URL-адрес SAS.</span><span class="sxs-lookup"><span data-stu-id="e3439-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
