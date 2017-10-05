---
title: "Масштабирование обработки мультимедиа с помощью портала Azure | Документация Майкрософт"
description: "В этом руководстве описывается, как масштабировать обработку данных мультимедиа с помощью портала Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="28a65-103">Изменение типа зарезервированных единиц</span><span class="sxs-lookup"><span data-stu-id="28a65-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28a65-104">.NET</span><span class="sxs-lookup"><span data-stu-id="28a65-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="28a65-105">Портал</span><span class="sxs-lookup"><span data-stu-id="28a65-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="28a65-106">REST</span><span class="sxs-lookup"><span data-stu-id="28a65-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="28a65-107">Java</span><span class="sxs-lookup"><span data-stu-id="28a65-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="28a65-108">PHP</span><span class="sxs-lookup"><span data-stu-id="28a65-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="28a65-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="28a65-109">Overview</span></span>

<span data-ttu-id="28a65-110">Учетная запись служб мультимедиа связана с типом зарезервированных единиц, который определяет скорость обработки задач обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="28a65-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="28a65-111">Вы можете выбрать один из следующих типов зарезервированных единиц: **S1**, **S2** или **S3**.</span><span class="sxs-lookup"><span data-stu-id="28a65-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="28a65-112">Например, если использовать тип зарезервированной единицы **S2**, задание по кодированию выполняется быстрее по сравнению заданием, для которого выбран тип **S1**.</span><span class="sxs-lookup"><span data-stu-id="28a65-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="28a65-113">Помимо указания типа зарезервированных единиц, можно также указать параметр, позволяющий использовать **зарезервированные единицы** при подготовке учетной записи.</span><span class="sxs-lookup"><span data-stu-id="28a65-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="28a65-114">Количеством подготовленных зарезервированных единиц определяется количество задач мультимедиа, которые могут одновременно обрабатываться в данной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="28a65-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="28a65-115">Зарезервированные единицы позволяют распараллелить всю обработку мультимедиа, включая задания индексирования с использованием индексатора мультимедийных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="28a65-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="28a65-116">Однако в отличие от кодировки, задания индексирования не будут обрабатываться быстрее при использовании более производительных зарезервированных единиц.</span><span class="sxs-lookup"><span data-stu-id="28a65-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28a65-117">Обязательно ознакомьтесь с этим [обзором](media-services-scale-media-processing-overview.md) , чтобы получить дополнительные сведения о масштабировании обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="28a65-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="28a65-118">Масштабирование обработки мультимедиа</span><span class="sxs-lookup"><span data-stu-id="28a65-118">Scale media processing</span></span>
<span data-ttu-id="28a65-119">Чтобы изменить тип зарезервированных единиц и число зарезервированных единиц, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="28a65-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="28a65-120">Выберите учетную запись служб мультимедиа Azure на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="28a65-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="28a65-121">В окне **Параметры** выберите **Зарезервированные единицы мультимедиа**.</span><span class="sxs-lookup"><span data-stu-id="28a65-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="28a65-122">Чтобы изменить число зарезервированных единиц для выбранного типа зарезервированных единиц, используйте ползунок **Media Served Units** (Зарезервированные единицы мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="28a65-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="28a65-123">Чтобы изменить **ТИП ЗАРЕЗЕРВИРОВАННЫХ ЕДИНИЦ**, выберите S1, S2 или S3.</span><span class="sxs-lookup"><span data-stu-id="28a65-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Страница "Процессоры"](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="28a65-125">Нажмите кнопку СОХРАНИТЬ, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="28a65-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="28a65-126">Новые зарезервированные единицы выделяются сразу после нажатия кнопки "СОХРАНИТЬ".</span><span class="sxs-lookup"><span data-stu-id="28a65-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28a65-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28a65-127">Next steps</span></span>
<span data-ttu-id="28a65-128">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="28a65-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="28a65-129">Отзывы</span><span class="sxs-lookup"><span data-stu-id="28a65-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

