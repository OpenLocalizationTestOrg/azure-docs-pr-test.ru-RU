---
title: "Выставление счетов и о гибком управлении ресурсами в Azure стек aaaCustomer | Документы Microsoft"
description: "Узнайте, как сведения об использовании ресурсов tooretrieve из стека Azure."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="f1a19-103">Использование и выставление счетов в стек Azure</span><span class="sxs-lookup"><span data-stu-id="f1a19-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="f1a19-104">Использование представляет hello количество ресурсов, потребляемых пользователем.</span><span class="sxs-lookup"><span data-stu-id="f1a19-104">Usage represents hello quantity of resources consumed by a user.</span></span> <span data-ttu-id="f1a19-105">Стек Azure собирает сведения об использовании для каждого пользователя и использует их toobill их.</span><span class="sxs-lookup"><span data-stu-id="f1a19-105">Azure Stack collects usage information for each user and uses it toobill them.</span></span> <span data-ttu-id="f1a19-106">Эта статья описывает, каким образом пользователи стек Azure взимается плата за использование ресурсов, и способ доступа к hello сведений о выставлении счетов для аналитики, гибкого управления ресурсами, и т. д.</span><span class="sxs-lookup"><span data-stu-id="f1a19-106">This article describes how Azure Stack users are billed for resource usage, and how hello billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="f1a19-107">Стек Azure содержит toocollect инфраструктуры hello и собирать данные об использовании для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f1a19-107">Azure Stack contains hello infrastructure toocollect and aggregate usage data for all resources.</span></span> <span data-ttu-id="f1a19-108">Доступ к этим данным и экспортировать tooa система выставления счетов с помощью адаптера выставления счетов или экспортировать его средство tooa бизнес-аналитики, такие как Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="f1a19-108">You can access this data and export it tooa billing system by using a billing adapter, or export it tooa business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="f1a19-109">После экспорта, это сведения об оплате используется для аналитики или передаваться tooa системы о гибком управлении ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f1a19-109">After exporting, this billing information is used for analytics or transferred tooa chargeback system.</span></span>

![Концептуальная модель для подключения Azure стека tooa адаптер выставления счетов выставления счетов для приложения](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="f1a19-111">Какие сведения об использовании можно найти и как?</span><span class="sxs-lookup"><span data-stu-id="f1a19-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="f1a19-112">Azure поставщиков ресурсов стека, например вычислений, хранения и сети, создают данные об использовании через часовые интервалы для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="f1a19-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="f1a19-113">Hello данные об использовании содержит сведения о ресурсе hello, например, имя ресурса, индикатор имя, идентификатор отслеживать количество использованные toolearn т. д. о ресурсах идентификатор hello метрах см. в toohello [API часто задаваемые вопросы об использовании](azure-stack-usage-related-faq.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f1a19-113">hello usage data contains information about hello resource used such as resource name, meter name, meter ID, quantity used etc. toolearn about hello meters ID resources, refer toohello [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="f1a19-114">После сбора данных об использовании hello — [сообщил tooAzure](azure-stack-usage-reporting.md) toogenerate счета, который можно просмотреть с помощью hello Azure портале выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="f1a19-114">After hello usage data has been collected, it is [reported tooAzure](azure-stack-usage-reporting.md) toogenerate a bill, which can be viewed through hello Azure billing portal.</span></span> <span data-ttu-id="f1a19-115">Hello Azure портале выставления счетов выводятся данные об использовании hello только для ресурсов оплачивается hello.</span><span class="sxs-lookup"><span data-stu-id="f1a19-115">hello Azure billing portal shows hello usage data only for hello chargeable resources.</span></span> <span data-ttu-id="f1a19-116">В дополнение к этому toohello оплачивается ресурсы, стек Azure записывает данные об использовании для более широкому набору ресурсов, которые можно использовать в среде Azure стека через API-интерфейс REST или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1a19-116">In addition toohello chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="f1a19-117">Администраторов облака Azure стека можно получить данные об использовании hello для всех пользовательских подписок, в то время как пользователь сможет получить только свои сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="f1a19-117">Azure Stack cloud administrators can retrieve hello usage data for all user subscriptions whereas a user can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="f1a19-118">Получить сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="f1a19-118">Retrieve usage information</span></span>

<span data-ttu-id="f1a19-119">данные об использовании toogenerate hello, должен иметь ресурсы, которые запущена и активно используете hello системы.</span><span class="sxs-lookup"><span data-stu-id="f1a19-119">toogenerate hello usage data, you should have resources that are running and actively using hello system.</span></span> <span data-ttu-id="f1a19-120">Если вы не знаете ли какие либо ресурсы в Azure Marketplace стека, развертывание виртуальной машины (VM) и проверить hello ВМ мониторинга колонке toomake убедиться, что она выполняет.</span><span class="sxs-lookup"><span data-stu-id="f1a19-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify hello VM monitoring blade toomake sure it’s running.</span></span> <span data-ttu-id="f1a19-121">Используйте следующие данные об использовании hello tooview командлеты PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f1a19-121">Use hello following PowerShell cmdlets tooview hello usage data:</span></span>

1. [<span data-ttu-id="f1a19-122">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="f1a19-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. * <span data-ttu-id="f1a19-123">[Настройка пользователя Azure стека hello](azure-stack-powershell-configure-user.md) или hello [стека Azure оператор](azure-stack-powershell-configure-admin.md) среды PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1a19-123">[Configure hello Azure Stack user's](azure-stack-powershell-configure-user.md) or hello [Azure Stack operator's](azure-stack-powershell-configure-admin.md) PowerShell environment</span></span> 
3. <span data-ttu-id="f1a19-124">данные об использовании tooretrieve hello, использовать hello [Get UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) командлета PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1a19-124">tooretrieve hello usage data, use hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="f1a19-125">Если данные об использовании недоступны, возвращается в как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="f1a19-125">If usage data is available, it’s returned in as shown in hello following screenshot:</span></span> 
   
   ![Использование статистических выражений](media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="f1a19-127">PowerShell возвращает 1 000 строк использование каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="f1a19-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="f1a19-128">Можно использовать параметр tooretrieve hello продолжения более 1000 строк</span><span class="sxs-lookup"><span data-stu-id="f1a19-128">You can use hello continuation parameter tooretrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1a19-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1a19-129">Next steps</span></span>

[<span data-ttu-id="f1a19-130">Отчет tooAzure данных об использовании стек Azure</span><span class="sxs-lookup"><span data-stu-id="f1a19-130">Report Azure Stack usage data tooAzure</span></span>](azure-stack-usage-reporting.md)

[<span data-ttu-id="f1a19-131">Использование поставщика ресурсов API</span><span class="sxs-lookup"><span data-stu-id="f1a19-131">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="f1a19-132">Использование ресурсов API клиента</span><span class="sxs-lookup"><span data-stu-id="f1a19-132">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="f1a19-133">Часто задаваемые вопросы, относящиеся к использованию</span><span class="sxs-lookup"><span data-stu-id="f1a19-133">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

