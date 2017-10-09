---
title: "toouse aaaHow API управления Azure с внутреннюю виртуальную сеть | Документы Microsoft"
description: "Узнайте, как toosetup и настройка службы управления API Azure в внутреннюю виртуальную сеть."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="b0c60-103">Использование службы управления API Azure совместно с внутренней виртуальной сетью</span><span class="sxs-lookup"><span data-stu-id="b0c60-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="b0c60-104">API управления Azure виртуальных сетей (Vnet), позволяет управлять API-интерфейсы не доступен в Интернете hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="b0c60-105">Число технологии виртуальных частных СЕТЕЙ, доступных toomake hello подключения и управления API может быть развернуто на два основных режима внутри hello виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="b0c60-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="b0c60-106">Внешний</span><span class="sxs-lookup"><span data-stu-id="b0c60-106">External</span></span>
* <span data-ttu-id="b0c60-107">Внутренний</span><span class="sxs-lookup"><span data-stu-id="b0c60-107">Internal</span></span>

## <span data-ttu-id="b0c60-108"><a name="overview"> </a>Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="b0c60-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="b0c60-109">При развертывании управления API в режиме внутренней виртуальной сети все hello конечные точки службы (шлюза, портал разработчиков, портал издателя, прямого управления и Git) отображаются только внутри виртуальной сети, управления доступом к.</span><span class="sxs-lookup"><span data-stu-id="b0c60-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="b0c60-110">Ни одна из конечных точек службы hello регистрируются на общедоступном DNS-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="b0c60-111">С помощью API управления в режиме внутренней можно добиться hello следующие сценарии</span><span class="sxs-lookup"><span data-stu-id="b0c60-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="b0c60-112">безопасно предоставлять третьим лицам доступ к API, размещенным в частном центре обработки данных, с помощью VPN-подключений типа "сеть —сеть" или ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="b0c60-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="b0c60-113">поддерживать сценарии гибридного облака, предоставляя облачные и локально размещенные API-интерфейсы через общий шлюз;</span><span class="sxs-lookup"><span data-stu-id="b0c60-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="b0c60-114">управлять API-интерфейсами, размещенными в разных географических расположениях, через одну общую конечную точку шлюза.</span><span class="sxs-lookup"><span data-stu-id="b0c60-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="b0c60-115"><a name="enable-vpn"> </a>Создание управления API во внутренней виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b0c60-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="b0c60-116">за внутреннего Balancer(ILB) нагрузки размещается Hello службе управления API в внутренней виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0c60-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="b0c60-117">Hello hello ILB IP-адрес находится в hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) диапазона.</span><span class="sxs-lookup"><span data-stu-id="b0c60-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="b0c60-118">Активация подключения к виртуальной сети с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b0c60-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="b0c60-119">Сначала создать службу управления API hello, выполните действия hello [службы управления API создания][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="b0c60-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="b0c60-120">Затем toobe управления API настройки, развернута внутри виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0c60-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Меню настройки APIM во внутренней виртуальной сети][api-management-using-internal-vnet-menu]

<span data-ttu-id="b0c60-122">После успешного завершения развертывания hello hello внутренний виртуальный IP-адрес службы появится на панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Панель мониторинга управления API с настроенной внутренней сетью][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="b0c60-124">Активация подключения к виртуальной сети с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0c60-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="b0c60-125">Можно также включить подключения к виртуальной сети с помощью командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="b0c60-126">**Создание службы управления API внутри виртуальной сети**: с помощью командлета hello [New AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate управления API Azure службы внутри виртуальной сети и настроить его тип внутренней виртуальной сети toouse hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="b0c60-127">**Развернуть существующую службу управления API внутри виртуальной сети**: с помощью командлета hello [AzureRmApiManagementDeployment обновление](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove существующие Azure API Management службы внутри виртуальной сети и настроить его toouse Внутренний тип виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0c60-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="b0c60-128"><a name="apim-dns-configuration"></a>Настройка DNS</span><span class="sxs-lookup"><span data-stu-id="b0c60-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="b0c60-129">Когда вы используете управление API во внешнем режиме виртуальной сети, службой DNS управляет Azure.</span><span class="sxs-lookup"><span data-stu-id="b0c60-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="b0c60-130">Для режима внутренней виртуальной сети у вас toomanage собственные DNS.</span><span class="sxs-lookup"><span data-stu-id="b0c60-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="b0c60-131">Служба управления API не прослушивает toorequests, поступающий на IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="b0c60-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="b0c60-132">Отвечает только toorequests toohello имя узла настроен на его конечные точки службы (которая включает шлюза, портал разработчиков, портал издателя, конечная точка прямого управления и git).</span><span class="sxs-lookup"><span data-stu-id="b0c60-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="b0c60-133">По умолчанию используются такие имена узлов:</span><span class="sxs-lookup"><span data-stu-id="b0c60-133">Access on default host names:</span></span>
<span data-ttu-id="b0c60-134">При создании API управления службы в общедоступном облаке Azure, например с именем «contoso», hello следующих конечных точек службы настраиваются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b0c60-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="b0c60-135">шлюз или прокси — contoso.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="b0c60-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="b0c60-136">портал издателя и портал для разработчиков — contoso.portal.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="b0c60-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="b0c60-137">конечная точка прямого управления — contoso.management.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="b0c60-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="b0c60-138">Git — contoso.scm.azure-api.net.</span><span class="sxs-lookup"><span data-stu-id="b0c60-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="b0c60-139">tooaccess эти конечные точки службы управления API, можно создать виртуальную машину в виртуальной сети toohello подсетью и подключенная, в которой развертывается API управления.</span><span class="sxs-lookup"><span data-stu-id="b0c60-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="b0c60-140">При условии hello внутренний виртуальный IP-адрес для службы 10.0.0.5, можно сделать hello сопоставления файлов узлов (% SystemDrive%\drivers\etc\hosts) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b0c60-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="b0c60-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b0c60-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="b0c60-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b0c60-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="b0c60-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b0c60-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="b0c60-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b0c60-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="b0c60-145">Можно затем получить все конечные точки службы hello из виртуальной машины, созданную hello.</span><span class="sxs-lookup"><span data-stu-id="b0c60-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="b0c60-146">Если вы используете пользовательский DNS-сервер в виртуальной сети, можно создать соответствующие записи DNS типа A. Тогда доступ к конечным точкам будет возможен из любого расположения в пределах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0c60-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="b0c60-147">Доступ по пользовательским доменным именам</span><span class="sxs-lookup"><span data-stu-id="b0c60-147">Access on custom domain names:</span></span>
<span data-ttu-id="b0c60-148">Если вы не хотите tooaccess приветствия имен узлов по умолчанию hello в службе управления API, вы можете настроить пользовательские доменные имена для всех конечных точек службы, такие как ниже</span><span class="sxs-lookup"><span data-stu-id="b0c60-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Настройка пользовательского домена для управления API][api-management-custom-domain-name]

<span data-ttu-id="b0c60-150">Затем можно создать записи в вашей tooaccess DNS-сервер этих конечных точек, которые доступны только внутри виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0c60-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="b0c60-151"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="b0c60-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="b0c60-152">Обзор [распространенных проблем с конфигурацией сети при настройке APIM в виртуальной сети][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="b0c60-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="b0c60-153">Часто задаваемые вопросы по виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b0c60-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* <span data-ttu-id="b0c60-154">Инструкции по [созданию записей DNS типа A](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span><span class="sxs-lookup"><span data-stu-id="b0c60-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span></span>

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
