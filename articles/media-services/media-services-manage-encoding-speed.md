---
title: "скорость управление AAA и параллелизм кодирования с помощью служб мультимедиа Azure | Документы Microsoft"
description: "В этой статье вкратце описывается, как можно управлять скоростью и параллелизмом кодирования заданий и задач с помощью служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="c1fca-103">Управление скоростью и параллелизмом кодирования</span><span class="sxs-lookup"><span data-stu-id="c1fca-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="c1fca-104">В этой статье вкратце описывается, как можно управлять скоростью и параллелизмом кодирования заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="c1fca-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="c1fca-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="c1fca-105">Overview</span></span>

<span data-ttu-id="c1fca-106">В службах мультимедиа **тип зарезервированных единиц** определяет hello скорость обработки задач обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c1fca-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="c1fca-107">Можно выбрать между hello следующие зарезервированные типы единиц измерения: **S1**, **S2**, или **S3**.</span><span class="sxs-lookup"><span data-stu-id="c1fca-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="c1fca-108">Например, hello же кодированию выполняется быстрее при использовании hello **S2** тип зарезервированных единиц сравнить toohello **S1** типа.</span><span class="sxs-lookup"><span data-stu-id="c1fca-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="c1fca-109">Hello [масштабирование единиц кодирования](media-services-scale-media-processing-overview.md) разделе показана таблица, которая поможет принять решение, при выборе между различные скорости кодирования.</span><span class="sxs-lookup"><span data-stu-id="c1fca-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="c1fca-110">Кроме toospecifying hello зарезервировано тип единицы измерения, можно указать tooprovision свою учетную запись с **зарезервированных единиц**.</span><span class="sxs-lookup"><span data-stu-id="c1fca-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="c1fca-111">Hello количество провизионированных зарезервированных единиц определяет hello количество мультимедийных задач, которые можно одновременно обрабатывать в данной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c1fca-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="c1fca-112">Например если ваша учетная запись имеет пять зарезервированных единиц, то пять мультимедийных задач будет выполняться параллельно при условии, как существуют toobe задачи обработки.</span><span class="sxs-lookup"><span data-stu-id="c1fca-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="c1fca-113">Hello оставшиеся задачи будут ожидать в очереди hello и будут извлекаться последовательно обработки после завершения выполняющихся задач.</span><span class="sxs-lookup"><span data-stu-id="c1fca-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="c1fca-114">Если учетная запись не имеет подготовленных зарезервированных единиц, задачи будут отбираться последовательно.</span><span class="sxs-lookup"><span data-stu-id="c1fca-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="c1fca-115">В этом случае hello время ожидания между один завершение задачи и hello началом будет зависеть от hello доступность ресурсов в системе hello.</span><span class="sxs-lookup"><span data-stu-id="c1fca-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="c1fca-116">Подробные сведения и примеры где показано, как tooscale единицы кодирования, в разделе [это](media-services-scale-media-processing-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="c1fca-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="c1fca-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1fca-117">Next step</span></span>

[<span data-ttu-id="c1fca-118">Масштабирование единиц кодирования</span><span class="sxs-lookup"><span data-stu-id="c1fca-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="c1fca-119">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="c1fca-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c1fca-120">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c1fca-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

