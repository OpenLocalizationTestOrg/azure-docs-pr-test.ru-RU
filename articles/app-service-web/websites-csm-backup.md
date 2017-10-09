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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Использование REST tooback и восстановление приложения служб приложений
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [ИНТЕРФЕЙС REST API](websites-csm-backup.md)
> 
> 

[приложений службы приложений](https://azure.microsoft.com/services/app-service/web/) можно создавать резервную копию в виде больших двоичных объектов в хранилище Azure. резервное копирование Hello также может содержать приложение hello баз данных. Если приложение hello-либо случайно удален, или если toobe потребностей приложения hello восстановлен tooa предыдущей версии, его можно восстановить из любой предыдущей резервной копии. Резервное копирование может выполняться по запросу в любое время или по расписанию с нужными интервалами.

В этой статье объясняется, как toobackup и восстановление приложения с помощью RESTful API запросов. Если бы как toocreate и управлять резервными копиями приложения графически через hello портал Azure, см. раздел [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Приступая к работе
запрашивает toosend REST, необходимо tooknow приложения **имя**, **группы ресурсов**, и **идентификатор подписки**. Эти сведения можно найти, щелкнув приложение hello **службы приложений** колонке hello [портал Azure](https://portal.azure.com). Примеры hello в этой статье, настраиваете веб-сайт hello **backuprestoreapiexamples.azurewebsites.net**. Он хранится в группе ресурсов по умолчанию-Web-WestUS hello и работает на подписку с Идентификатором 00001111-2222-3333-4444-555566667777 hello.

![Пример информации о веб-сайте][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>REST API архивации и восстановления
Теперь мы рассмотрим несколько примеров того, как toouse hello toobackup API-Интерфейс REST и восстановить приложение. Каждый пример содержит URL-адрес и текст HTTP-запроса. URL-адрес образца Hello содержит заполнители, заключенного в фигурные скобки, например {код_подписки}. Замените заполнители hello hello соответствующие сведения для вашего приложения. Для ссылки здесь приведено пояснение для каждого заполнитель, который отображается в URL-адресах пример hello.

* Подписка id — идентификатор содержащего приложения hello hello подписки Azure
* Resource-group-name — имя содержащего приложение hello hello ресурсов группы
* имя — имя приложения hello
* резервное копирование id — идентификатор копии приложения hello

Hello полную документацию по hello API, включая несколько необязательных параметров, которые могут быть включены в запрос hello HTTP см. в hello [обозревателя ресурсов Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Резервное копирование приложения по требованию
tooback копирование приложение немедленно, отправить **POST** запроса слишком**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ резервного копирования или**.

Здесь будет hello URL-адрес выглядеть наш пример веб-сайте. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Укажите объект JSON в тексте hello toospecify ваш запрос, какие toostore toouse учетной записи хранилища hello резервного копирования. Hello объекта JSON должен иметь свойство с именем **storageAccountUrl**, который содержит [URL-адрес SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) предоставление доступа на запись toohello хранилища Azure контейнер, хранящий hello большого двоичного объекта. Если требуется tooback копии баз данных, необходимо также указать список, содержащий hello имена, типы и строки подключения из toobe hello баз данных, резервное копирование.

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

Резервная копия приложение hello начинается немедленно при получении запроса hello. Hello резервного копирования может занять длительное время toocomplete. Hello HTTP-ответа содержит идентификатор, который можно использовать в другой запрос toosee hello состояние hello операции резервного копирования. Ниже приведен пример текста hello hello HTTP-ответа tooour резервного копирования запроса.

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
> Сообщения об ошибках можно найти в свойстве журнала hello hello HTTP-ответа.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Планирование автоматического резервного копирования
В добавление toobacking копии приложения по требованию можно также запланировать резервного копирования toohappen автоматически.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Создание расписания автоматического резервного копирования
Отправить tooset расписание резервного копирования, **ПОМЕСТИТЬ** запроса слишком**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config и резервного копирования**.

Вот, как выглядит hello URL-адрес для наших пример веб-сайта. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

Hello текст запроса должен иметь объект JSON, который указывает hello конфигурации резервного копирования. Ниже приведен пример со всеми параметрами необходимые hello.

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

В этом примере настраивается toobe приложения hello, автоматическое резервное копирование каждые семь дней. Здравствуйте, параметры **frequencyInterval** и **frequencyUnit** вместе определяют, как часто hello резервное копирование осуществляется. Допустимые значения для **frequencyUnit** — **hour** (час) и **day** (день). Например tooback копии приложения через каждые 12 часов, задайте frequencyInterval too12 и frequencyUnit toohour.

Старые резервные копии, автоматически удаляются из учетной записи хранения hello. Можно управлять как старый hello резервных копий может быть с помощью параметра hello **retentionPeriodInDays** параметра. Если требуется tooalways иметь хотя бы один архив сохранен, независимо от того, как старый установлено **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Получить hello автоматической архивации по расписанию
tooget приложения резервное копирование конфигурации, отправить **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ узлы / {имя} / config/резервной копии или списка**.

Hello URL-адрес сайта нашем примере — **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Получить состояние hello резервной копии
В зависимости от размера приложения hello является, резервной копии может занять некоторое время toocomplete. Более того, процесс копирования может завершиться ошибкой, прекратиться по истечении времени ожидания или оказаться частично выполненным. Отправить состояние hello toosee копий приложения **получить** toohello URL-адрес запроса **/providers/ https://management.azure.com/subscriptions/ {код_подписки} /resourceGroups/ {resource-group-name} Microsoft.Web/sites/{name}/backups**.

состояние hello toosee заданной резервной копии, отправить запрос GET toohello URL-адрес **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { резервное копирование id}**.

Вот, как выглядит hello URL-адрес для наших пример веб-сайта. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

текст ответа Hello содержит объект JSON аналогичный пример toothis.

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

Перечислимый тип находится в состоянии Hello резервной копии. Вот все возможные значения состояния:

* 0 — InProgress: hello резервное копирование было начато, но еще не завершено.
* 1 — окончился неудачей: hello Архивация завершилась со сбоем.
* 2 — успешно выполнено: hello Архивация выполнена успешно.
* 3 — TimedOut: hello резервная копия не была завершена в момент и была отменена.
* 4 — созданы: hello резервного копирования запрос помещается в очередь, но не была запущена.
* 5 — пропущено: hello резервной копии не удастся из-за tooa расписание запуска слишком много резервных копий.
* 6 — PartiallySucceeded: hello резервное копирование выполнено успешно, но некоторые файлы не были сохранены, так как они не удалось прочитать. Обычно это происходит, поскольку монопольная блокировка была размещена на файлы hello.
* 7 – DeleteInProgress: hello резервная копия была запрошенный toobe удалены, но еще не было удалено.
* 8 – DeleteFailed: не удалось удалить hello резервного копирования. Это может произойти, поскольку истек срок действия hello URL-адрес SAS, резервного копирования используется toocreate hello.
* 9 — удалены: hello резервного копирования успешно удален.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Восстановление приложения из резервной копии
Если приложения была удалена, или если требуется toorevert tooa предыдущую версию приложения, приложение hello можно восстановить из резервной копии. Отправить tooinvoke восстановления **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ резервное копирование / {backup-id} / restore**.

Вот, как выглядит hello URL-адрес для наших пример веб-сайта. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

В тексте запроса hello отправьте объект JSON, содержащий свойства hello для операции восстановления hello. Вот пример, содержащий все обязательные свойства:

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

### <a name="restore-tooa-new-app"></a>Восстановление tooa нового приложения
Иногда возникает необходимость toocreate новое приложение при восстановлении резервной копии, вместо перезаписи уже существующего приложения. toodo, изменение запроса URL-адрес toopoint toohello новое приложение hello toocreate и изменить hello **перезаписать** свойство в hello JSON слишком**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Удаление резервной копии приложения
При желании toodelete резервной копии отправки **удаление** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ узлы / {имя} {backup-id} /backups/**.

Вот, как выглядит hello URL-адрес для наших пример веб-сайта. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Управление URL-адресом SAS резервной копии
Служба приложений Azure попытается toodelete резервную копию в хранилище Azure с помощью URL-адрес, предоставленный при создании резервной копии hello hello. Если этот URL-адрес SAS больше не является допустимым, нельзя удалить hello резервного копирования через hello REST API. Тем не менее, можно обновить URL-адрес SAS связанные с резервным копированием, отправляя hello **POST** toohello URL-адрес запроса **https://management.azure.com/subscriptions/ {код_подписки} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Вот, как выглядит hello URL-адрес для наших пример веб-сайта. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

В тексте запроса hello отправьте объект JSON, содержащий hello новый URL-адрес SAS. Ниже приведен пример.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> По соображениям безопасности hello URL-адрес SAS, связанного с помощью резервной копии не возвращается при отправке запроса GET для заданной резервной копии. Hello tooview URL-адрес SAS связанные с резервным копированием, отправьте запрос POST toohello же URL-адрес выше. Включите пустой объект JSON в теле запроса hello. Hello ответа от сервера hello содержит все сведения этой резервной копии, включая его URL-адрес SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
