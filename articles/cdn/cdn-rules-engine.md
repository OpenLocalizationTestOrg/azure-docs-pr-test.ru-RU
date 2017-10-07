---
title: "Использование обработчика правил hello Azure CDN поведение aaaOverride HTTP | Документы Microsoft"
description: "Обработчик правил Hello позволяет toocustomize обработке HTTP-запросов Azure CDN, такие как блокировка доставки hello определенных типов содержимого и определить политику кэширования изменения заголовков HTTP."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="9e4af-103">Переопределить поведение HTTP с помощью модуля правил hello Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9e4af-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="9e4af-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9e4af-104">Overview</span></span>
<span data-ttu-id="9e4af-105">Обработчик правил Hello позволяет toocustomize обработку HTTP-запросов, таких как блокировки доставки hello определенных типов содержимого, определяющий политику кэширования и изменение заголовков HTTP.</span><span class="sxs-lookup"><span data-stu-id="9e4af-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="9e4af-106">Этот учебник покажем, что создания правила, которые будут изменяться hello кэширование CDN активов.</span><span class="sxs-lookup"><span data-stu-id="9e4af-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="9e4af-107">Отсутствуют также видео-контента в hello»[см. также](#see-also)» раздела.</span><span class="sxs-lookup"><span data-stu-id="9e4af-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9e4af-108">Синтаксис toohello ссылка подробно см [ссылку на модуль правил](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9e4af-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="9e4af-109">Учебник</span><span class="sxs-lookup"><span data-stu-id="9e4af-109">Tutorial</span></span>
1. <span data-ttu-id="9e4af-110">В колонке профиля CDN hello выберите hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9e4af-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="9e4af-112">Открытие портала управления CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="9e4af-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="9e4af-113">Щелкните hello **HTTP больших** пользовательская вкладка, **обработчик правил**.</span><span class="sxs-lookup"><span data-stu-id="9e4af-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="9e4af-114">Появятся параметры для нового правила.</span><span class="sxs-lookup"><span data-stu-id="9e4af-114">Options for a new rule are displayed.</span></span>
   
    ![Параметры нового правила CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="9e4af-116">Hello порядок, в котором перечислены несколько правил влияет на способ обработки.</span><span class="sxs-lookup"><span data-stu-id="9e4af-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="9e4af-117">Последующие правила могут переопределять hello действия, указанные с помощью предыдущего правила.</span><span class="sxs-lookup"><span data-stu-id="9e4af-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="9e4af-118">Введите имя в hello **имя и описание** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="9e4af-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="9e4af-119">Укажите тип hello hello правила будут применяться к запросов.</span><span class="sxs-lookup"><span data-stu-id="9e4af-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="9e4af-120">По умолчанию hello **всегда** выбрано условие соответствия.</span><span class="sxs-lookup"><span data-stu-id="9e4af-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="9e4af-121">В этом учебнике будет использоваться условие **Всегда** , поэтому не изменяйте его.</span><span class="sxs-lookup"><span data-stu-id="9e4af-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Условие соответствия CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="9e4af-123">Существует много типов совпадения условия, доступные в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="9e4af-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="9e4af-124">Щелкнув синий hello toohello информационный значок слева от условия соответствия hello объясняется, выбранного в данный момент hello условие подробно.</span><span class="sxs-lookup"><span data-stu-id="9e4af-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="9e4af-125">Hello полный список условные выражения подробное описание см. в разделе [условного выражения правила ядра](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="9e4af-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="9e4af-126">Hello полный список условия совпадения подробное описание см. в разделе [условия соответствует обработчик правил](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="9e4af-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9e4af-127">Нажмите кнопку hello  **+**  рядом слишком**функции** tooadd новую функцию.</span><span class="sxs-lookup"><span data-stu-id="9e4af-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="9e4af-128">В раскрывающемся списке hello hello слева, выберите **Force внутренней Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="9e4af-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="9e4af-129">В появившемся текстовом hello введите **300**.</span><span class="sxs-lookup"><span data-stu-id="9e4af-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="9e4af-130">Оставьте hello, оставшиеся значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9e4af-130">Leave hello remaining default values.</span></span>
   
   ![Функция CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="9e4af-132">Как с условиями соответствия, щелкнув синий hello toohello информационный значок слева от hello новые функции будут отображаться сведения об этой функции.</span><span class="sxs-lookup"><span data-stu-id="9e4af-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="9e4af-133">В случае hello **Force внутренней Max-Age**, мы переопределении hello активов **Cache-Control** и **Expires** toocontrol заголовки при hello CDN граничного узла будет обновлен hello ресурс из источника hello.</span><span class="sxs-lookup"><span data-stu-id="9e4af-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="9e4af-134">Наш пример 300 секунд означает, что hello CDN граничного узла будет кэшировать активов hello в течение 5 минут до обновления активов hello от начала координат.</span><span class="sxs-lookup"><span data-stu-id="9e4af-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="9e4af-135">Hello полный список компонентов подробно см. в разделе [подробные сведения о возможностях обработчик правил](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="9e4af-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="9e4af-136">Нажмите кнопку hello **добавить** кнопку toosave hello новое правило.</span><span class="sxs-lookup"><span data-stu-id="9e4af-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="9e4af-137">новое правило Hello теперь ожидает утверждения.</span><span class="sxs-lookup"><span data-stu-id="9e4af-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="9e4af-138">После его утверждения hello состояние изменится с **ожидающие XML** слишком**Active XML**.</span><span class="sxs-lookup"><span data-stu-id="9e4af-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9e4af-139">Правила изменения может занять toopropagate минут too90 через hello CDN.</span><span class="sxs-lookup"><span data-stu-id="9e4af-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="9e4af-140">См. также</span><span class="sxs-lookup"><span data-stu-id="9e4af-140">See also</span></span>
* [<span data-ttu-id="9e4af-141">Обзор Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9e4af-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="9e4af-142">Справочник по обработчику правил</span><span class="sxs-lookup"><span data-stu-id="9e4af-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="9e4af-143">Условия соответствия обработчика правил</span><span class="sxs-lookup"><span data-stu-id="9e4af-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="9e4af-144">Условные выражения обработчика правил</span><span class="sxs-lookup"><span data-stu-id="9e4af-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="9e4af-145">Функции обработчика правил</span><span class="sxs-lookup"><span data-stu-id="9e4af-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="9e4af-146">Переопределение поведения по умолчанию HTTP с помощью модуля правил hello</span><span class="sxs-lookup"><span data-stu-id="9e4af-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="9e4af-147">[Пятничный видеоролик об Azure. Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (Новые возможности Azure CDN уровня "Премиум")</span><span class="sxs-lookup"><span data-stu-id="9e4af-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>