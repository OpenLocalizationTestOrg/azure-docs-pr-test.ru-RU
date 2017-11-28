---
title: "toomanage aaaUsing PowerShell диспетчера трафика в Azure | Документы Microsoft"
description: "Использование PowerShell для диспетчера трафика в Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="ef1a9-103">С помощью PowerShell toomanage диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="ef1a9-104">Диспетчер ресурсов Azure — интерфейс hello предпочтительный управления для служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="ef1a9-105">Профилями диспетчера трафика Azure можно управлять с помощью интерфейсов API и инструментов на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="ef1a9-106">Модель ресурсов</span><span class="sxs-lookup"><span data-stu-id="ef1a9-106">Resource model</span></span>

<span data-ttu-id="ef1a9-107">Для настройки диспетчера трафика используется набор параметров, которые называются профилем.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="ef1a9-108">Этот профиль содержит параметры DNS, параметры маршрутизации трафика, параметров мониторинга конечной точки, а перенаправляется список трафик toowhich конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="ef1a9-109">Каждый профиль диспетчера трафика представлен ресурсом типа TrafficManagerProfiles.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="ef1a9-110">В hello уровень REST API hello URI для каждого профиля выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="ef1a9-111">Настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef1a9-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="ef1a9-112">В данных инструкциях используется Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="ef1a9-113">Hello следующей статье объясняется, как tooinstall и настройка Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="ef1a9-114">Как tooinstall и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef1a9-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="ef1a9-115">Примеры Hello в этой статье предполагается, что существующая группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="ef1a9-116">Можно создать группу ресурсов с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="ef1a9-117">Для Azure Resource Manager необходимо, чтобы все группы ресурсов имели расположение.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="ef1a9-118">Это расположение используется в качестве значения по умолчанию hello для ресурсов, созданных в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="ef1a9-119">Тем не менее поскольку ресурсы профиля диспетчера трафика глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="ef1a9-120">Создание профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="ef1a9-121">использовать профиль диспетчера трафика toocreate hello `New-AzureRmTrafficManagerProfile` командлета:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="ef1a9-122">Привет, в следующей таблице описаны параметры hello:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="ef1a9-123">Параметр</span><span class="sxs-lookup"><span data-stu-id="ef1a9-123">Parameter</span></span> | <span data-ttu-id="ef1a9-124">Описание</span><span class="sxs-lookup"><span data-stu-id="ef1a9-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef1a9-125">Имя</span><span class="sxs-lookup"><span data-stu-id="ef1a9-125">Name</span></span> |<span data-ttu-id="ef1a9-126">Имя ресурса Hello для hello ресурс профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="ef1a9-127">Профили hello же группу ресурсов должны иметь уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="ef1a9-128">Это имя не зависит от hello DNS-имя DNS-запросы.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="ef1a9-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ef1a9-129">ResourceGroupName</span></span> |<span data-ttu-id="ef1a9-130">Имя Hello hello ресурсов группы содержащего hello профиля ресурса.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="ef1a9-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="ef1a9-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="ef1a9-132">Указывает toodetermine маршрутизации трафика метод, используемый hello, какая конечная точка возвращается в ответе DNS-запрос.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="ef1a9-133">Возможные значения: Performance (производительность), Weighted (взвешенный) и Priority (приоритетный).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="ef1a9-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="ef1a9-134">RelativeDnsName</span></span> |<span data-ttu-id="ef1a9-135">Задает hello часть имени узла DNS-имя hello, предоставляемые этим профилем диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="ef1a9-136">Это значение объединяется с hello доменное имя DNS диспетчера трафика Azure tooform hello полное доменное имя (FQDN) профиля hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="ef1a9-137">Например установка значения hello 'Contoso' становится «contoso.trafficmanager.net.»</span><span class="sxs-lookup"><span data-stu-id="ef1a9-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="ef1a9-138">Срок жизни</span><span class="sxs-lookup"><span data-stu-id="ef1a9-138">TTL</span></span> |<span data-ttu-id="ef1a9-139">Указывает hello DNS время жизни (TTL), в секундах.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="ef1a9-140">Это TTL информирует hello локальным распознавателям DNS и DNS-клиенты, как долго toocache ответов DNS, для этого профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="ef1a9-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="ef1a9-141">MonitorProtocol</span></span> |<span data-ttu-id="ef1a9-142">Указывает протокол toouse hello toomonitor-исправности конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="ef1a9-143">Допустимые значения: HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="ef1a9-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="ef1a9-144">MonitorPort</span></span> |<span data-ttu-id="ef1a9-145">Указывает, что hello TCP-порт используется toomonitor исправности конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="ef1a9-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="ef1a9-146">MonitorPath</span></span> |<span data-ttu-id="ef1a9-147">Указывает имя домена конечной точки toohello относительный путь hello tooprobe работоспособности конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="ef1a9-148">Hello командлет создает профиль диспетчера трафика в Azure и возвращает соответствующий tooPowerShell объекта профиля.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="ef1a9-149">На этом этапе hello профиль не содержит конечные точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="ef1a9-150">Дополнительные сведения о добавлении профиля диспетчера трафика tooa конечных точек см. в разделе [Добавление конечных точек диспетчера трафика](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="ef1a9-151">Получение профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="ef1a9-152">использовать существующий объект профиля диспетчера трафика, tooretrieve hello `Get-AzureRmTrafficManagerProfle` командлета:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="ef1a9-153">Этот командлет возвращает профиль объекта трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="ef1a9-154">Изменение профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="ef1a9-155">Изменение профилей диспетчера трафика выполняется в три этапа.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="ef1a9-156">С помощью профиля hello получить `Get-AzureRmTrafficManagerProfile` или используйте профиль hello, возвращенных `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="ef1a9-157">Изменение профиля hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-157">Modify hello profile.</span></span> <span data-ttu-id="ef1a9-158">Можно добавить и удалить конечные точки или изменить параметры профиля или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="ef1a9-159">Эти изменения выполняются в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-159">These changes are off-line operations.</span></span> <span data-ttu-id="ef1a9-160">Изменяются только hello локального объекта в памяти, представляющий профиль hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="ef1a9-161">Фиксация изменений с помощью hello `Set-AzureRmTrafficManagerProfile` командлета.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="ef1a9-162">За исключением RelativeDnsName hello профиль можно изменить все свойства профиля.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="ef1a9-163">toochange hello RelativeDnsName, необходимо удалить профиль и новый профиль с новым именем.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="ef1a9-164">Hello в следующем примере показано, как toochange hello TTL профиля:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="ef1a9-165">Существует три типа конечных точек диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="ef1a9-166">**Конечные точки Azure** — это службы, размещенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="ef1a9-167">**Внешние конечные точки** — службы, размещенные за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="ef1a9-168">**Вложенные конечные точки** представляют собой иерархии используется tooconstruct вложенных профилей диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="ef1a9-169">Вложенные конечные точки позволяют создавать расширенные конфигурации маршрутизации трафика для сложных приложений.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="ef1a9-170">Конечные точки всех трех типов можно добавлять двумя способами.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="ef1a9-171">С помощью описанных выше трех шагов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="ef1a9-172">Преимущество этого метода Hello — несколько конечной точки может выполняться в одно обновление.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="ef1a9-173">С помощью командлета New-AzureRmTrafficManagerEndpoint hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="ef1a9-174">Этот командлет добавляет конечную точку tooan существующего профиля диспетчера трафика в одной операции.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="ef1a9-175">Добавление конечных точек Azure</span><span class="sxs-lookup"><span data-stu-id="ef1a9-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="ef1a9-176">Конечные точки Azure ссылаются на службы, размещенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="ef1a9-177">Поддерживаются два типа конечных точек Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="ef1a9-178">Веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-178">Azure Web Apps</span></span>
2. <span data-ttu-id="ef1a9-179">Ресурсы Azure PublicIpAddress (которые могут быть вложенные tooa подсистемы балансировки нагрузки, или сетевого Адаптера виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="ef1a9-180">Hello PublicIpAddress должен иметь имя DNS, назначенное toobe, используемый в диспетчере трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="ef1a9-181">В каждом случае:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-181">In each case:</span></span>

* <span data-ttu-id="ef1a9-182">Hello службы задается с помощью параметра «с идентификатором targetResourceId» hello `Add-AzureRmTrafficManagerEndpointConfig` или `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="ef1a9-183">Hello «Целевой объект» и «EndpointLocation» содержится в разрешении hello идентификатором TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="ef1a9-184">Указание hello «Weight» является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="ef1a9-185">Весовые коэффициенты используются только в том случае, если профиль hello настроенных toouse метод маршрутизации трафика «Взвешенное» hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="ef1a9-186">В остальных случаях этот параметр игнорируется.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="ef1a9-187">Если указано, hello значение должно быть числом от 1 до 1000.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="ef1a9-188">значение по умолчанию Hello — "1".</span><span class="sxs-lookup"><span data-stu-id="ef1a9-188">hello default value is '1'.</span></span>
* <span data-ttu-id="ef1a9-189">Указание hello «Приоритет» не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="ef1a9-190">Приоритеты используются только в том случае, если профиль hello настроенных toouse метод маршрутизации трафика «Приоритет» hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="ef1a9-191">В остальных случаях этот параметр игнорируется.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="ef1a9-192">Допустимые значения: от 1 too1000 с более низкими значениями, указывающее, более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="ef1a9-193">Если приоритет указан для одной конечной точки, он должен указываться и для всех остальных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="ef1a9-194">Если не указано, по умолчанию значения, начинающиеся с "1" применяются в порядке hello, что перечислены конечные точки hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="ef1a9-195">Пример 1. Добавление конечных точек веб-приложения с помощью командлета `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="ef1a9-196">В этом примере мы создать профиль диспетчера трафика и добавьте две конечные точки веб-приложения с помощью hello `Add-AzureRmTrafficManagerEndpointConfig` командлета.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="ef1a9-197">Пример 2. Добавление конечной точки publicIpAddress с помощью командлета `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="ef1a9-198">В этом примере открытого ресурса IP-адреса добавляется toohello профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="ef1a9-199">Hello общедоступный IP-адрес должен иметь имя DNS настроены и могут быть привязаны либо toohello сетевого Адаптера виртуальной Машины или tooa подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="ef1a9-200">Добавление внешних конечных точек</span><span class="sxs-lookup"><span data-stu-id="ef1a9-200">Adding External Endpoints</span></span>

<span data-ttu-id="ef1a9-201">Трафик Manager использует tooservices трафика toodirect внешние конечные точки, размещенных за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="ef1a9-202">Как и конечные точки Azure, внешние конечные точки можно добавить с помощью командлета `Add-AzureRmTrafficManagerEndpointConfig`, за которым следует командлет `Set-AzureRmTrafficManagerProfile` или `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="ef1a9-203">При добавлении внешних конечных точек:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="ef1a9-204">должно быть указано имя домена Hello конечной точки с помощью параметра «Целевой объект» hello</span><span class="sxs-lookup"><span data-stu-id="ef1a9-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="ef1a9-205">При использовании hello метод маршрутизации трафика «Производительность» hello «EndpointLocation» является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="ef1a9-206">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-206">Otherwise it is optional.</span></span> <span data-ttu-id="ef1a9-207">Hello значение должно быть [имя допустимым регион Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="ef1a9-208">Здравствуйте, «Вес» и «Приоритет» являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="ef1a9-209">Пример 1. Добавление внешних конечных точек с помощью командлетов `Add-AzureRmTrafficManagerEndpointConfig` и `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="ef1a9-210">В этом примере мы создать профиль диспетчера трафика, добавьте две внешние конечные точки и фиксации изменений hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="ef1a9-211">Пример 2. Добавление внешних конечных точек с помощью командлета `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="ef1a9-212">В этом примере мы добавить существующий профиль tooan внешней конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="ef1a9-213">профиль Hello задается с помощью имен групп hello профиля и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="ef1a9-214">Добавление "вложенных" конечных точек</span><span class="sxs-lookup"><span data-stu-id="ef1a9-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="ef1a9-215">Каждый профиль диспетчера трафика определяет один метод маршрутизации трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="ef1a9-216">Однако существуют сценарии, требующие более сложные маршрутизации трафика, чем hello маршрутизации, предоставляемые единый профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="ef1a9-217">Можно вложить профилей диспетчера трафика toocombine преимущества hello более чем один метод маршрутизации трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="ef1a9-218">Вложенные профили позволяют toooverride hello по умолчанию диспетчер трафика поведение toosupport больших и сложных развертываний приложений.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="ef1a9-219">Более подробные примеры см. в статье [Вложенные профили диспетчера трафика](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="ef1a9-220">Вложенные конечные точки настраиваются на родительском профиле hello, с помощью типа конкретной конечной точки, «NestedEndpoints».</span><span class="sxs-lookup"><span data-stu-id="ef1a9-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="ef1a9-221">При указании вложенных конечных точек:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="ef1a9-222">Hello конечной точки должен быть указан с помощью параметра «с идентификатором targetResourceId» hello</span><span class="sxs-lookup"><span data-stu-id="ef1a9-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="ef1a9-223">При использовании hello метод маршрутизации трафика «Производительность» hello «EndpointLocation» является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="ef1a9-224">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-224">Otherwise it is optional.</span></span> <span data-ttu-id="ef1a9-225">Hello значение должно быть [имя допустимым регион Azure](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="ef1a9-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="ef1a9-226">Здравствуйте, «Вес» и «Приоритет» являются необязательными, как и для конечные точки Azure.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="ef1a9-227">параметр «MinChildEndpoints» Hello является необязательным.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="ef1a9-228">значение по умолчанию Hello — "1".</span><span class="sxs-lookup"><span data-stu-id="ef1a9-228">hello default value is '1'.</span></span> <span data-ttu-id="ef1a9-229">Если число доступных конечных точек в hello падает ниже этого значения, hello родительским профилем считает hello дочернем профиле «Деградация» и в результате трафик toohello другим конечным точкам в родительском профиле hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="ef1a9-230">Пример 1. Добавление вложенных конечных точек с помощью командлетов `Add-AzureRmTrafficManagerEndpointConfig` и `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="ef1a9-231">В этом примере мы создать новый диспетчер трафика дочерней и родительской профили, добавить дочерний hello как родитель toohello вложенных конечной точки и фиксации изменений hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="ef1a9-232">Для краткости в этом примере мы не добавил другие конечные точки toohello дочерних или родительских профили.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="ef1a9-233">Пример 2. Добавление вложенных конечных точек с помощью командлета `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="ef1a9-234">В этом примере мы добавить существующий профиль дочерних как родительский профиль существующих tooan вложенных конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="ef1a9-235">профиль Hello задается с помощью имен групп hello профиля и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="ef1a9-236">Обновление конечной точки диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="ef1a9-237">Существует два способа tooupdate существующую конечную точку диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="ef1a9-238">Получить с помощью профиля диспетчера трафика hello `Get-AzureRmTrafficManagerProfile`, обновить hello свойства конечной точки в профиле hello и фиксации изменений hello, с помощью `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="ef1a9-239">Этот метод имеет hello преимущество может tooupdate более одной конечной точки в одной операции.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="ef1a9-240">Получить hello конечной точки диспетчера трафика с помощью `Get-AzureRmTrafficManagerEndpoint`, обновить свойства конечной точки hello и фиксации изменений hello, с помощью `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="ef1a9-241">Этот способ проще, так как он не требует индексирование в массиве hello конечных точек в профиле hello.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="ef1a9-242">Пример 1. Обновление конечных точек с помощью командлетов `Get-AzureRmTrafficManagerProfile` и `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="ef1a9-243">В этом примере мы изменение приоритета hello на две конечные точки в пределах существующего профиля.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="ef1a9-244">Пример 2. Обновление конечной точки с помощью командлетов `Get-AzureRmTrafficManagerEndpoint` и `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="ef1a9-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="ef1a9-245">В этом примере мы изменить вес hello одну конечную точку в существующий профиль.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="ef1a9-246">Включение и отключение конечных точек и профилей</span><span class="sxs-lookup"><span data-stu-id="ef1a9-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="ef1a9-247">Диспетчер трафика позволяет toobe отдельные конечные точки включенных и отключенных предоставлять Включение и отключение всего профилей.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="ef1a9-248">Эти изменения можно внести ресурсами конечная точка либо профиль hello получения и обновления или установки.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="ef1a9-249">toostreamline этих общих операций, также поддерживаются через специализированные командлеты.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="ef1a9-250">Пример 1. Включение и отключение профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="ef1a9-251">использовать профиль диспетчера трафика tooenable `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="ef1a9-252">Hello профиля можно указать с помощью объекта профиля.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="ef1a9-253">Hello объекта профиля можно передать по конвейеру hello, или с помощью hello "-TrafficManagerProfile" параметра.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="ef1a9-254">В этом примере мы укажите профиль hello hello профиля и ресурсов групп по имени.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="ef1a9-255">toodisable профиль диспетчера трафика:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="ef1a9-256">командлет Disable-AzureRmTrafficManagerProfile Hello запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="ef1a9-257">Это предупреждение можно подавить при помощи hello '-Force "параметра.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="ef1a9-258">Пример 2. Включение и отключение конечной точки диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="ef1a9-259">использовать конечную точку диспетчера трафика, tooenable `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="ef1a9-260">Существует два способа toospecify hello endpoint</span><span class="sxs-lookup"><span data-stu-id="ef1a9-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="ef1a9-261">С помощью TrafficManagerEndpoint объект, переданный через конвейер hello или hello "-TrafficManagerEndpoint" параметра</span><span class="sxs-lookup"><span data-stu-id="ef1a9-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="ef1a9-262">Использование имени конечной точки hello, тип конечной точки, имя профиля и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="ef1a9-263">Аналогичным образом toodisable конечную точку диспетчера трафика:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="ef1a9-264">Как и в `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` командлет запросит подтверждение.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="ef1a9-265">Это предупреждение можно подавить при помощи hello '-Force "параметра.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="ef1a9-266">Удаление конечной точки диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="ef1a9-267">использовать отдельные конечные точки tooremove hello `Remove-AzureRmTrafficManagerEndpoint` командлета:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="ef1a9-268">Этот командлет запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="ef1a9-269">Это предупреждение можно подавить при помощи hello '-Force "параметра.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="ef1a9-270">Удаление профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="ef1a9-271">использовать профиль диспетчера трафика toodelete hello `Remove-AzureRmTrafficManagerProfile` командлета, указание имен hello профиля и ресурсов группы:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="ef1a9-272">Этот командлет запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="ef1a9-273">Это предупреждение можно подавить при помощи hello '-Force "параметра.</span><span class="sxs-lookup"><span data-stu-id="ef1a9-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="ef1a9-274">удалить toobe профиль Hello могут быть указаны с помощью объекта профиля:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="ef1a9-275">Эти операции также можно объединить в последовательность:</span><span class="sxs-lookup"><span data-stu-id="ef1a9-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="ef1a9-276">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef1a9-276">Next steps</span></span>

[<span data-ttu-id="ef1a9-277">Мониторинг диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="ef1a9-278">Рекомендации по безопасности для диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="ef1a9-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
