---
title: "Служба приложений Azure: масштабирование приложений службы приложений"
description: "Узнайте обо всех тонкостях масштабирования приложений в службе приложений."
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
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="acbb6-104">Служба приложений Azure: масштабирование приложений службы приложений</span><span class="sxs-lookup"><span data-stu-id="acbb6-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="acbb6-105">Приложения, размещенные в службе приложений Azure, можно [значительно масштабировать](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="acbb6-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="acbb6-106">Однако масштабирование приложения является сложной задачей, у которой нет одного универсального решения.</span><span class="sxs-lookup"><span data-stu-id="acbb6-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="acbb6-107">Чтобы правильно масштабировать приложение, обратите внимание на 3 основных фактора:</span><span class="sxs-lookup"><span data-stu-id="acbb6-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="acbb6-108">Понимание архитектуры и слабых сторон приложения.</span><span class="sxs-lookup"><span data-stu-id="acbb6-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="acbb6-109">Отслеживается в вашем приложении состояние</span><span class="sxs-lookup"><span data-stu-id="acbb6-109">Is your Application Stateful?</span></span> <span data-ttu-id="acbb6-110">или нет?</span><span class="sxs-lookup"><span data-stu-id="acbb6-110">Stateless?</span></span>
   * <span data-ttu-id="acbb6-111">Каковы основные компоненты вашего приложения?</span><span class="sxs-lookup"><span data-stu-id="acbb6-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="acbb6-112">Какие "узкие места" есть в вашем приложении?</span><span class="sxs-lookup"><span data-stu-id="acbb6-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="acbb6-113">Что страдает в первую очередь, если приложение подвергается высокой нагрузке?</span><span class="sxs-lookup"><span data-stu-id="acbb6-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="acbb6-114">Понимание ожидаемой нагрузки и требований к производительности.</span><span class="sxs-lookup"><span data-stu-id="acbb6-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="acbb6-115">Сколько пользователей будет обслуживать приложение — тысячу или миллион?</span><span class="sxs-lookup"><span data-stu-id="acbb6-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="acbb6-116">Будет ли трафик создаваться в определенном географическом регионе или повсеместно?</span><span class="sxs-lookup"><span data-stu-id="acbb6-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="acbb6-117">Будут ли иметь место сезонные колебания? Пики нагрузки?</span><span class="sxs-lookup"><span data-stu-id="acbb6-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="acbb6-118">Как быстро должно реагировать приложение —</span><span class="sxs-lookup"><span data-stu-id="acbb6-118">How fast should the app respond?</span></span> <span data-ttu-id="acbb6-119">в течение секунды</span><span class="sxs-lookup"><span data-stu-id="acbb6-119">1 second?</span></span> <span data-ttu-id="acbb6-120">или миллисекунды?</span><span class="sxs-lookup"><span data-stu-id="acbb6-120">1 millisecond?</span></span>
3. <span data-ttu-id="acbb6-121">Понимание и правильное использование платформы, на которой размещается ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="acbb6-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="acbb6-122">Какие функции следует использовать для достижения поставленных целей масштабирования?</span><span class="sxs-lookup"><span data-stu-id="acbb6-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="acbb6-123">Этот раздел поможет вам разобраться во всех этих факторах и создать стратегию, реализующую все необходимые функции службы приложений для достижения искомого уровня масштабирования.</span><span class="sxs-lookup"><span data-stu-id="acbb6-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

