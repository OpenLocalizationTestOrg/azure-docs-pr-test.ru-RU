---
title: "aaaHow tooencode актива Azure с помощью Media Encoder стандартные | Документы Microsoft"
description: "Узнайте, как стандартный кодировщик мультимедиа media tooencode toouse содержимого служб мультимедиа Azure. В примерах кода используется REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Как tooencode актива с помощью стандартных кодировщика мультимедиа
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Портал](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Обзор
toodeliver цифрового видео по Интернету hello, необходимо сжать мультимедиа hello. Цифровые видеофайлы велики и может быть слишком большой toodeliver по hello Интернет или для клиентов устройств toodisplay должным образом. Кодирование-это процесс сжатия видео и аудио, чтобы ваши клиенты могли просмотреть мультимедиа hello.

Задания кодирования — это один из самых распространенных операций обработки hello в службах мультимедиа Azure. Создать кодирования файлов мультимедиа tooconvert заданий из одной кодировки tooanother. При кодировании можно использовать hello служб мультимедиа встроенный кодировщик (стандартный кодировщик мультимедиа). Можно также использовать кодировщик, предоставленный партнером служб мультимедиа. Сторонние кодировщики можно найти hello Azure Marketplace. Можно указать hello данные задач кодирования, используя предустановленные строки, заданные для кодировщика или используя предустановленные файлы конфигурации. toosee hello типов наборов параметров, доступных в разделе [предустановки задачи для Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).

Каждое задание может включать один или несколько задач в зависимости от типа hello обработки, которую хотите tooaccomplish. Через hello REST API можно создать задания и связанные задачи одним из двух способов:

* Задачи могут быть определен как встроенный через hello свойства навигации Tasks объекта сущности задания.
* можно использовать пакетную обработку OData.

Рекомендуется всегда кодировать исходные файлы в набор MP4 с адаптивной скоростью, а затем преобразовать hello набор toohello нужный формат с помощью [динамической упаковки](media-services-dynamic-packaging-overview.md).

Если выходной актив является зашифрованного в хранилище, необходимо настроить политику доставки актива hello. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Рекомендации

При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах. Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).

