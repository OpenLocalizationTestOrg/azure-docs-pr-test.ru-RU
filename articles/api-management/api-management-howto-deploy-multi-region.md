---
title: "aaaDeploy управления API Azure служб toomultiple Azure областей | Документы Microsoft"
description: "Узнайте, как toodeploy управления API Azure службы toomultiple экземпляра Azure областей."
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="232c2-103">Как toodeploy управления API Azure службы toomultiple экземпляра Azure областей</span><span class="sxs-lookup"><span data-stu-id="232c2-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="232c2-104">API-Интерфейс управления поддерживает развертывание в нескольких регионах позволяющий toodistribute издателей API одну службу управления API между любым числом требуемой регионов Azure.</span><span class="sxs-lookup"><span data-stu-id="232c2-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="232c2-105">Это сокращает задержки, связанные с географической удаленностью потребителей API, а также повышает доступность службы, когда какой-либо из регионов переходит в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="232c2-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="232c2-106">Если изначально создается служба управления API, он содержит только один [единицы] [ unit] и находится в одном регионе Azure, обозначенного как hello основной регион.</span><span class="sxs-lookup"><span data-stu-id="232c2-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="232c2-107">Других регионах могут быть легко добавлена через hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="232c2-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="232c2-108">Сервер шлюза управления API является tooeach развернутой области и вызова трафик будет поступать перенаправленное toohello ближайший шлюза.</span><span class="sxs-lookup"><span data-stu-id="232c2-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="232c2-109">Если область переходит в автономный режим, трафик hello — toohello автоматически перенаправляется далее ближайший шлюза.</span><span class="sxs-lookup"><span data-stu-id="232c2-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="232c2-110">Развертывание в нескольких регионах доступен только в hello  **[Premium] [ Premium]**  уровня.</span><span class="sxs-lookup"><span data-stu-id="232c2-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="232c2-111"><a name="add-region"></a>API управления службы экземпляра tooa новую область развертывания</span><span class="sxs-lookup"><span data-stu-id="232c2-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="232c2-112">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="232c2-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="232c2-113">В портале Azure hello перейдите toohello **масштабирования и ценах** страницы для вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="232c2-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Вкладка "Масштаб"][api-management-scale-service]

<span data-ttu-id="232c2-115">Новая область tooa toodeploy, если щелкнуть **+ добавить область** из инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="232c2-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Добавление региона][api-management-add-region]

<span data-ttu-id="232c2-117">Выберите расположение hello hello раскрывающегося списка и задайте hello число единиц для с hello ползунка.</span><span class="sxs-lookup"><span data-stu-id="232c2-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Указание единиц][api-management-select-location-units]

<span data-ttu-id="232c2-119">Нажмите кнопку **добавить** tooplace выбора, сделанного в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="232c2-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="232c2-120">Повторите эту процедуру, чтобы отобразить все расположения, настроенные и нажмите кнопку **Сохранить** из процесса развертывания hello toostart инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="232c2-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="232c2-121"><a name="remove-region"> </a>Удаление экземпляра службы управления API из расположения</span><span class="sxs-lookup"><span data-stu-id="232c2-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="232c2-122">В портале Azure hello перейдите toohello **масштабирования и ценах** страницы для вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="232c2-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Вкладка "Масштаб"][api-management-scale-service]

<span data-ttu-id="232c2-124">Для расположения hello хотелось бы tooremove откройте контекстное меню hello, с помощью hello **...**  кнопку в правом конце hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="232c2-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="232c2-125">Выберите hello **удалить** параметр.</span><span class="sxs-lookup"><span data-stu-id="232c2-125">Select hello **Delete** option.</span></span>

![Удаление региона][api-management-remove-region]

<span data-ttu-id="232c2-127">Запрашивать подтверждение при удалении hello и нажмите кнопку **Сохранить** tooapply hello изменения.</span><span class="sxs-lookup"><span data-stu-id="232c2-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

