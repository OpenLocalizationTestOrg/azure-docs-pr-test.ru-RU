---
title: "aaaManage учетные записи служб мультимедиа Azure с помощью PowerShell"
description: "Узнайте, как учетные записи служб мультимедиа Azure toomanage с помощью командлетов PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="738d3-103">Управление учетными записями служб мультимедиа Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="738d3-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="738d3-104">Портал</span><span class="sxs-lookup"><span data-stu-id="738d3-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="738d3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="738d3-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="738d3-106">REST</span><span class="sxs-lookup"><span data-stu-id="738d3-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="738d3-107">toocreate toobe доступ учетной записи служб мультимедиа Azure, необходимо иметь учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="738d3-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="738d3-108">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="738d3-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="738d3-109">Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="738d3-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="738d3-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="738d3-110">Overview</span></span>
<span data-ttu-id="738d3-111">В этой статье перечислены hello командлетов Azure PowerShell для служб мультимедиа Azure (AMS) в framework hello диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="738d3-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="738d3-112">Существуют командлеты Hello в hello **Microsoft.Azure.Commands.Media** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="738d3-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="738d3-113">Версии</span><span class="sxs-lookup"><span data-stu-id="738d3-113">Versions</span></span>
<span data-ttu-id="738d3-114">**ApiVersion**: от 01.10.2015.</span><span class="sxs-lookup"><span data-stu-id="738d3-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="738d3-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="738d3-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="738d3-116">Создает службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-117">Syntax</span></span>
<span data-ttu-id="738d3-118">Набор параметров: StorageAccountIdParamSet.</span><span class="sxs-lookup"><span data-stu-id="738d3-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="738d3-119">Набор параметров: StorageAccountsParamSet.</span><span class="sxs-lookup"><span data-stu-id="738d3-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-120">Parameters</span></span>
<span data-ttu-id="738d3-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-122">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-123">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-123">Aliases</span></span> | <span data-ttu-id="738d3-124">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-125">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-125">Required?</span></span> |<span data-ttu-id="738d3-126">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-126">true</span></span> |
| <span data-ttu-id="738d3-127">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-127">Position?</span></span> |<span data-ttu-id="738d3-128">0</span><span class="sxs-lookup"><span data-stu-id="738d3-128">0</span></span> |
| <span data-ttu-id="738d3-129">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-129">Default value</span></span> |<span data-ttu-id="738d3-130">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-130">none</span></span> |
| <span data-ttu-id="738d3-131">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-131">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-133">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-133">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-134">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-134">false</span></span> |

<span data-ttu-id="738d3-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-136">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-137">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-137">Aliases</span></span> | <span data-ttu-id="738d3-138">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="738d3-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-139">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-139">Required?</span></span> |<span data-ttu-id="738d3-140">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-140">true</span></span> |
| <span data-ttu-id="738d3-141">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-141">Position?</span></span> |<span data-ttu-id="738d3-142">1</span><span class="sxs-lookup"><span data-stu-id="738d3-142">1</span></span> |
| <span data-ttu-id="738d3-143">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-143">Default value</span></span> |<span data-ttu-id="738d3-144">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-144">none</span></span> |
| <span data-ttu-id="738d3-145">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-145">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-146">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-146">false</span></span> |
| <span data-ttu-id="738d3-147">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-147">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-148">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-148">false</span></span> |

<span data-ttu-id="738d3-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-150">Указывает расположение ресурса hello hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="738d3-151">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-151">Aliases</span></span> | <span data-ttu-id="738d3-152">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-153">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-153">Required?</span></span> |<span data-ttu-id="738d3-154">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-154">true</span></span> |
| <span data-ttu-id="738d3-155">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-155">Position?</span></span> |<span data-ttu-id="738d3-156">2</span><span class="sxs-lookup"><span data-stu-id="738d3-156">2</span></span> |
| <span data-ttu-id="738d3-157">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-157">Default value</span></span> |<span data-ttu-id="738d3-158">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-158">none</span></span> |
| <span data-ttu-id="738d3-159">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-159">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-161">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-161">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-162">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-162">false</span></span> |

