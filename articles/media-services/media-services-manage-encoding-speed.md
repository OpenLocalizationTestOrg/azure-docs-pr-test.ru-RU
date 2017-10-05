---
title: "Управление скоростью и параллелизмом кодирования с помощью служб мультимедиа Azure | Документация Майкрософт"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="5b5e2-103">Управление скоростью и параллелизмом кодирования</span><span class="sxs-lookup"><span data-stu-id="5b5e2-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="5b5e2-104">В этой статье вкратце описывается, как можно управлять скоростью и параллелизмом кодирования заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="5b5e2-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="5b5e2-105">Overview</span></span>

<span data-ttu-id="5b5e2-106">В службах мультимедиа **тип зарезервированных единиц** определяет скорость обработки задач обработки мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="5b5e2-107">Вы можете выбрать один из следующих типов зарезервированных единиц: **S1**, **S2** или **S3**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="5b5e2-108">Например, если использовать тип зарезервированной единицы **S2**, задание по кодированию выполняется быстрее по сравнению заданием, для которого выбран тип **S1**.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="5b5e2-109">В разделе [Масштабирование единиц кодирования](media-services-scale-media-processing-overview.md) представлена таблица, которая поможет вам принять решение при выборе между разными скоростями кодирования.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="5b5e2-110">Вы можете указать не только тип зарезервированных единиц, но и параметр, который позволит вам использовать **зарезервированные единицы** при подготовке учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="5b5e2-111">Количеством подготовленных зарезервированных единиц определяется количество задач мультимедиа, которые могут одновременно обрабатываться в данной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="5b5e2-112">Например, если в учетной записи имеется пять зарезервированных единиц, то будет запущено пять одновременно выполняемых задач мультимедиа, если имеются задачи, которые требуется обработать.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="5b5e2-113">Остальные задачи будут ожидать в очереди, они будут последовательно отбираться для обработки после завершения выполнения текущей задачи.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="5b5e2-114">Если учетная запись не имеет подготовленных зарезервированных единиц, задачи будут отбираться последовательно.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="5b5e2-115">В этом случае время ожидания между завершением одной задачи и началом выполнения следующей будет зависеть от доступности ресурсов в системе.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="5b5e2-116">Дополнительные сведения и примеры масштабирования единиц кодирования см. в [этом](media-services-scale-media-processing-overview.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="5b5e2-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="5b5e2-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b5e2-117">Next step</span></span>

[<span data-ttu-id="5b5e2-118">Масштабирование единиц кодирования</span><span class="sxs-lookup"><span data-stu-id="5b5e2-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="5b5e2-119">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="5b5e2-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5b5e2-120">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5b5e2-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

