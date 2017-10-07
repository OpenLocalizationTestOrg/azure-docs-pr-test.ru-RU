---
title: "aaaIssuer имя и ключ поставщика в службах BizTalk | Документы Microsoft"
description: "Дополнительные сведения о том, как tooretrieve имя издателя и ключ издателя для шины обслуживания или управления доступом (ACS) в службах BizTalk. MABS, WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="62498-104">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="62498-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="62498-105">Службы BizTalk Azure использует hello имя издателя шины обслуживания и ключ издателя и hello имя издателя контроля доступа и ключ издателя.</span><span class="sxs-lookup"><span data-stu-id="62498-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="62498-106">В частности:</span><span class="sxs-lookup"><span data-stu-id="62498-106">Specifically:</span></span>

| <span data-ttu-id="62498-107">Задача</span><span class="sxs-lookup"><span data-stu-id="62498-107">Task</span></span> | <span data-ttu-id="62498-108">Используемые имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="62498-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="62498-109">Развертывание приложения из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62498-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="62498-110">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="62498-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="62498-111">Настройка hello портале служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="62498-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="62498-112">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="62498-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="62498-113">Создание ретрансляции больших двоичных ОБЪЕКТОВ с hello службы адаптера BizTalk в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62498-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="62498-114">Имя и ключ издателя шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="62498-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="62498-115">В этом разделе перечислены hello действия tooretrieve hello имя издателя и ключ издателя.</span><span class="sxs-lookup"><span data-stu-id="62498-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="62498-116">Имя и ключ издателя для службы Access Control</span><span class="sxs-lookup"><span data-stu-id="62498-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="62498-117">Hello имя издателя контроля доступа и ключ издателя используются hello следующее:</span><span class="sxs-lookup"><span data-stu-id="62498-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="62498-118">Приложение службы Azure BizTalk, созданных в Visual Studio: toosuccessfully развернуть приложение службы BizTalk в Visual Studio tooAzure, введите имя издателя контроля доступа hello и ключ издателя.</span><span class="sxs-lookup"><span data-stu-id="62498-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="62498-119">Hello портале служб BizTalk Azure: при создание службы BizTalk откройте hello портале служб BizTalk, имя издателя управления доступом и ключ издателя автоматически регистрируются для развертываний с hello одинаковые значения для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="62498-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="62498-120">Получить hello имя издателя контроля доступа и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="62498-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="62498-121">toouse ACS для проверки подлинности и get Здравствуйте значения имени издателя и ключ издателя, hello общие шаги включают:</span><span class="sxs-lookup"><span data-stu-id="62498-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="62498-122">Установка hello [командлетов Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="62498-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="62498-123">Добавьте учетную запись Azure: `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="62498-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="62498-124">Получите имя подписки: `get-azuresubscription`.</span><span class="sxs-lookup"><span data-stu-id="62498-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="62498-125">Выберите свою подписку: `select-azuresubscription <name of your subscription>`.</span><span class="sxs-lookup"><span data-stu-id="62498-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="62498-126">Создайте пространство имен: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`.</span><span class="sxs-lookup"><span data-stu-id="62498-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="62498-127">Пример:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="62498-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="62498-128">Когда создается новое пространство имен ACS hello (это может занять несколько минут), hello имя издателя и ключ издателя значения перечислены в строке подключения hello:</span><span class="sxs-lookup"><span data-stu-id="62498-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="62498-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="62498-129">toosummarize:</span></span>  
<span data-ttu-id="62498-130">имя издателя — SharedSecretIssuer;</span><span class="sxs-lookup"><span data-stu-id="62498-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="62498-131">ключ издателя — SharedSecretKey.</span><span class="sxs-lookup"><span data-stu-id="62498-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="62498-132">Подробнее об hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="62498-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="62498-133">Имя и ключ издателя шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="62498-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="62498-134">Имя и ключ издателя шины обслуживания используются службами адаптера BizTalk.</span><span class="sxs-lookup"><span data-stu-id="62498-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="62498-135">В проекте службы BizTalk в Visual Studio используйте Line of Business (LOB) hello службы адаптера BizTalk tooconnect tooan в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="62498-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="62498-136">tooconnect, создать hello посредника LOB и введите свои данные системы LOB.</span><span class="sxs-lookup"><span data-stu-id="62498-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="62498-137">При этом также введите имя издателя шины обслуживания hello и ключ издателя.</span><span class="sxs-lookup"><span data-stu-id="62498-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="62498-138">hello tooretrieve имя издателя шины обслуживания и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="62498-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="62498-139">Войдите в toohello [классический портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="62498-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="62498-140">В области навигации слева hello выберите **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="62498-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="62498-141">Выберите пространство имен.</span><span class="sxs-lookup"><span data-stu-id="62498-141">Select your namespace.</span></span> <span data-ttu-id="62498-142">На панели задач hello, выберите **сведения о соединении**.</span><span class="sxs-lookup"><span data-stu-id="62498-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="62498-143">При этом отображаются hello **поставщика по умолчанию** (имя поставщика) и **ключ по умолчанию** (ключ).</span><span class="sxs-lookup"><span data-stu-id="62498-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="62498-144">Эти значения можно скопировать.</span><span class="sxs-lookup"><span data-stu-id="62498-144">Their values can be copied.</span></span>  

<span data-ttu-id="62498-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="62498-145">toosummarize:</span></span>  
<span data-ttu-id="62498-146">Имя издателя = издатель по умолчанию</span><span class="sxs-lookup"><span data-stu-id="62498-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="62498-147">Ключ издателя = ключ по умолчанию</span><span class="sxs-lookup"><span data-stu-id="62498-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="62498-148">Далее</span><span class="sxs-lookup"><span data-stu-id="62498-148">Next</span></span>
<span data-ttu-id="62498-149">Дополнительная информация о службах BizTalk в Azure</span><span class="sxs-lookup"><span data-stu-id="62498-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="62498-150">Установка пакета SDK служб BizTalk Azure hello</span><span class="sxs-lookup"><span data-stu-id="62498-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="62498-151">Руководства по службам BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="62498-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="62498-152">Как я запустить с помощью hello пакета SDK служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="62498-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="62498-153">Службы BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="62498-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="62498-154">См. также</span><span class="sxs-lookup"><span data-stu-id="62498-154">See Also</span></span>
* [<span data-ttu-id="62498-155">Как: использование службы управления ACS tooConfigure удостоверения службы</span><span class="sxs-lookup"><span data-stu-id="62498-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="62498-156">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="62498-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="62498-157">Службы BizTalk: подготовка с использованием классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="62498-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="62498-158">Службы BizTalk. Диаграмма состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="62498-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="62498-159">Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»</span><span class="sxs-lookup"><span data-stu-id="62498-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="62498-160">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="62498-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="62498-161">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="62498-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

