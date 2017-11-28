---
title: "Как получить экземпляр обработчика мультимедиа с помощью REST | Документация Майкрософт"
description: "Узнайте, как создать компонент обработчика мультимедиа для кодирования, преобразования формата, шифрования или расшифровки мультимедийного контента служб мультимедиа Azure."
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
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="a3350-103">Как получить экземпляр обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a3350-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3350-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a3350-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="a3350-105">REST</span><span class="sxs-lookup"><span data-stu-id="a3350-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a3350-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="a3350-106">Overview</span></span>
<span data-ttu-id="a3350-107">В службах мультимедиа обработчик мультимедиа является компонентом, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного контента.</span><span class="sxs-lookup"><span data-stu-id="a3350-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="a3350-108">Обработчик мультимедиа обычно создается при создании задачи для кодирования, шифрования или преобразования формата мультимедийного контента.</span><span class="sxs-lookup"><span data-stu-id="a3350-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="a3350-109">Обработчики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="a3350-109">Azure media processors</span></span> 

<span data-ttu-id="a3350-110">В следующем разделе приводятся списки обработчиков мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a3350-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="a3350-111">Кодировщики мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a3350-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="a3350-112">Обработчики мультимедиа аналитики</span><span class="sxs-lookup"><span data-stu-id="a3350-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="a3350-113">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="a3350-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a3350-114">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a3350-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="a3350-115">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a3350-115">Connect to Media Services</span></span>

<span data-ttu-id="a3350-116">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a3350-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a3350-117">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a3350-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a3350-118">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="a3350-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="a3350-119">Получение обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a3350-119">Get a media processor</span></span>

<span data-ttu-id="a3350-120">Следующий вызов REST показывает, как получить экземпляр обработчика мультимедиа по имени (в данном случае это **стандартный кодировщик мультимедиа**).</span><span class="sxs-lookup"><span data-stu-id="a3350-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="a3350-121">Запрос:</span><span class="sxs-lookup"><span data-stu-id="a3350-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="a3350-122">Ответ:</span><span class="sxs-lookup"><span data-stu-id="a3350-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="a3350-123">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a3350-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a3350-124">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a3350-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a3350-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3350-125">Next Steps</span></span>
<span data-ttu-id="a3350-126">Теперь, когда вы знаете, как получить экземпляр обработчика мультимедиа, перейдите в раздел [Кодировка актива](media-services-rest-get-started.md) , в котором будет показано, как использовать Media Encoder Standard для кодирования ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="a3350-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

