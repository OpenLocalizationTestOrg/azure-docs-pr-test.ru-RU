---
title: "Служба приложений Azure: масштабирование приложений службы приложений"
description: "Узнайте hello тонкости масштабирование приложения в службе приложений."
keywords: "служба приложений, служба приложений azure, масштабировать, масштабируемый, план службы приложений, стоимость службы приложений"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="58b02-104">Служба приложений Azure: масштабирование приложений службы приложений</span><span class="sxs-lookup"><span data-stu-id="58b02-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="58b02-105">Приложения, размещенные в службе приложений Azure, можно [значительно масштабировать](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="58b02-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="58b02-106">Однако масштабирование приложения является сложной задачей, у которой нет одного универсального решения.</span><span class="sxs-lookup"><span data-stu-id="58b02-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="58b02-107">toocorrectly масштабировании приложения существует 3 ключевых областях, которые будут передавать успех tooyour приложений:</span><span class="sxs-lookup"><span data-stu-id="58b02-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="58b02-108">Понимание архитектуры и слабых сторон приложения.</span><span class="sxs-lookup"><span data-stu-id="58b02-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="58b02-109">Отслеживается в вашем приложении состояние</span><span class="sxs-lookup"><span data-stu-id="58b02-109">Is your Application Stateful?</span></span> <span data-ttu-id="58b02-110">или нет?</span><span class="sxs-lookup"><span data-stu-id="58b02-110">Stateless?</span></span>
   * <span data-ttu-id="58b02-111">Что такое все компоненты приложения hello</span><span class="sxs-lookup"><span data-stu-id="58b02-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="58b02-112">Где находятся hello узких мест в приложении hello?</span><span class="sxs-lookup"><span data-stu-id="58b02-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="58b02-113">При нагрузке app примененных tooyour, что нарушит первый?</span><span class="sxs-lookup"><span data-stu-id="58b02-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="58b02-114">Основные сведения о hello ожидается требований к производительности и нагрузки.</span><span class="sxs-lookup"><span data-stu-id="58b02-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="58b02-115">Требуется ли приложение hello tooserve тысяч пользователей? или один миллион?</span><span class="sxs-lookup"><span data-stu-id="58b02-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="58b02-116">Будет ли трафик создаваться в определенном географическом регионе или повсеместно?</span><span class="sxs-lookup"><span data-stu-id="58b02-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="58b02-117">Будут ли иметь место сезонные колебания? Пики нагрузки?</span><span class="sxs-lookup"><span data-stu-id="58b02-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="58b02-118">Как быстро следует реагировать приложение hello</span><span class="sxs-lookup"><span data-stu-id="58b02-118">How fast should hello app respond?</span></span> <span data-ttu-id="58b02-119">в течение секунды</span><span class="sxs-lookup"><span data-stu-id="58b02-119">1 second?</span></span> <span data-ttu-id="58b02-120">или миллисекунды?</span><span class="sxs-lookup"><span data-stu-id="58b02-120">1 millisecond?</span></span>
3. <span data-ttu-id="58b02-121">Основные сведения о и правильно используйте hello платформы размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="58b02-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="58b02-122">Функции следует использовать tooachieve моих целей масштабирования?</span><span class="sxs-lookup"><span data-stu-id="58b02-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="58b02-123">В этом разделе помогут понять все факторы hello и справки, разработать стратегию, которая использует преимущества hello необходимые службы приложений функции tooachieve целей масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="58b02-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

