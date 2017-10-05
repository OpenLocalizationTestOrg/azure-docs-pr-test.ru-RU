---
title: "Развертывание служб управления API Azure в нескольких регионах Azure | Документация Майкрософт"
description: "Дополнительные сведения о развертывании экземпляра службы управления Azure API в различных регионах Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="f7f9c-103">Развертывание экземпляра службы управления Azure API в различных регионах Azure</span><span class="sxs-lookup"><span data-stu-id="f7f9c-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="f7f9c-104">Служба управления API поддерживает развертывание в нескольких регионах, что позволяет издателям API распространять единую службу управления API в любых требуемых регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="f7f9c-105">Это сокращает задержки, связанные с географической удаленностью потребителей API, а также повышает доступность службы, когда какой-либо из регионов переходит в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="f7f9c-106">При создании службы управления API она содержит только одну [единицу][unit] и располагается в одном регионе Azure, который считается основным.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="f7f9c-107">Однако через портал Azure можно легко добавить дополнительные регионы.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="f7f9c-108">В каждом регионе развертывается сервер шлюза управления API, и весь трафик вызовов направляется на ближайший из таких шлюзов.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="f7f9c-109">Если регион переходит в автономный режим, трафик автоматически перенаправляется к другому ближайшему шлюзу.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f7f9c-110">Развертывание в нескольких регионах доступно только для уровня **[Премиум][Premium]**.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="f7f9c-111"><a name="add-region"> </a>Создание экземпляра службы управления API в новом регионе</span><span class="sxs-lookup"><span data-stu-id="f7f9c-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="f7f9c-112">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f7f9c-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="f7f9c-113">На портале Azure перейдите на страницу **Scale and pricing** (Масштаб и цены) для своего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Вкладка "Масштаб"][api-management-scale-service]

<span data-ttu-id="f7f9c-115">Чтобы развернуть службу в новом регионе, щелкните **+ Add region** (+ Добавить регион) на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Добавление региона][api-management-add-region]

<span data-ttu-id="f7f9c-117">Выберите расположение из раскрывающегося списка и задайте число единиц с помощью ползунка.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Указание единиц][api-management-select-location-units]

<span data-ttu-id="f7f9c-119">Щелкните **Добавить**, чтобы разместить выбранные ресурсы в таблице "Расположения".</span><span class="sxs-lookup"><span data-stu-id="f7f9c-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="f7f9c-120">Повторите этот процесс, пока не будут настроены все расположения, затем щелкните **Сохранить** на панели инструментов, чтобы начать процесс развертывания.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="f7f9c-121"><a name="remove-region"> </a>Удаление экземпляра службы управления API из расположения</span><span class="sxs-lookup"><span data-stu-id="f7f9c-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="f7f9c-122">На портале Azure перейдите на страницу **Scale and pricing** (Масштаб и цены) для своего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Вкладка "Масштаб"][api-management-scale-service]

<span data-ttu-id="f7f9c-124">Для расположения, которое нужно удалить, откройте контекстное меню с помощью кнопки **…** в правой части таблицы.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="f7f9c-125">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-125">Select the **Delete** option.</span></span>

![Удаление региона][api-management-remove-region]

<span data-ttu-id="f7f9c-127">Подтвердите удаление и нажмите кнопку **Сохранить**, чтобы применить изменения.</span><span class="sxs-lookup"><span data-stu-id="f7f9c-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