<span data-ttu-id="738d3-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-164">Указывает учетную запись основного хранилища, связанный с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="738d3-165">Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.</span><span class="sxs-lookup"><span data-stu-id="738d3-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="738d3-166">Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="738d3-167">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-167">Aliases</span></span> | <span data-ttu-id="738d3-168">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-169">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-169">Required?</span></span> |<span data-ttu-id="738d3-170">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-170">true</span></span> |
| <span data-ttu-id="738d3-171">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-171">Position?</span></span> |<span data-ttu-id="738d3-172">3</span><span class="sxs-lookup"><span data-stu-id="738d3-172">3</span></span> |
| <span data-ttu-id="738d3-173">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-173">Default value</span></span> |<span data-ttu-id="738d3-174">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-174">none</span></span> |
| <span data-ttu-id="738d3-175">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-175">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-177">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="738d3-177">Parameter set name</span></span> |<span data-ttu-id="738d3-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="738d3-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="738d3-179">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-179">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-180">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-180">false</span></span> |

<span data-ttu-id="738d3-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="738d3-182">Задает учетные записи хранения, связанный с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="738d3-183">Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.</span><span class="sxs-lookup"><span data-stu-id="738d3-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="738d3-184">Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="738d3-185">Можно указать только одну основную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="738d3-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="738d3-186">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-186">Aliases</span></span> | <span data-ttu-id="738d3-187">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-188">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-188">Required?</span></span> |<span data-ttu-id="738d3-189">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-189">true</span></span> |
| <span data-ttu-id="738d3-190">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-190">Position?</span></span> |<span data-ttu-id="738d3-191">3</span><span class="sxs-lookup"><span data-stu-id="738d3-191">3</span></span> |
| <span data-ttu-id="738d3-192">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-192">Default value</span></span> |<span data-ttu-id="738d3-193">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-193">none</span></span> |
| <span data-ttu-id="738d3-194">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-194">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-196">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="738d3-196">Parameter set name</span></span> |<span data-ttu-id="738d3-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="738d3-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="738d3-198">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-198">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-199">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-199">false</span></span> |

<span data-ttu-id="738d3-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="738d3-201">Указывает хэш-таблицу hello теги, связанные с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="738d3-202">Пример: @{«tag1 «=» значение1»;» tag2» =: значение2»}</span><span class="sxs-lookup"><span data-stu-id="738d3-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="738d3-203">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-203">Aliases</span></span> | <span data-ttu-id="738d3-204">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-205">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-205">Required?</span></span> |<span data-ttu-id="738d3-206">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-206">false</span></span> |
| <span data-ttu-id="738d3-207">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-207">Position?</span></span> |<span data-ttu-id="738d3-208">именованная</span><span class="sxs-lookup"><span data-stu-id="738d3-208">named</span></span> |
| <span data-ttu-id="738d3-209">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-209">Default value</span></span> |<span data-ttu-id="738d3-210">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-210">none</span></span> |
| <span data-ttu-id="738d3-211">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-211">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-212">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-212">false</span></span> |
| <span data-ttu-id="738d3-213">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-213">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-214">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-214">false</span></span> |

<span data-ttu-id="738d3-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-216">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-217">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-217">Inputs</span></span>
<span data-ttu-id="738d3-218">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-219">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-219">Outputs</span></span>
<span data-ttu-id="738d3-220">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="738d3-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="738d3-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="738d3-222">Обновляет службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-223">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-224">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-224">Parameters</span></span>
<span data-ttu-id="738d3-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-226">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-227">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-227">Aliases</span></span> | <span data-ttu-id="738d3-228">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-229">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-229">Required?</span></span> |<span data-ttu-id="738d3-230">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-230">true</span></span> |
| <span data-ttu-id="738d3-231">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-231">Position?</span></span> |<span data-ttu-id="738d3-232">0</span><span class="sxs-lookup"><span data-stu-id="738d3-232">0</span></span> |
| <span data-ttu-id="738d3-233">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-233">Default Value</span></span> |<span data-ttu-id="738d3-234">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-234">none</span></span> |
| <span data-ttu-id="738d3-235">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="738d3-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-237">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-237">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-238">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-238">false</span></span> |

