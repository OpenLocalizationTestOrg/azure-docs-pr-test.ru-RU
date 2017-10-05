---
title: "Масштабирование обработки мультимедийных данных путем добавления единиц кодирования в Azure | Документация Майкрософт"
description: "Информация о добавлении единиц кодирования с помощью .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="6208c-103">Масштабирование кодирования с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="6208c-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6208c-104">Портал</span><span class="sxs-lookup"><span data-stu-id="6208c-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="6208c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6208c-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="6208c-106">REST</span><span class="sxs-lookup"><span data-stu-id="6208c-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="6208c-107">Java</span><span class="sxs-lookup"><span data-stu-id="6208c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="6208c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="6208c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="6208c-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="6208c-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6208c-110">Обязательно ознакомьтесь с этим [обзором](media-services-scale-media-processing-overview.md) , чтобы получить дополнительные сведения о масштабировании обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="6208c-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="6208c-111">Чтобы изменить тип зарезервированных единиц и число зарезервированных единиц кодирования с помощью пакета SDK для .NET, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6208c-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="6208c-112">Открытие запроса в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="6208c-112">Opening a Support Ticket</span></span>
<span data-ttu-id="6208c-113">По умолчанию каждая учетная запись служб мультимедиа может масштабироваться до 25 зарезервированных единиц кодирования и 5 зарезервированных единиц потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="6208c-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="6208c-114">Вы можете запросить более высокий предел, открыв запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="6208c-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="6208c-115">Открытие запроса в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="6208c-115">Open a support ticket</span></span>
<span data-ttu-id="6208c-116">Чтобы открыть запрос в службу поддержки, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="6208c-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="6208c-117">Щелкните [Получить поддержку](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="6208c-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="6208c-118">Если вы не выполнили вход, будет предложено ввести учетные данные.</span><span class="sxs-lookup"><span data-stu-id="6208c-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="6208c-119">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="6208c-119">Select your subscription.</span></span>
3. <span data-ttu-id="6208c-120">В группе типа поддержки выберите "Техническая".</span><span class="sxs-lookup"><span data-stu-id="6208c-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="6208c-121">Щелкните "Создать запрос в службу поддержки".</span><span class="sxs-lookup"><span data-stu-id="6208c-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="6208c-122">Выберите "Службы мультимедиа Azure" в списке продуктов, представленных на следующей странице.</span><span class="sxs-lookup"><span data-stu-id="6208c-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="6208c-123">Выберите соответствующее значение в поле "Тип проблемы".</span><span class="sxs-lookup"><span data-stu-id="6208c-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="6208c-124">Нажмите кнопку "Продолжить".</span><span class="sxs-lookup"><span data-stu-id="6208c-124">Click Continue.</span></span>
8. <span data-ttu-id="6208c-125">Следуйте указаниям на следующей странице, а затем введите сведения о проблеме.</span><span class="sxs-lookup"><span data-stu-id="6208c-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="6208c-126">Нажмите кнопку "Отправить" для создания запроса в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="6208c-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6208c-127">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="6208c-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6208c-128">Отзывы</span><span class="sxs-lookup"><span data-stu-id="6208c-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

