---
title: "Рекомендации по обеспечению безопасности помощник по настройке ядра aaaAzure | Документы Microsoft"
description: "Используйте помощник по Azure toohelp повышения безопасности hello развертываний Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="0f06d-103">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="0f06d-103">Advisor Security recommendations</span></span>

<span data-ttu-id="0f06d-104">Помощник по Azure предоставляет согласованное сводное представление с рекомендациями для всех ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f06d-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="0f06d-105">Она интегрируется с toobring центра безопасности Azure вам рекомендации по обеспечению безопасности.</span><span class="sxs-lookup"><span data-stu-id="0f06d-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="0f06d-106">Можно получить рекомендации по обеспечению безопасности hello **безопасности** на hello мониторинга ядра СУБД.</span><span class="sxs-lookup"><span data-stu-id="0f06d-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![Кнопка Hello безопасность ядра СУБД](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="0f06d-108">Центр обеспечения безопасности помогает предотвратить, обнаружения и вернуть toothreats Повышенная видимость и контроль над безопасностью hello Azure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0f06d-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="0f06d-109">Периодически проверяет состояние безопасности hello ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="0f06d-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="0f06d-110">Когда Центр безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации.</span><span class="sxs-lookup"><span data-stu-id="0f06d-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="0f06d-111">рекомендации Hello выполнения процесса hello hello элементов управления, которые необходимо настроить.</span><span class="sxs-lookup"><span data-stu-id="0f06d-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![Вкладка "Безопасность ядра СУБД" Hello](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="0f06d-113">Дополнительные сведения о рекомендациях по безопасности см. в разделе [Управление рекомендациями по безопасности в Центре безопасности Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="0f06d-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="0f06d-114">Как tooaccess рекомендации по обеспечению безопасности в помощнике по Azure</span><span class="sxs-lookup"><span data-stu-id="0f06d-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="0f06d-115">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f06d-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0f06d-116">Hello левой панели щелкните **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="0f06d-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="0f06d-117">В hello службы панели меню в разделе **управление и мониторинг**, нажмите кнопку **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="0f06d-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="0f06d-118">отображается панель мониторинга Advisor Hello.</span><span class="sxs-lookup"><span data-stu-id="0f06d-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="0f06d-119">На панели мониторинга Advisor hello, нажмите кнопку hello **безопасности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0f06d-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="0f06d-120">Выберите подписку hello, для которого требуется tooreceive рекомендации и нажмите кнопку **получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="0f06d-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="0f06d-121">tooaccess рекомендаций Advisor, необходимо сначала *зарегистрировать подписку* помощника по.</span><span class="sxs-lookup"><span data-stu-id="0f06d-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="0f06d-122">Подписка зарегистрирована при *владелец подписки* запускает hello hello панели мониторинга и щелкает пункт помощник по настройке ядра **получить рекомендации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0f06d-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="0f06d-123">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="0f06d-123">This is a *one-time operation*.</span></span> <span data-ttu-id="0f06d-124">После регистрации подписки hello, можно использовать получать рекомендации помощника по как *владельца*, *участника*, или *чтения* для подписки, группу ресурсов или конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="0f06d-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f06d-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f06d-125">Next steps</span></span>

<span data-ttu-id="0f06d-126">в разделе toolearn Дополнительные сведения о рекомендаций помощник по настройке ядра:</span><span class="sxs-lookup"><span data-stu-id="0f06d-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="0f06d-127">Введение tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="0f06d-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="0f06d-128">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="0f06d-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="0f06d-129">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="0f06d-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="0f06d-130">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="0f06d-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="0f06d-131">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="0f06d-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