<span data-ttu-id="738d3-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-240">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-241">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-241">Aliases</span></span> | <span data-ttu-id="738d3-242">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="738d3-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-243">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-243">Required?</span></span> |<span data-ttu-id="738d3-244">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-244">True</span></span> |
| <span data-ttu-id="738d3-245">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-245">Position?</span></span> |<span data-ttu-id="738d3-246">1</span><span class="sxs-lookup"><span data-stu-id="738d3-246">1</span></span> |
| <span data-ttu-id="738d3-247">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-247">Default value</span></span> |<span data-ttu-id="738d3-248">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-248">None</span></span> |
| <span data-ttu-id="738d3-249">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-249">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-251">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-251">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-252">Ложь</span><span class="sxs-lookup"><span data-stu-id="738d3-252">False</span></span> |

<span data-ttu-id="738d3-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="738d3-254">Задает учетные записи хранения, связанный с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="738d3-255">Новая учетная запись хранилища (созданная с параметром hello API диспетчера ресурсов) поддерживается только.</span><span class="sxs-lookup"><span data-stu-id="738d3-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="738d3-256">Hello учетная запись хранения должна существовать и имеет hello того же расположения, службы мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="738d3-257">Можно указать только одну основную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="738d3-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="738d3-258">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-258">Aliases</span></span> | <span data-ttu-id="738d3-259">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-260">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-260">Required?</span></span> |<span data-ttu-id="738d3-261">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-261">false</span></span> |
| <span data-ttu-id="738d3-262">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-262">Position?</span></span> |<span data-ttu-id="738d3-263">именованная</span><span class="sxs-lookup"><span data-stu-id="738d3-263">Named</span></span> |
| <span data-ttu-id="738d3-264">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-264">Default value</span></span> |<span data-ttu-id="738d3-265">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-265">none</span></span> |
| <span data-ttu-id="738d3-266">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-266">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-268">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="738d3-268">Parameter set name</span></span> |<span data-ttu-id="738d3-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="738d3-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="738d3-270">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-270">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-271">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-271">false</span></span> |

<span data-ttu-id="738d3-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="738d3-273">Указывает хэш-таблицу hello теги, связанные с этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="738d3-274">значение, указанное клиентом hello заменяются Hello теги, связанные с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="738d3-275">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-275">Aliases</span></span> | <span data-ttu-id="738d3-276">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-277">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-277">Required?</span></span> |<span data-ttu-id="738d3-278">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-278">False</span></span> |
| <span data-ttu-id="738d3-279">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-279">Position?</span></span> |<span data-ttu-id="738d3-280">именованная</span><span class="sxs-lookup"><span data-stu-id="738d3-280">Named</span></span> |
| <span data-ttu-id="738d3-281">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-281">Default value</span></span> |<span data-ttu-id="738d3-282">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-282">None</span></span> |
| <span data-ttu-id="738d3-283">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-283">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-285">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-285">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-286">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-286">false</span></span> |

<span data-ttu-id="738d3-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-288">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-289">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-289">Inputs</span></span>
<span data-ttu-id="738d3-290">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-291">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-291">Outputs</span></span>
<span data-ttu-id="738d3-292">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="738d3-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="738d3-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="738d3-294">Удаляет службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-295">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-296">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-296">Parameters</span></span>
<span data-ttu-id="738d3-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-298">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-299">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-299">Aliases</span></span> | <span data-ttu-id="738d3-300">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-301">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-301">Required?</span></span> |<span data-ttu-id="738d3-302">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-302">true</span></span> |
| <span data-ttu-id="738d3-303">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-303">Position?</span></span> |<span data-ttu-id="738d3-304">0</span><span class="sxs-lookup"><span data-stu-id="738d3-304">0</span></span> |
| <span data-ttu-id="738d3-305">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-305">Default value</span></span> |<span data-ttu-id="738d3-306">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-306">none</span></span> |
| <span data-ttu-id="738d3-307">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-307">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-309">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-309">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-310">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-310">false</span></span> |

