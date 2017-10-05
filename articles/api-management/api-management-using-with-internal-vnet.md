---
title: "Как использовать управление API Azure с внутренними виртуальными сетями | Документация Майкрософт"
description: "Узнайте, как установить и настроить управление API Azure во внутренней виртуальной сети."
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
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="7173f-103">Использование службы управления API Azure совместно с внутренней виртуальной сетью</span><span class="sxs-lookup"><span data-stu-id="7173f-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="7173f-104">Используемая с виртуальными сетями Azure служба управления API Azure позволяет работать с интерфейсами API, которые недоступны из Интернета.</span><span class="sxs-lookup"><span data-stu-id="7173f-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="7173f-105">Такие подключения устанавливаются с помощью разных средств, а служба управления API может быть развернута в одном из двух режимов.</span><span class="sxs-lookup"><span data-stu-id="7173f-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="7173f-106">Внешний</span><span class="sxs-lookup"><span data-stu-id="7173f-106">External</span></span>
* <span data-ttu-id="7173f-107">Внутренний</span><span class="sxs-lookup"><span data-stu-id="7173f-107">Internal</span></span>

## <span data-ttu-id="7173f-108"><a name="overview"> </a>Содержание раздела</span><span class="sxs-lookup"><span data-stu-id="7173f-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="7173f-109">Когда вы развертываете управление API во внутреннем режиме виртуальной сети, все конечные точки службы (шлюз, портал разработчика, портал издателя, конечная точка прямого управления и Git) отображаются только в пределах виртуальной сети, доступ к которой вы контролируете.</span><span class="sxs-lookup"><span data-stu-id="7173f-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="7173f-110">Ни одна из конечных точек службы не регистрируется на общедоступных DNS-серверах.</span><span class="sxs-lookup"><span data-stu-id="7173f-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="7173f-111">Используя управление API во внутреннем режиме, вы можете реализовать следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="7173f-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="7173f-112">безопасно предоставлять третьим лицам доступ к API, размещенным в частном центре обработки данных, с помощью VPN-подключений типа "сеть —сеть" или ExpressRoute;</span><span class="sxs-lookup"><span data-stu-id="7173f-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="7173f-113">поддерживать сценарии гибридного облака, предоставляя облачные и локально размещенные API-интерфейсы через общий шлюз;</span><span class="sxs-lookup"><span data-stu-id="7173f-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="7173f-114">управлять API-интерфейсами, размещенными в разных географических расположениях, через одну общую конечную точку шлюза.</span><span class="sxs-lookup"><span data-stu-id="7173f-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="7173f-115"><a name="enable-vpn"> </a>Создание управления API во внутренней виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="7173f-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="7173f-116">Служба управления API во внутренней виртуальной сети размещается за внутренней подсистемой балансировки нагрузки (ILB).</span><span class="sxs-lookup"><span data-stu-id="7173f-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="7173f-117">IP-адрес ILB находится в диапазоне [RFC1918](http://www.faqs.org/rfcs/rfc1918.html).</span><span class="sxs-lookup"><span data-stu-id="7173f-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="7173f-118">Активация подключения к виртуальной сети с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="7173f-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="7173f-119">Сначала создайте службу управления API, выполнив действия из раздела [Создание экземпляра управления API][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="7173f-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="7173f-120">Затем укажите, что управление API будет развертываться в пределах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7173f-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Меню настройки APIM во внутренней виртуальной сети][api-management-using-internal-vnet-menu]