Прежде чем начать, ссылающиеся на обработчики мультимедиа, убедитесь, что имеют hello идентификатор правильный носитель процессора. Дополнительные сведения см. в статье [Получение экземпляра процессора мультимедиа](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Подключение служб tooMedia

Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Создание задания с одной задачей кодирования
> [!NOTE]
> При работе с API REST служб мультимедиа hello hello действуют следующие ограничения.
>
> При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах. Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).
>
> После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI. Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> При использовании JSON и указав toouse hello **__metadata** ключевое слово в запросе hello (например, tooreferences связанный объект), необходимо задать hello **Accept** заголовок слишком[JSON в подробном формате ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Принять: приложение/json; odata = подробных сведений.
>
>

Hello в следующем примере показано, как toocreate и post задание с одной задачи набор tooencode видео с определенным разрешением и качества. При кодировании с помощью Media Encoder Standard вы можете использовать предустановки конфигурации задач, указанные [здесь](http://msdn.microsoft.com/library/mt269960).

Запрос:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Ответ:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Задайте имя выходного актива hello
Привет, в следующем примере показано, как tooset hello атрибута assetName:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Рекомендации
* Свойства TaskBody должны использовать числовой литерал XML toodefine hello ввода или вывода ресурсы, которые используются задачей «hello». раздел задача Hello содержит hello определения схемы XML для hello XML.
* В hello TaskBody определение каждого внутреннее значение атрибута <inputAsset> и <outputAsset> должен быть задан как JobInputAsset(value) или JobOutputAsset(value).
* В задаче может содержаться несколько выходных ресурсов. Значение JobOutputAsset(x) может использоваться только один раз в качестве выходных данных задачи в задании.
* В качестве входного ресурса задачи можно указать JobInputAsset или JobOutputAsset.
* Задачи не должны образовывать цикл.
* значение параметра Hello передается tooJobInputAsset или JobOutputAsset представляет hello значение индекса для актива. Hello фактические ресурсы определяются в hello InputMediaAssets и OutputMediaAssets свойства навигации в определении объекта job hello.
* Поскольку службы мультимедиа разработаны на основе OData v3, hello отдельные ресурсы в hello InputMediaAssets и коллекциях свойств навигации OutputMediaAssets указываются с помощью «__metadata: uri» пары "имя значение".
* Объекты InputMediaAssets сопоставляются tooone или несколько ресурсов, созданные в службах мультимедиа. Объекты OutputMediaAssets создаются системой hello. Они не ссылаются на существующий ресурс.
* Может иметь имя OutputMediaAssets с помощью атрибута assetName hello. Если этот атрибут не задан, то имя hello hello объекта OutputMediaAsset будет любое значение внутренний текст hello hello <outputAsset> существует элемент с суффиксом hello имя задания значение или значение идентификатора задания hello (в случае hello, где свойство Name hello не определено). Например если задать значение для assetName слишком «Пример», а затем задать свойство Name объекта OutputMediaAsset hello слишком «Sample.» Тем не менее если не задать значение для assetName, но был указан hello имя задания слишком «NewJob», а затем hello Name объекта OutputMediaAsset будет «JobOutputAsset (значение) _NewJob».

## <a name="create-a-job-with-chained-tasks"></a>Создание задания с цепными задачами
Во многих сценариях приложений разработчики должны toocreate ряд задач обработки. В службах мультимедиа вы можете создавать серии цепных задач. Каждая задача выполняет разные шаги обработки. Эти задачи также могут использовать разные обработчики мультимедиа. Hello связанных задач можно передавать актив из одной задачи tooanother, выполняя линейную последовательность задач в активе hello. Однако hello задачи, выполняемые в задании не требуется toobe в последовательности. При создании связанной задачи связанные hello **ITask** объекты создаются в одном **IJob** объекта.

> [!NOTE]
> Сейчас количество задач ограничено 30 задачами на задание. Если требуется более 30 задач toochain создайте более чем одному заданию toocontain hello задачи.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Рекомендации
tooenable цепочки задач:

* в задании должно быть по крайней мере две задачи;
* Должен существовать хотя бы одна задача, входные данные — hello выходными данными другой задачи в задании hello.

## <a name="use-odata-batch-processing"></a>Использование пакетной обработки OData
Hello в следующем примере показано, как toouse OData пакетной обработки toocreate задания и задачи. Чтобы узнать больше о пакетной обработке, ознакомьтесь с [пакетной обработкой посредством протокола OData](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Создание задания с помощью сущности JobTemplate
При обработке нескольких активов с помощью общего набора задач, используйте стили задачу по умолчанию hello toospecify JobTemplate или tooset hello порядка задач.

Привет, в следующем примере показан способ toocreate JobTemplate с TaskTemplate, который является встроенной. Hello TaskTemplate использует стандартный кодировщик мультимедиа hello как файл актива hello tooencode обработчика мультимедиа hello. Но также можно использовать и другие обработчики.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> В отличие от других сущностей служб мультимедиа необходимо определить новый идентификатор GUID для каждого шаблона TaskTemplate и поместите его в свойства hello taskTemplateId и Id в тексте запроса. Схема идентификации контента Hello должны соответствовать схеме hello, описанной в идентификации сущностей служб мультимедиа Azure. Кроме того, сущности JobTemplates нельзя обновлять. Вместо этого необходимо создавать новые сущности с необходимыми изменениями.
>
>

В случае успешного выполнения возвращается следующий ответ hello:

    HTTP/1.1 201 Created

    . . .


Следующий пример показывает как Hello toocreate задание, которое ссылается на идентификатор JobTemplate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


В случае успешного выполнения возвращается следующий ответ hello:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы знаете, как toocreate tooencode задания Создать файл, см. статью [как toocheck задания выполняется с помощью служб мультимедиа](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>См. также
[Получение обработчиков мультимедиа](media-services-rest-get-media-processor.md)
