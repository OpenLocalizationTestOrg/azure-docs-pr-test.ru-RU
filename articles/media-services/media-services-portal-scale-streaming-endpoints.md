---
title: "конечные точки с портала Azure hello потоковой передачи aaaScale | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги hello масштабирования конечных точек потоковой передачи с hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="a416c-103">Масштабирование конечных точек потоковой передачи с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a416c-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="a416c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a416c-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="a416c-105">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a416c-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a416c-106">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a416c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="a416c-107">Конечные точки уровня **Премиум** подходят для выполнения более сложных задач благодаря выделенной пропускной способности и возможности масштабирования.</span><span class="sxs-lookup"><span data-stu-id="a416c-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="a416c-108">Клиенты, имеющие конечную точку потоковой передачи уровня **Премиум**, по умолчанию получают одну единицу потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a416c-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="a416c-109">Hello конечной точки потоковой передачи можно масштабировать, добавляя SUs.</span><span class="sxs-lookup"><span data-stu-id="a416c-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="a416c-110">Каждый SU приводится дополнительная пропускная способность емкость toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="a416c-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="a416c-111">Дополнительные сведения о потоковой передаче типы конечных точек и настройке CDN см. в разделе hello [Общие сведения о конечной точке потоковой передачи](media-services-portal-manage-streaming-endpoints.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="a416c-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="a416c-112">В этом разделе показано, как tooscale конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a416c-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="a416c-113">Дополнительные сведения о ценах на службы мультимедиа см. [здесь](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="a416c-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="a416c-114">Масштабирование конечных точек потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="a416c-114">Scale streaming endpoints</span></span>

<span data-ttu-id="a416c-115">число единиц потоковой передачи hello toochange hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a416c-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="a416c-116">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="a416c-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a416c-117">В hello **параметры** выберите **конечные точки потоковой передачи**.</span><span class="sxs-lookup"><span data-stu-id="a416c-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="a416c-118">Щелкните конечную точку потоковой передачи hello, которые должны tooscale.</span><span class="sxs-lookup"><span data-stu-id="a416c-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="a416c-119">Масштабировать можно только конечные точки потоковой передачи уровня **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="a416c-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="a416c-120">Переместите hello ползунок toospecify hello число единиц потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="a416c-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="a416c-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a416c-122">Next steps</span></span>
<span data-ttu-id="a416c-123">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="a416c-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a416c-124">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a416c-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