<span data-ttu-id="738d3-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-312">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-313">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-313">Aliases</span></span> | <span data-ttu-id="738d3-314">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-315">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-315">Required?</span></span> |<span data-ttu-id="738d3-316">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-316">true</span></span> |
| <span data-ttu-id="738d3-317">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-317">Position?</span></span> |<span data-ttu-id="738d3-318">2</span><span class="sxs-lookup"><span data-stu-id="738d3-318">2</span></span> |
| <span data-ttu-id="738d3-319">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-319">Default value</span></span> |<span data-ttu-id="738d3-320">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-320">None</span></span> |
| <span data-ttu-id="738d3-321">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-321">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-323">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-323">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-324">Ложь</span><span class="sxs-lookup"><span data-stu-id="738d3-324">False</span></span> |

<span data-ttu-id="738d3-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-326">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-327">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-327">Inputs</span></span>
<span data-ttu-id="738d3-328">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-329">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-329">Outputs</span></span>
<span data-ttu-id="738d3-330">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="738d3-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="738d3-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="738d3-332">Получает все службы мультимедиа в группе ресурсов или службу мультимедиа с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="738d3-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-333">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-333">Syntax</span></span>
<span data-ttu-id="738d3-334">Набор параметров: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="738d3-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="738d3-335">Набор параметров: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="738d3-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-336">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-336">Parameters</span></span>
<span data-ttu-id="738d3-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-338">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-339">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-339">Aliases</span></span> | <span data-ttu-id="738d3-340">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-341">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-341">Required?</span></span> |<span data-ttu-id="738d3-342">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-342">true</span></span> |
| <span data-ttu-id="738d3-343">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-343">Position?</span></span> |<span data-ttu-id="738d3-344">0</span><span class="sxs-lookup"><span data-stu-id="738d3-344">0</span></span> |
| <span data-ttu-id="738d3-345">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-345">Default value</span></span> |<span data-ttu-id="738d3-346">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-346">none</span></span> |
| <span data-ttu-id="738d3-347">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-347">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-349">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="738d3-349">Parameter set name</span></span> |<span data-ttu-id="738d3-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="738d3-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="738d3-351">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-351">Accept wildcard characters?</span></span>   <span data-ttu-id="738d3-352">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-352">false</span></span>

<span data-ttu-id="738d3-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-354">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-355">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-355">Aliases</span></span> | <span data-ttu-id="738d3-356">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-357">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-357">Required?</span></span> |<span data-ttu-id="738d3-358">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-358">true</span></span> |
| <span data-ttu-id="738d3-359">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-359">Position?</span></span> |<span data-ttu-id="738d3-360">1</span><span class="sxs-lookup"><span data-stu-id="738d3-360">1</span></span> |
| <span data-ttu-id="738d3-361">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-361">Default value</span></span> |<span data-ttu-id="738d3-362">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-362">none</span></span> |
| <span data-ttu-id="738d3-363">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-363">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-365">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="738d3-365">Parameter set name</span></span> |<span data-ttu-id="738d3-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="738d3-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="738d3-367">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-367">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-368">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-368">false</span></span> |

<span data-ttu-id="738d3-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-370">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-371">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-371">Inputs</span></span>
<span data-ttu-id="738d3-372">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-373">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-373">Outputs</span></span>
<span data-ttu-id="738d3-374">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="738d3-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="738d3-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="738d3-376">Возвращает ключи службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-377">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-378">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-378">Parameters</span></span>
<span data-ttu-id="738d3-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-380">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-381">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-381">Aliases</span></span> | <span data-ttu-id="738d3-382">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-383">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-383">Required?</span></span> |<span data-ttu-id="738d3-384">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-384">true</span></span> |
| <span data-ttu-id="738d3-385">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-385">Position?</span></span> |<span data-ttu-id="738d3-386">0</span><span class="sxs-lookup"><span data-stu-id="738d3-386">0</span></span> |
| <span data-ttu-id="738d3-387">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-387">Default value</span></span> |<span data-ttu-id="738d3-388">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-388">none</span></span> |
| <span data-ttu-id="738d3-389">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-389">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-391">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-391">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-392">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-392">false</span></span> |

