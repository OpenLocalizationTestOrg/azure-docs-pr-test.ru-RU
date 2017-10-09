---
title: "aaaManage CDN Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toouse hello toomanage командлеты Azure PowerShell Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="84f03-103">Управление Azure CDN с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f03-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="84f03-104">PowerShell предоставляет один из наиболее гибкие методы toomanage hello профили Azure CDN и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="84f03-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="84f03-105">PowerShell можно использовать в интерактивном режиме или путем написания скриптов tooautomate задач управления.</span><span class="sxs-lookup"><span data-stu-id="84f03-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="84f03-106">В этом учебнике показано несколько hello наиболее распространенные задачи можно выполнить с PowerShell toomanage профили Azure CDN и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="84f03-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84f03-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84f03-107">Prerequisites</span></span>
<span data-ttu-id="84f03-108">toouse PowerShell toomanage профили Azure CDN и конечных точек, то должен быть установлен модуль Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="84f03-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="84f03-109">toolearn как tooinstall Azure PowerShell и подключитесь с помощью hello tooAzure `Login-AzureRmAccount` командлета, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84f03-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84f03-110">Чтобы выполнять командлеты Azure PowerShell, необходимо сначала войти в систему с помощью `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="84f03-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="84f03-111">Список командлетов Azure CDN hello</span><span class="sxs-lookup"><span data-stu-id="84f03-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="84f03-112">Вы можете вывести список всех командлетов hello Azure CDN, с помощью hello `Get-Command` командлета.</span><span class="sxs-lookup"><span data-stu-id="84f03-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="84f03-113">Получение справки</span><span class="sxs-lookup"><span data-stu-id="84f03-113">Getting help</span></span>
<span data-ttu-id="84f03-114">Справку можно получить с помощью этих командлетов, с помощью hello `Get-Help` командлета.</span><span class="sxs-lookup"><span data-stu-id="84f03-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="84f03-115">`Get-Help` описывает назначение и синтаксис командлетов, а для некоторых из них приводит примеры.</span><span class="sxs-lookup"><span data-stu-id="84f03-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="84f03-116">Получение списка существующих профилей Azure CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="84f03-117">Hello `Get-AzureRmCdnProfile` командлет без параметров возвращает все существующие CDN профили.</span><span class="sxs-lookup"><span data-stu-id="84f03-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="84f03-118">Эти выходные данные могут быть выведенной toocmdlets для перечисления.</span><span class="sxs-lookup"><span data-stu-id="84f03-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="84f03-119">Можно также вернуть одного профиля, указав hello профиль имени и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="84f03-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="84f03-120">Это возможно toohave CDN несколько профилей с hello точно такое же имя, при условии, что они находятся в разных группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="84f03-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="84f03-121">Пропуск hello `ResourceGroupName` параметр Возвращает все профили с соответствующим именем.</span><span class="sxs-lookup"><span data-stu-id="84f03-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="84f03-122">Получение списка существующих конечных точек CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="84f03-123">`Get-AzureRmCdnEndpoint`можно получить конечную точку отдельных или всех конечных точек hello в профиле.</span><span class="sxs-lookup"><span data-stu-id="84f03-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="84f03-124">Создание конечных точек и профилей CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="84f03-125">`New-AzureRmCdnProfile`и `New-AzureRmCdnEndpoint` , используемые toocreate CDN профилей и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="84f03-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="84f03-126">Проверка доступности имени конечной точки</span><span class="sxs-lookup"><span data-stu-id="84f03-126">Checking endpoint name availability</span></span>
<span data-ttu-id="84f03-127">`Get-AzureRmCdnEndpointNameAvailability` возвращает объект с информацией о том, свободно ли указанное имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="84f03-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="84f03-128">Добавление пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="84f03-128">Adding a custom domain</span></span>
<span data-ttu-id="84f03-129">`New-AzureRmCdnCustomDomain`Добавляет существующий конечную tooan имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="84f03-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84f03-130">Необходимо настроить hello CNAME у поставщика DNS, как описано в [как toomap пользовательский домен tooContent сети Доставки endpoint](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="84f03-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="84f03-131">Вы можете протестировать сопоставление hello перед изменением конечной точки с помощью `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="84f03-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="84f03-132">Изменение конечной точки</span><span class="sxs-lookup"><span data-stu-id="84f03-132">Modifying an endpoint</span></span>
<span data-ttu-id="84f03-133">`Set-AzureRmCdnEndpoint` изменяет существующую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="84f03-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="84f03-134">Очистка и предварительная загрузка ресурсов CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="84f03-135">`Unpublish-AzureRmCdnEndpointContent` очищает все кэшированные ресурсы, а `Publish-AzureRmCdnEndpointContent` предварительно загружает ресурсы на всех поддерживаемых конечных точках.</span><span class="sxs-lookup"><span data-stu-id="84f03-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="84f03-136">Запуск и остановка конечных точек CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="84f03-137">`Start-AzureRmCdnEndpoint`и `Stop-AzureRmCdnEndpoint` можно использовать toostart и остановить отдельные конечные точки или группы конечных точек.</span><span class="sxs-lookup"><span data-stu-id="84f03-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="84f03-138">Удаление ресурсов CDN</span><span class="sxs-lookup"><span data-stu-id="84f03-138">Deleting CDN resources</span></span>
<span data-ttu-id="84f03-139">`Remove-AzureRmCdnProfile`и `Remove-AzureRmCdnEndpoint` может быть профилей используется tooremove и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="84f03-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="84f03-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84f03-140">Next Steps</span></span>
<span data-ttu-id="84f03-141">Узнайте, как tooautomate Azure CDN с [.NET](cdn-app-dev-net.md) или [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="84f03-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="84f03-142">toolearn о возможностях CDN, в разделе [Обзор CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84f03-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

