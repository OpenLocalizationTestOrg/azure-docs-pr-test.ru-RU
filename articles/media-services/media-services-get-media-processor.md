---
title: "Обработчик мультимедиа с помощью tooCreate aaaHow hello Azure Media Services SDK для .NET | Документы Microsoft"
description: "Узнайте, как toocreate tooencode компонента обработчика мультимедиа, преобразования формата, шифрования или расшифровки содержимого мультимедиа для служб мультимедиа Azure. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="4abaa-104">Получение экземпляра процессора мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4abaa-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4abaa-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4abaa-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="4abaa-106">REST</span><span class="sxs-lookup"><span data-stu-id="4abaa-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4abaa-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="4abaa-107">Overview</span></span>
<span data-ttu-id="4abaa-108">В службах мультимедиа обработчик мультимедиа является компонентом, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного контента.</span><span class="sxs-lookup"><span data-stu-id="4abaa-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="4abaa-109">Обычно вы Создание обработчика мультимедиа при создании tooencode задачи, зашифровать или преобразовать формат hello мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="4abaa-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="4abaa-110">Обработчики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="4abaa-110">Azure media processors</span></span> 

<span data-ttu-id="4abaa-111">Hello разделе представлен список обработчиков мультимедиа:</span><span class="sxs-lookup"><span data-stu-id="4abaa-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="4abaa-112">Кодировщики мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4abaa-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="4abaa-113">Обработчики мультимедиа аналитики</span><span class="sxs-lookup"><span data-stu-id="4abaa-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="4abaa-114">Получение обработчика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4abaa-114">Get Media Processor</span></span>

<span data-ttu-id="4abaa-115">Здравствуйте, как следующая показан метод tooget экземпляр обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="4abaa-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="4abaa-116">Hello примере кода предполагается, что используется hello переменную уровня модуля с именем **_контекста** tooreference hello server контекста, как описано в разделе "hello" [как: подключение службы программным образом tooMedia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="4abaa-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="4abaa-117">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="4abaa-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4abaa-118">Отзывы</span><span class="sxs-lookup"><span data-stu-id="4abaa-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4abaa-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4abaa-119">Next Steps</span></span>
<span data-ttu-id="4abaa-120">Теперь, когда вы знаете, как перейти tooget экземпляр обработчика мультимедиа toohello [как tooEncode актива](media-services-dotnet-encode-with-media-encoder-standard.md) раздела, в котором мы покажем, как toouse hello Media Encoder Стандартная tooencode актива.</span><span class="sxs-lookup"><span data-stu-id="4abaa-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