<span data-ttu-id="738d3-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-394">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-395">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-395">Aliases</span></span> | <span data-ttu-id="738d3-396">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-397">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-397">Required?</span></span> |<span data-ttu-id="738d3-398">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-398">true</span></span> |
| <span data-ttu-id="738d3-399">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-399">Position?</span></span> |<span data-ttu-id="738d3-400">1</span><span class="sxs-lookup"><span data-stu-id="738d3-400">1</span></span> |
| <span data-ttu-id="738d3-401">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-401">Default value</span></span> |<span data-ttu-id="738d3-402">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-402">none</span></span> |
| <span data-ttu-id="738d3-403">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-403">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-405">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-405">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-406">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-406">false</span></span> |

<span data-ttu-id="738d3-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-408">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-409">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-409">Inputs</span></span>
<span data-ttu-id="738d3-410">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-411">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-411">Outputs</span></span>
<span data-ttu-id="738d3-412">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="738d3-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="738d3-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="738d3-414">Повторно создает первичный или вторичный ключ службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-415">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-416">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-416">Parameters</span></span>
<span data-ttu-id="738d3-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-418">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-419">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-419">Aliases</span></span> | <span data-ttu-id="738d3-420">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-421">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-421">Required?</span></span> |<span data-ttu-id="738d3-422">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-422">true</span></span> |
| <span data-ttu-id="738d3-423">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-423">Position?</span></span> |<span data-ttu-id="738d3-424">0</span><span class="sxs-lookup"><span data-stu-id="738d3-424">0</span></span> |
| <span data-ttu-id="738d3-425">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-425">Default value</span></span> |<span data-ttu-id="738d3-426">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-426">none</span></span> |
| <span data-ttu-id="738d3-427">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-427">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-429">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-429">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-430">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-430">false</span></span> |

<span data-ttu-id="738d3-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-432">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-433">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-433">Aliases</span></span> | <span data-ttu-id="738d3-434">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-435">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-435">Required?</span></span> |<span data-ttu-id="738d3-436">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-436">true</span></span> |
| <span data-ttu-id="738d3-437">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-437">Position?</span></span> |<span data-ttu-id="738d3-438">1</span><span class="sxs-lookup"><span data-stu-id="738d3-438">1</span></span> |
| <span data-ttu-id="738d3-439">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-439">Default value</span></span> |<span data-ttu-id="738d3-440">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-440">none</span></span> |
| <span data-ttu-id="738d3-441">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-441">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-443">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-443">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-444">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-444">false</span></span> |

<span data-ttu-id="738d3-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="738d3-446">Задает тип ключа hello hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="738d3-447">Первичный или вторичный</span><span class="sxs-lookup"><span data-stu-id="738d3-447">Primary or Secondary</span></span>

| <span data-ttu-id="738d3-448">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-448">Aliases</span></span> | <span data-ttu-id="738d3-449">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-450">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-450">Required?</span></span> |<span data-ttu-id="738d3-451">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-451">true</span></span> |
| <span data-ttu-id="738d3-452">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-452">Position?</span></span> |<span data-ttu-id="738d3-453">2</span><span class="sxs-lookup"><span data-stu-id="738d3-453">2</span></span> |
| <span data-ttu-id="738d3-454">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-454">Default value</span></span> |<span data-ttu-id="738d3-455">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-455">none</span></span> |
| <span data-ttu-id="738d3-456">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-456">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-457">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-457">false</span></span> |
| <span data-ttu-id="738d3-458">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-458">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-459">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-459">false</span></span> |

