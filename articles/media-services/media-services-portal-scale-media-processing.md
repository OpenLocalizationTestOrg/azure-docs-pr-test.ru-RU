---
title: "Обработка с использованием носителя aaaScale hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить действия hello масштабирования носителя, обработка с использованием портала Azure hello."
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="55e9f-103">Изменение hello защищены тип единицы измерения</span><span class="sxs-lookup"><span data-stu-id="55e9f-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55e9f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="55e9f-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="55e9f-105">Портал</span><span class="sxs-lookup"><span data-stu-id="55e9f-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="55e9f-106">REST</span><span class="sxs-lookup"><span data-stu-id="55e9f-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="55e9f-107">Java</span><span class="sxs-lookup"><span data-stu-id="55e9f-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="55e9f-108">PHP</span><span class="sxs-lookup"><span data-stu-id="55e9f-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="55e9f-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="55e9f-109">Overview</span></span>

<span data-ttu-id="55e9f-110">Учетная запись служб мультимедиа связан с зарезервированным тип базового определяет hello скорость обработки задач обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55e9f-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="55e9f-111">Можно выбрать между hello следующие зарезервированные типы единиц измерения: **S1**, **S2**, или **S3**.</span><span class="sxs-lookup"><span data-stu-id="55e9f-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="55e9f-112">Например, hello же кодированию выполняется быстрее при использовании hello **S2** тип зарезервированных единиц сравнить toohello **S1** типа.</span><span class="sxs-lookup"><span data-stu-id="55e9f-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="55e9f-113">Кроме toospecifying hello зарезервировано тип единицы измерения, можно указать tooprovision свою учетную запись с **зарезервированных единиц** (RUs).</span><span class="sxs-lookup"><span data-stu-id="55e9f-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="55e9f-114">Hello число подготовленных RUs определяет hello количество мультимедийных задач, которые можно одновременно обрабатывать в данной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="55e9f-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="55e9f-115">Зарезервированные единицы позволяют распараллелить всю обработку мультимедиа, включая задания индексирования с использованием индексатора мультимедийных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="55e9f-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="55e9f-116">Однако в отличие от кодировки, задания индексирования не будут обрабатываться быстрее при использовании более производительных зарезервированных единиц.</span><span class="sxs-lookup"><span data-stu-id="55e9f-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55e9f-117">Убедитесь, что hello tooreview [Обзор](media-services-scale-media-processing-overview.md) tooget разделе Дополнительные сведения о масштабировании раздела с мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55e9f-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="55e9f-118">Масштабирование обработки мультимедиа</span><span class="sxs-lookup"><span data-stu-id="55e9f-118">Scale media processing</span></span>
<span data-ttu-id="55e9f-119">toochange hello зарезервированные единицы типа и hello число зарезервированных единиц hello следующие:</span><span class="sxs-lookup"><span data-stu-id="55e9f-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="55e9f-120">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="55e9f-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="55e9f-121">В hello **параметры** выберите **зарезервированные единицы мультимедиа**.</span><span class="sxs-lookup"><span data-stu-id="55e9f-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="55e9f-122">Число зарезервированных единиц для hello hello toochange выбранный тип зарезервированных единиц, используйте hello **единицы обслуживаться носителя** ползунок.</span><span class="sxs-lookup"><span data-stu-id="55e9f-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="55e9f-123">toochange hello **тип ЗАРЕЗЕРВИРОВАННЫХ ЕДИНИЦ**, нажмите клавишу S1, S2 и S3.</span><span class="sxs-lookup"><span data-stu-id="55e9f-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Страница "Процессоры"](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="55e9f-125">Нажмите клавишу hello СОХРАНИТЕ toosave кнопки изменения.</span><span class="sxs-lookup"><span data-stu-id="55e9f-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="55e9f-126">новые зарезервированные элементы Hello выделяются при нажатии клавиши СОХРАНЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="55e9f-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e9f-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55e9f-127">Next steps</span></span>
<span data-ttu-id="55e9f-128">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55e9f-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55e9f-129">Отзывы</span><span class="sxs-lookup"><span data-stu-id="55e9f-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