<span data-ttu-id="7173f-122">Завершив развертывание, вы увидите на панели мониторинга внутренний виртуальный IP-адрес вашей службы.</span><span class="sxs-lookup"><span data-stu-id="7173f-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Панель мониторинга управления API с настроенной внутренней сетью][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="7173f-124">Активация подключения к виртуальной сети с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="7173f-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="7173f-125">Подключение к виртуальной сети можно также активировать с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7173f-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="7173f-126">**Создание службы управления API в виртуальной сети**. Чтобы создать в виртуальной сети службу управления API Azure и настроить для нее внутренний режим виртуальной сети, используйте командлет [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement).</span><span class="sxs-lookup"><span data-stu-id="7173f-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="7173f-127">**Развертывание существующей службы управления API в виртуальной сети**. Чтобы переместить в виртуальную сеть существующую службу управления API Azure и настроить для нее внутренний режим виртуальной сети, используйте командлет [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment).</span><span class="sxs-lookup"><span data-stu-id="7173f-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="7173f-128"><a name="apim-dns-configuration"></a>Настройка DNS</span><span class="sxs-lookup"><span data-stu-id="7173f-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="7173f-129">Когда вы используете управление API во внешнем режиме виртуальной сети, службой DNS управляет Azure.</span><span class="sxs-lookup"><span data-stu-id="7173f-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="7173f-130">Чтобы использовать внутренний режим виртуальной сети, управлять DNS вы должны самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="7173f-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="7173f-131">Служба управления API не прослушивает запросы, поступающие по IP-адресам.</span><span class="sxs-lookup"><span data-stu-id="7173f-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="7173f-132">Она отвечает только на запросы, в которых указаны имена узлов, настроенные для конечных точек этой службы (включая шлюз, портал для разработчиков, портал издателя, конечную точку прямого управления и Git).</span><span class="sxs-lookup"><span data-stu-id="7173f-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="7173f-133">По умолчанию используются такие имена узлов:</span><span class="sxs-lookup"><span data-stu-id="7173f-133">Access on default host names:</span></span>
<span data-ttu-id="7173f-134">Например, при создании службы управления API в общедоступном облаке Azure с именем contoso будут по умолчанию настроены следующие конечные точки службы:</span><span class="sxs-lookup"><span data-stu-id="7173f-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="7173f-135">шлюз или прокси — contoso.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="7173f-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="7173f-136">портал издателя и портал для разработчиков — contoso.portal.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="7173f-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7173f-137">конечная точка прямого управления — contoso.management.azure api.net;</span><span class="sxs-lookup"><span data-stu-id="7173f-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="7173f-138">Git — contoso.scm.azure-api.net.</span><span class="sxs-lookup"><span data-stu-id="7173f-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7173f-139">Для получения доступа к этим конечным точкам службы управления API, можно создать виртуальную машину в подсети, подключенной к виртуальной сети, в которой развернута служба управления API.</span><span class="sxs-lookup"><span data-stu-id="7173f-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="7173f-140">Если для службы используется внутренний виртуальный IP-адрес 10.0.0.5, в файле hosts (расположен по адресу %системный_диск%\drivers\etc\hosts) можно задать следующие сопоставления:</span><span class="sxs-lookup"><span data-stu-id="7173f-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="7173f-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7173f-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="7173f-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7173f-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7173f-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7173f-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="7173f-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7173f-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7173f-145">Теперь с созданной виртуальной машины вы сможете обращаться к любой из конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="7173f-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="7173f-146">Если вы используете пользовательский DNS-сервер в виртуальной сети, можно создать соответствующие записи DNS типа A. Тогда доступ к конечным точкам будет возможен из любого расположения в пределах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7173f-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="7173f-147">Доступ по пользовательским доменным именам</span><span class="sxs-lookup"><span data-stu-id="7173f-147">Access on custom domain names:</span></span>
<span data-ttu-id="7173f-148">Если для обращения к службе управления API вы не хотите использовать имена узлов по умолчанию, для всех конечных точек службы можно настроить пользовательские доменные имена, как указано ниже:</span><span class="sxs-lookup"><span data-stu-id="7173f-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Настройка пользовательского домена для управления API][api-management-custom-domain-name]

<span data-ttu-id="7173f-150">После этого создайте на DNS-сервере записи тип A для обращения к этим конечным точкам, которые будут доступны только в пределах виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7173f-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="7173f-151"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="7173f-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="7173f-152">Обзор [распространенных проблем с конфигурацией сети при настройке APIM в виртуальной сети][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="7173f-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="7173f-153">Часто задаваемые вопросы по виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="7173f-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* <span data-ttu-id="7173f-154">Инструкции по [созданию записей DNS типа A](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span><span class="sxs-lookup"><span data-stu-id="7173f-154">[Creating A record in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)</span></span>

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
