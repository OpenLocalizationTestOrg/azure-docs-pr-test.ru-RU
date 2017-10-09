---
title: "Как tooget экземпляр обработчика мультимедиа с помощью REST AAA | Документы Microsoft"
description: "Узнайте, как toocreate tooencode компонента обработчика мультимедиа, преобразования формата, шифрования или расшифровки содержимого мультимедиа для служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="cd6f9-103">Как tooget экземпляр обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cd6f9-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd6f9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cd6f9-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="cd6f9-105">REST</span><span class="sxs-lookup"><span data-stu-id="cd6f9-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="cd6f9-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="cd6f9-106">Overview</span></span>
<span data-ttu-id="cd6f9-107">В службах мультимедиа обработчик мультимедиа является компонентом, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного контента.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="cd6f9-108">Обычно вы Создание обработчика мультимедиа при создании tooencode задачи, зашифровать или преобразовать формат hello мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="cd6f9-109">Обработчики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="cd6f9-109">Azure media processors</span></span> 

<span data-ttu-id="cd6f9-110">Hello разделе представлен список обработчиков мультимедиа:</span><span class="sxs-lookup"><span data-stu-id="cd6f9-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="cd6f9-111">Кодировщики мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cd6f9-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="cd6f9-112">Обработчики мультимедиа аналитики</span><span class="sxs-lookup"><span data-stu-id="cd6f9-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="cd6f9-113">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="cd6f9-114">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cd6f9-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="cd6f9-115">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="cd6f9-115">Connect tooMedia Services</span></span>

<span data-ttu-id="cd6f9-116">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="cd6f9-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="cd6f9-117">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="cd6f9-118">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="cd6f9-119">Получение обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cd6f9-119">Get a media processor</span></span>

<span data-ttu-id="cd6f9-120">После вызова REST Hello показано, как экземпляр tooget обработчик мультимедиа по имени (в этом случае **Media Encoder Стандартная**).</span><span class="sxs-lookup"><span data-stu-id="cd6f9-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="cd6f9-121">Запрос:</span><span class="sxs-lookup"><span data-stu-id="cd6f9-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="cd6f9-122">Ответ:</span><span class="sxs-lookup"><span data-stu-id="cd6f9-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="cd6f9-123">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cd6f9-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cd6f9-124">Отзывы</span><span class="sxs-lookup"><span data-stu-id="cd6f9-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cd6f9-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd6f9-125">Next Steps</span></span>
<span data-ttu-id="cd6f9-126">Теперь, когда вы знаете, как перейти tooget экземпляр обработчика мультимедиа toohello [как tooEncode актива](media-services-rest-get-started.md) раздела, в котором мы покажем, как toouse hello Media Encoder Стандартная tooencode актива.</span><span class="sxs-lookup"><span data-stu-id="cd6f9-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