<span data-ttu-id="738d3-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-461">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-462">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-462">Inputs</span></span>
<span data-ttu-id="738d3-463">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toothe.</span><span class="sxs-lookup"><span data-stu-id="738d3-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-464">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-464">Outputs</span></span>
<span data-ttu-id="738d3-465">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="738d3-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="738d3-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="738d3-467">Синхронизация ключей учетной записи хранения для учетной записи хранения, связанный с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="738d3-468">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="738d3-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="738d3-469">Параметры</span><span class="sxs-lookup"><span data-stu-id="738d3-469">Parameters</span></span>
<span data-ttu-id="738d3-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-471">Указывает имя hello toowhich группы ресурсов hello, к которому относится эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="738d3-472">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-472">Aliases</span></span> | <span data-ttu-id="738d3-473">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-474">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-474">Required?</span></span> |<span data-ttu-id="738d3-475">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-475">true</span></span> |
| <span data-ttu-id="738d3-476">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-476">Position?</span></span> |<span data-ttu-id="738d3-477">0</span><span class="sxs-lookup"><span data-stu-id="738d3-477">0</span></span> |
| <span data-ttu-id="738d3-478">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-478">Default value</span></span> |<span data-ttu-id="738d3-479">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-479">none</span></span> |
| <span data-ttu-id="738d3-480">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-480">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-482">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-482">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-483">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-483">false</span></span> |

<span data-ttu-id="738d3-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-485">Указывает имя службы мультимедиа hello hello.</span><span class="sxs-lookup"><span data-stu-id="738d3-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="738d3-486">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-486">Aliases</span></span> | <span data-ttu-id="738d3-487">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-488">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-488">Required?</span></span> |<span data-ttu-id="738d3-489">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-489">true</span></span> |
| <span data-ttu-id="738d3-490">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-490">Position?</span></span> |<span data-ttu-id="738d3-491">1</span><span class="sxs-lookup"><span data-stu-id="738d3-491">1</span></span> |
| <span data-ttu-id="738d3-492">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-492">Default value</span></span> |<span data-ttu-id="738d3-493">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-493">none</span></span> |
| <span data-ttu-id="738d3-494">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-494">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-496">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-496">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-497">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-497">false</span></span> |

<span data-ttu-id="738d3-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="738d3-499">Указывает учетную запись хранилища hello, связанные с hello службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="738d3-500">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="738d3-500">Aliases</span></span> | <span data-ttu-id="738d3-501">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="738d3-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="738d3-502">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="738d3-502">Required?</span></span> |<span data-ttu-id="738d3-503">Да</span><span class="sxs-lookup"><span data-stu-id="738d3-503">true</span></span> |
| <span data-ttu-id="738d3-504">Позиция?</span><span class="sxs-lookup"><span data-stu-id="738d3-504">Position?</span></span> |<span data-ttu-id="738d3-505">2</span><span class="sxs-lookup"><span data-stu-id="738d3-505">2</span></span> |
| <span data-ttu-id="738d3-506">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="738d3-506">Default value</span></span> |<span data-ttu-id="738d3-507">Нет</span><span class="sxs-lookup"><span data-stu-id="738d3-507">none</span></span> |
| <span data-ttu-id="738d3-508">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="738d3-508">Accept pipeline input?</span></span> |<span data-ttu-id="738d3-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="738d3-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="738d3-510">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="738d3-510">Accept wildcard characters?</span></span> |<span data-ttu-id="738d3-511">нет</span><span class="sxs-lookup"><span data-stu-id="738d3-511">false</span></span> |

<span data-ttu-id="738d3-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="738d3-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="738d3-513">Этот командлет поддерживает общие параметры hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction и - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="738d3-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="738d3-514">Входные данные</span><span class="sxs-lookup"><span data-stu-id="738d3-514">Inputs</span></span>
<span data-ttu-id="738d3-515">Hello входным типом является тип hello hello объекты, можно передать по конвейеру командлету toohello.</span><span class="sxs-lookup"><span data-stu-id="738d3-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="738d3-516">outputs</span><span class="sxs-lookup"><span data-stu-id="738d3-516">Outputs</span></span>
<span data-ttu-id="738d3-517">Тип выходных данных Hello — выдает hello типы объектов hello hello командлета.</span><span class="sxs-lookup"><span data-stu-id="738d3-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="738d3-518">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="738d3-518">Next step</span></span>
<span data-ttu-id="738d3-519">Изучите схемы обучения для служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="738d3-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="738d3-520">Отзывы</span><span class="sxs-lookup"><span data-stu-id="738d3-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

