---
title: "Переопределение режима HTTP с помощью обработчика правил Azure CDN | Документация Майкрософт"
description: "Обработчик правил помогает настраивать способ обработки HTTP-запросов в Azure CDN, включая блокировку доставки определенных типов содержимого, определение политики кэширования и изменение заголовков HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="da493-103">Переопределение режима HTTP с помощью обработчика правил Azure CDN</span><span class="sxs-lookup"><span data-stu-id="da493-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="da493-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="da493-104">Overview</span></span>
<span data-ttu-id="da493-105">Обработчик правил позволяет настроить способ обработки HTTP-запросов, например блокировку доставки определенных типов содержимого, определение политики кэширования и изменение заголовков HTTP.</span><span class="sxs-lookup"><span data-stu-id="da493-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="da493-106">В этом руководстве описано, как создать правило, которое изменит схему кэширования ресурсов CDN.</span><span class="sxs-lookup"><span data-stu-id="da493-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="da493-107">В разделе[См. также](#see-also)находятся соответствующие видеоматериалы.</span><span class="sxs-lookup"><span data-stu-id="da493-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="da493-108">Подробные сведения о синтаксисе см. в [справочнике по обработчику правил](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="da493-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="da493-109">Учебник</span><span class="sxs-lookup"><span data-stu-id="da493-109">Tutorial</span></span>
1. <span data-ttu-id="da493-110">В колонке профиля сети CDN нажмите кнопку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="da493-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="da493-112">Откроется портал управления CDN.</span><span class="sxs-lookup"><span data-stu-id="da493-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="da493-113">Щелкните вкладку **HTTP Large** (Большая HTTP-платформа), а затем вкладку **Подсистема правил**.</span><span class="sxs-lookup"><span data-stu-id="da493-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="da493-114">Появятся параметры для нового правила.</span><span class="sxs-lookup"><span data-stu-id="da493-114">Options for a new rule are displayed.</span></span>
   
    ![Параметры нового правила CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="da493-116">Порядок перечисления правил влияет на способ их обработки.</span><span class="sxs-lookup"><span data-stu-id="da493-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="da493-117">Последующее правило может переопределить действия, заданные предыдущим правилом.</span><span class="sxs-lookup"><span data-stu-id="da493-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="da493-118">В поле **Имя и описание** введите имя.</span><span class="sxs-lookup"><span data-stu-id="da493-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="da493-119">Укажите тип запросов, к которым будет применяться правило.</span><span class="sxs-lookup"><span data-stu-id="da493-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="da493-120">По умолчанию выбрано условие соответствия **Всегда** .</span><span class="sxs-lookup"><span data-stu-id="da493-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="da493-121">В этом учебнике будет использоваться условие **Всегда** , поэтому не изменяйте его.</span><span class="sxs-lookup"><span data-stu-id="da493-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Условие соответствия CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="da493-123">В раскрывающемся списке доступно много типов условий соответствия.</span><span class="sxs-lookup"><span data-stu-id="da493-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="da493-124">Щелкнув синий информационный значок слева от условия соответствия, вы сможете получить подробные сведения о выбранном условии.</span><span class="sxs-lookup"><span data-stu-id="da493-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="da493-125">Полный список условных выражений обработчика правил см. в [этой статье](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="da493-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="da493-126">Полный список условий соответствия обработчика правил см. в [этой статье](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="da493-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="da493-127">Нажмите кнопку **+** рядом с пунктом **Функции**, чтобы добавить новую функцию.</span><span class="sxs-lookup"><span data-stu-id="da493-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="da493-128">В раскрывающемся списке в левой части выберите **Принудительно извлечь внутренний максимальный возраст**.</span><span class="sxs-lookup"><span data-stu-id="da493-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="da493-129">В появившемся текстовом поле введите **300**.</span><span class="sxs-lookup"><span data-stu-id="da493-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="da493-130">Оставьте остальные значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="da493-130">Leave the remaining default values.</span></span>
   
   ![Функция CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="da493-132">Как и в случае с условиями соответствия, при щелчке синего информационного значка слева от новой функции будут отображены подробные сведения об этой функции.</span><span class="sxs-lookup"><span data-stu-id="da493-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="da493-133">При использовании параметра **Force Internal Max-Age** (Принудительно извлечь внутренний максимальный возраст) мы переопределяем заголовки ресурса **Cache-Control** и **Expires** для управления моментом обновления граничным узлом CDN ресурса из источника.</span><span class="sxs-lookup"><span data-stu-id="da493-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="da493-134">В нашем примере 300 секунд означает, что граничный узел CDN будет кэшировать ресурс в течение 5 минут перед его обновлением из источника.</span><span class="sxs-lookup"><span data-stu-id="da493-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="da493-135">Полный список функций обработчика правил см. в [этой статье](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="da493-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="da493-136">Нажмите кнопку **Добавить** , чтобы сохранить новое правило.</span><span class="sxs-lookup"><span data-stu-id="da493-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="da493-137">Теперь новое правило ожидает утверждения.</span><span class="sxs-lookup"><span data-stu-id="da493-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="da493-138">После утверждения состояние правила изменится с **Pending XML** (XML в ожидании) на **Active XML** (Активный XML).</span><span class="sxs-lookup"><span data-stu-id="da493-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="da493-139">Распространение изменений правил по сети CDN может занять до 90 минут.</span><span class="sxs-lookup"><span data-stu-id="da493-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="da493-140">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="da493-140">See also</span></span>
* [<span data-ttu-id="da493-141">Обзор Azure CDN</span><span class="sxs-lookup"><span data-stu-id="da493-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="da493-142">Справочник по обработчику правил</span><span class="sxs-lookup"><span data-stu-id="da493-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="da493-143">Условия соответствия обработчика правил</span><span class="sxs-lookup"><span data-stu-id="da493-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="da493-144">Условные выражения обработчика правил</span><span class="sxs-lookup"><span data-stu-id="da493-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="da493-145">Функции обработчика правил</span><span class="sxs-lookup"><span data-stu-id="da493-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="da493-146">Переопределение стандартного поведения через HTTP с помощью обработчика правил</span><span class="sxs-lookup"><span data-stu-id="da493-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="da493-147">[Пятничный видеоролик об Azure. Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Новые возможности Azure CDN уровня "Премиум")</span><span class="sxs-lookup"><span data-stu-id="da493-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>