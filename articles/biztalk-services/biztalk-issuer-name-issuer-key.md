---
title: "Имя издателя и ключ издателя в службах BizTalk | Документация Майкрософт"
description: "Узнайте, как извлечь имя и ключ издателя для Service Bus или управления доступом (ACS) в службах BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="bcea6-104">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="bcea6-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="bcea6-105">В службах BizTalk в Azure используются имя и ключ издателя Service Bus, а также имя и ключ издателя службы Access Control.</span><span class="sxs-lookup"><span data-stu-id="bcea6-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="bcea6-106">В частности:</span><span class="sxs-lookup"><span data-stu-id="bcea6-106">Specifically:</span></span>

| <span data-ttu-id="bcea6-107">Задача</span><span class="sxs-lookup"><span data-stu-id="bcea6-107">Task</span></span> | <span data-ttu-id="bcea6-108">Используемые имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="bcea6-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="bcea6-109">Развертывание приложения из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcea6-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="bcea6-110">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="bcea6-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="bcea6-111">Настройка портала служб BizTalk в Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="bcea6-112">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="bcea6-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="bcea6-113">Создание бизнес-ретрансляций со службами адаптера BizTalk в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcea6-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="bcea6-114">Имя и ключ издателя шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="bcea6-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="bcea6-115">В этом разделе перечислены шаги для извлечения имени и ключа издателя.</span><span class="sxs-lookup"><span data-stu-id="bcea6-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="bcea6-116">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="bcea6-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="bcea6-117">Имя и ключ издателя для службы Access Control используются в следующих областях:</span><span class="sxs-lookup"><span data-stu-id="bcea6-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="bcea6-118">Приложение службы BizTalk в Azure, созданное в среде Visual Studio: для успешного развертывания в Azure приложения службы BizTalk, созданного в среде Visual Studio, необходимо ввести имя и ключ издателя для службы Access Control.</span><span class="sxs-lookup"><span data-stu-id="bcea6-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="bcea6-119">Портал служб BizTalk Azure. При открытии портала служб BizTalk во время создания службы BizTalk имя и ключ издателя для службы контроля доступа автоматически регистрируются для развертываний с теми же значениями службы контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="bcea6-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="bcea6-120">Имя и ключ издателя для службы контроля доступа</span><span class="sxs-lookup"><span data-stu-id="bcea6-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="bcea6-121">Чтобы использовать ACS для аутентификации и получить значения имени и ключа издателя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="bcea6-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="bcea6-122">Установите [командлеты Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="bcea6-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="bcea6-123">Добавьте учетную запись Azure: `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="bcea6-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="bcea6-124">Получите имя подписки: `get-azuresubscription`.</span><span class="sxs-lookup"><span data-stu-id="bcea6-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="bcea6-125">Выберите свою подписку: `select-azuresubscription <name of your subscription>`.</span><span class="sxs-lookup"><span data-stu-id="bcea6-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="bcea6-126">Создайте пространство имен: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`.</span><span class="sxs-lookup"><span data-stu-id="bcea6-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="bcea6-127">Пример:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="bcea6-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="bcea6-128">При создании пространства имен ACS (занимает несколько минут) значения имени и ключа издателя указываются в строке подключения:</span><span class="sxs-lookup"><span data-stu-id="bcea6-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="bcea6-129">Итог:</span><span class="sxs-lookup"><span data-stu-id="bcea6-129">To summarize:</span></span>  
<span data-ttu-id="bcea6-130">имя издателя — SharedSecretIssuer;</span><span class="sxs-lookup"><span data-stu-id="bcea6-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="bcea6-131">ключ издателя — SharedSecretKey.</span><span class="sxs-lookup"><span data-stu-id="bcea6-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="bcea6-132">Дополнительные сведения о командлете [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx).</span><span class="sxs-lookup"><span data-stu-id="bcea6-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="bcea6-133">Имя и ключ издателя шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="bcea6-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="bcea6-134">Имя и ключ издателя шины обслуживания используются службами адаптера BizTalk.</span><span class="sxs-lookup"><span data-stu-id="bcea6-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="bcea6-135">В проекте служб BizTalk в Visual Studio можно использовать службы адаптера BizTalk для подключения к локальной бизнес-системе.</span><span class="sxs-lookup"><span data-stu-id="bcea6-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="bcea6-136">Для подключения создайте бизнес-ретранслятор и введите сведения о бизнес-системе.</span><span class="sxs-lookup"><span data-stu-id="bcea6-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="bcea6-137">При этом также вводится имя и ключ издателя шины обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bcea6-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="bcea6-138">Чтобы извлечь имя и ключ издателя Service Bus</span><span class="sxs-lookup"><span data-stu-id="bcea6-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="bcea6-139">Перейдите на [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="bcea6-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="bcea6-140">В левой области навигации щелкните **Шина обслуживания**.</span><span class="sxs-lookup"><span data-stu-id="bcea6-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="bcea6-141">Выберите пространство имен.</span><span class="sxs-lookup"><span data-stu-id="bcea6-141">Select your namespace.</span></span> <span data-ttu-id="bcea6-142">На панели задач выберите **Сведения о подключении**.</span><span class="sxs-lookup"><span data-stu-id="bcea6-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="bcea6-143">Появятся поля **Издатель по умолчанию** (имя издателя) и **Ключ по умолчанию** (ключ издателя).</span><span class="sxs-lookup"><span data-stu-id="bcea6-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="bcea6-144">Эти значения можно скопировать.</span><span class="sxs-lookup"><span data-stu-id="bcea6-144">Their values can be copied.</span></span>  

<span data-ttu-id="bcea6-145">Итог:</span><span class="sxs-lookup"><span data-stu-id="bcea6-145">To summarize:</span></span>  
<span data-ttu-id="bcea6-146">Имя издателя = издатель по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bcea6-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="bcea6-147">Ключ издателя = ключ по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bcea6-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="bcea6-148">Далее</span><span class="sxs-lookup"><span data-stu-id="bcea6-148">Next</span></span>
<span data-ttu-id="bcea6-149">Дополнительная информация о службах BizTalk в Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="bcea6-150">Установка пакета SDK для служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="bcea6-151">Руководства по службам BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="bcea6-152">Как приступить к работе с пакетом SDK для служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="bcea6-153">Службы BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="bcea6-154">См. также</span><span class="sxs-lookup"><span data-stu-id="bcea6-154">See Also</span></span>
* [<span data-ttu-id="bcea6-155">Инструкция по использованию службы управления ACS для настройки удостоверений службы</span><span class="sxs-lookup"><span data-stu-id="bcea6-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="bcea6-156">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="bcea6-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="bcea6-157">Службы BizTalk: подготовка с использованием классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="bcea6-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="bcea6-158">Службы BizTalk. Диаграмма состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="bcea6-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="bcea6-159">Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»</span><span class="sxs-lookup"><span data-stu-id="bcea6-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="bcea6-160">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="bcea6-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="bcea6-161">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="bcea6-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

