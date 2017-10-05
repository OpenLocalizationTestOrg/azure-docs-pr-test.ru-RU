---
title: "Управление учетными записями служб мультимедиа Azure с помощью PowerShell"
description: "Узнайте, как управлять учетными записями служб мультимедиа Azure с помощью командлетов PowerShell."
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
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="5c0b5-103">Управление учетными записями служб мультимедиа Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c0b5-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c0b5-104">Портал</span><span class="sxs-lookup"><span data-stu-id="5c0b5-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="5c0b5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c0b5-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="5c0b5-106">REST</span><span class="sxs-lookup"><span data-stu-id="5c0b5-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="5c0b5-107">Для создания учетной записи служб мультимедиа Azure необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="5c0b5-108">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5c0b5-109">Дополнительные сведения см. в разделе <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="5c0b5-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="5c0b5-110">Overview</span></span>
<span data-ttu-id="5c0b5-111">В этой статье перечислены командлеты Azure PowerShell для служб мультимедиа Azure (AMS), доступные в инфраструктуре Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="5c0b5-112">Командлеты существуют в пространстве имен **Microsoft.Azure.Commands.Media** .</span><span class="sxs-lookup"><span data-stu-id="5c0b5-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="5c0b5-113">Версии</span><span class="sxs-lookup"><span data-stu-id="5c0b5-113">Versions</span></span>
<span data-ttu-id="5c0b5-114">**ApiVersion**: от 01.10.2015.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="5c0b5-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5c0b5-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="5c0b5-116">Создает службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-117">Syntax</span></span>
<span data-ttu-id="5c0b5-118">Набор параметров: StorageAccountIdParamSet.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="5c0b5-119">Набор параметров: StorageAccountsParamSet.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-120">Parameters</span></span>
<span data-ttu-id="5c0b5-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-122">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-123">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-123">Aliases</span></span> | <span data-ttu-id="5c0b5-124">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-125">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-125">Required?</span></span> |<span data-ttu-id="5c0b5-126">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-126">true</span></span> |
| <span data-ttu-id="5c0b5-127">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-127">Position?</span></span> |<span data-ttu-id="5c0b5-128">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-128">0</span></span> |
| <span data-ttu-id="5c0b5-129">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-129">Default value</span></span> |<span data-ttu-id="5c0b5-130">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-130">none</span></span> |
| <span data-ttu-id="5c0b5-131">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-131">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-133">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-133">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-134">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-134">false</span></span> |

<span data-ttu-id="5c0b5-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-136">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-137">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-137">Aliases</span></span> | <span data-ttu-id="5c0b5-138">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-139">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-139">Required?</span></span> |<span data-ttu-id="5c0b5-140">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-140">true</span></span> |
| <span data-ttu-id="5c0b5-141">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-141">Position?</span></span> |<span data-ttu-id="5c0b5-142">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-142">1</span></span> |
| <span data-ttu-id="5c0b5-143">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-143">Default value</span></span> |<span data-ttu-id="5c0b5-144">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-144">none</span></span> |
| <span data-ttu-id="5c0b5-145">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-145">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-146">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-146">false</span></span> |
| <span data-ttu-id="5c0b5-147">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-147">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-148">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-148">false</span></span> |

<span data-ttu-id="5c0b5-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-150">Указывает расположение ресурсов для этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="5c0b5-151">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-151">Aliases</span></span> | <span data-ttu-id="5c0b5-152">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-153">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-153">Required?</span></span> |<span data-ttu-id="5c0b5-154">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-154">true</span></span> |
| <span data-ttu-id="5c0b5-155">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-155">Position?</span></span> |<span data-ttu-id="5c0b5-156">2</span><span class="sxs-lookup"><span data-stu-id="5c0b5-156">2</span></span> |
| <span data-ttu-id="5c0b5-157">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-157">Default value</span></span> |<span data-ttu-id="5c0b5-158">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-158">none</span></span> |
| <span data-ttu-id="5c0b5-159">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-159">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-161">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-161">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-162">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-162">false</span></span> |

<span data-ttu-id="5c0b5-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-164">Указывает основную учетную запись хранения, связанную с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="5c0b5-165">Поддерживаются только новые учетные записи хранения (созданные с помощью API Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5c0b5-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5c0b5-166">Учетная запись хранения должна существовать и находиться в том же расположении, что и служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="5c0b5-167">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-167">Aliases</span></span> | <span data-ttu-id="5c0b5-168">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-169">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-169">Required?</span></span> |<span data-ttu-id="5c0b5-170">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-170">true</span></span> |
| <span data-ttu-id="5c0b5-171">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-171">Position?</span></span> |<span data-ttu-id="5c0b5-172">3</span><span class="sxs-lookup"><span data-stu-id="5c0b5-172">3</span></span> |
| <span data-ttu-id="5c0b5-173">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-173">Default value</span></span> |<span data-ttu-id="5c0b5-174">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-174">none</span></span> |
| <span data-ttu-id="5c0b5-175">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-175">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-177">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="5c0b5-177">Parameter set name</span></span> |<span data-ttu-id="5c0b5-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="5c0b5-179">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-179">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-180">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-180">false</span></span> |

<span data-ttu-id="5c0b5-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="5c0b5-182">Указывает учетные записи хранения, связанные с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="5c0b5-183">Поддерживаются только новые учетные записи хранения (созданные с помощью API Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5c0b5-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5c0b5-184">Учетная запись хранения должна существовать и находиться в том же расположении, что и служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="5c0b5-185">Можно указать только одну основную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="5c0b5-186">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-186">Aliases</span></span> | <span data-ttu-id="5c0b5-187">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-188">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-188">Required?</span></span> |<span data-ttu-id="5c0b5-189">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-189">true</span></span> |
| <span data-ttu-id="5c0b5-190">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-190">Position?</span></span> |<span data-ttu-id="5c0b5-191">3</span><span class="sxs-lookup"><span data-stu-id="5c0b5-191">3</span></span> |
| <span data-ttu-id="5c0b5-192">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-192">Default value</span></span> |<span data-ttu-id="5c0b5-193">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-193">none</span></span> |
| <span data-ttu-id="5c0b5-194">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-194">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-196">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="5c0b5-196">Parameter set name</span></span> |<span data-ttu-id="5c0b5-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="5c0b5-198">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-198">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-199">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-199">false</span></span> |

<span data-ttu-id="5c0b5-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="5c0b5-201">Указывает хэш-таблицу тегов, которые связаны с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="5c0b5-202">Пример: @{«tag1 «=» значение1»;» tag2» =: значение2»}</span><span class="sxs-lookup"><span data-stu-id="5c0b5-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="5c0b5-203">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-203">Aliases</span></span> | <span data-ttu-id="5c0b5-204">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-205">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-205">Required?</span></span> |<span data-ttu-id="5c0b5-206">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-206">false</span></span> |
| <span data-ttu-id="5c0b5-207">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-207">Position?</span></span> |<span data-ttu-id="5c0b5-208">именованная</span><span class="sxs-lookup"><span data-stu-id="5c0b5-208">named</span></span> |
| <span data-ttu-id="5c0b5-209">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-209">Default value</span></span> |<span data-ttu-id="5c0b5-210">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-210">none</span></span> |
| <span data-ttu-id="5c0b5-211">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-211">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-212">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-212">false</span></span> |
| <span data-ttu-id="5c0b5-213">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-213">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-214">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-214">false</span></span> |

<span data-ttu-id="5c0b5-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-216">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-217">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-217">Inputs</span></span>
<span data-ttu-id="5c0b5-218">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-219">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-219">Outputs</span></span>
<span data-ttu-id="5c0b5-220">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="5c0b5-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5c0b5-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="5c0b5-222">Обновляет службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-223">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-224">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-224">Parameters</span></span>
<span data-ttu-id="5c0b5-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-226">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-227">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-227">Aliases</span></span> | <span data-ttu-id="5c0b5-228">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-229">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-229">Required?</span></span> |<span data-ttu-id="5c0b5-230">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-230">true</span></span> |
| <span data-ttu-id="5c0b5-231">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-231">Position?</span></span> |<span data-ttu-id="5c0b5-232">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-232">0</span></span> |
| <span data-ttu-id="5c0b5-233">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-233">Default Value</span></span> |<span data-ttu-id="5c0b5-234">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-234">none</span></span> |
| <span data-ttu-id="5c0b5-235">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="5c0b5-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-237">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-237">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-238">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-238">false</span></span> |

<span data-ttu-id="5c0b5-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-240">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-241">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-241">Aliases</span></span> | <span data-ttu-id="5c0b5-242">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-243">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-243">Required?</span></span> |<span data-ttu-id="5c0b5-244">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-244">True</span></span> |
| <span data-ttu-id="5c0b5-245">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-245">Position?</span></span> |<span data-ttu-id="5c0b5-246">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-246">1</span></span> |
| <span data-ttu-id="5c0b5-247">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-247">Default value</span></span> |<span data-ttu-id="5c0b5-248">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-248">None</span></span> |
| <span data-ttu-id="5c0b5-249">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-249">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-251">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-251">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-252">Ложь</span><span class="sxs-lookup"><span data-stu-id="5c0b5-252">False</span></span> |

<span data-ttu-id="5c0b5-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="5c0b5-254">Указывает учетные записи хранения, связанные с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="5c0b5-255">Поддерживаются только новые учетные записи хранения (созданные с помощью API Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="5c0b5-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="5c0b5-256">Учетная запись хранения должна существовать и находиться в том же расположении, что и служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="5c0b5-257">Можно указать только одну основную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="5c0b5-258">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-258">Aliases</span></span> | <span data-ttu-id="5c0b5-259">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-260">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-260">Required?</span></span> |<span data-ttu-id="5c0b5-261">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-261">false</span></span> |
| <span data-ttu-id="5c0b5-262">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-262">Position?</span></span> |<span data-ttu-id="5c0b5-263">именованная</span><span class="sxs-lookup"><span data-stu-id="5c0b5-263">Named</span></span> |
| <span data-ttu-id="5c0b5-264">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-264">Default value</span></span> |<span data-ttu-id="5c0b5-265">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-265">none</span></span> |
| <span data-ttu-id="5c0b5-266">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-266">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-268">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="5c0b5-268">Parameter set name</span></span> |<span data-ttu-id="5c0b5-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="5c0b5-270">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-270">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-271">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-271">false</span></span> |

<span data-ttu-id="5c0b5-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="5c0b5-273">Указывает хэш-таблицу тегов, которые связаны с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="5c0b5-274">Теги, которые связаны со службой мультимедиа, заменяются значением, указанным пользователем.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="5c0b5-275">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-275">Aliases</span></span> | <span data-ttu-id="5c0b5-276">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-277">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-277">Required?</span></span> |<span data-ttu-id="5c0b5-278">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-278">False</span></span> |
| <span data-ttu-id="5c0b5-279">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-279">Position?</span></span> |<span data-ttu-id="5c0b5-280">именованная</span><span class="sxs-lookup"><span data-stu-id="5c0b5-280">Named</span></span> |
| <span data-ttu-id="5c0b5-281">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-281">Default value</span></span> |<span data-ttu-id="5c0b5-282">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-282">None</span></span> |
| <span data-ttu-id="5c0b5-283">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-283">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-285">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-285">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-286">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-286">false</span></span> |

<span data-ttu-id="5c0b5-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-288">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-289">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-289">Inputs</span></span>
<span data-ttu-id="5c0b5-290">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-291">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-291">Outputs</span></span>
<span data-ttu-id="5c0b5-292">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="5c0b5-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5c0b5-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="5c0b5-294">Удаляет службу мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-295">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-296">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-296">Parameters</span></span>
<span data-ttu-id="5c0b5-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-298">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-299">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-299">Aliases</span></span> | <span data-ttu-id="5c0b5-300">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-301">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-301">Required?</span></span> |<span data-ttu-id="5c0b5-302">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-302">true</span></span> |
| <span data-ttu-id="5c0b5-303">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-303">Position?</span></span> |<span data-ttu-id="5c0b5-304">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-304">0</span></span> |
| <span data-ttu-id="5c0b5-305">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-305">Default value</span></span> |<span data-ttu-id="5c0b5-306">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-306">none</span></span> |
| <span data-ttu-id="5c0b5-307">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-307">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-309">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-309">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-310">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-310">false</span></span> |

<span data-ttu-id="5c0b5-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-312">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-313">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-313">Aliases</span></span> | <span data-ttu-id="5c0b5-314">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-315">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-315">Required?</span></span> |<span data-ttu-id="5c0b5-316">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-316">true</span></span> |
| <span data-ttu-id="5c0b5-317">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-317">Position?</span></span> |<span data-ttu-id="5c0b5-318">2</span><span class="sxs-lookup"><span data-stu-id="5c0b5-318">2</span></span> |
| <span data-ttu-id="5c0b5-319">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-319">Default value</span></span> |<span data-ttu-id="5c0b5-320">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-320">None</span></span> |
| <span data-ttu-id="5c0b5-321">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-321">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-323">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-323">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-324">Ложь</span><span class="sxs-lookup"><span data-stu-id="5c0b5-324">False</span></span> |

<span data-ttu-id="5c0b5-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-326">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-327">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-327">Inputs</span></span>
<span data-ttu-id="5c0b5-328">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-329">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-329">Outputs</span></span>
<span data-ttu-id="5c0b5-330">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="5c0b5-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="5c0b5-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="5c0b5-332">Получает все службы мультимедиа в группе ресурсов или службу мультимедиа с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-333">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-333">Syntax</span></span>
<span data-ttu-id="5c0b5-334">Набор параметров: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="5c0b5-335">Набор параметров: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-336">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-336">Parameters</span></span>
<span data-ttu-id="5c0b5-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-338">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-339">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-339">Aliases</span></span> | <span data-ttu-id="5c0b5-340">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-341">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-341">Required?</span></span> |<span data-ttu-id="5c0b5-342">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-342">true</span></span> |
| <span data-ttu-id="5c0b5-343">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-343">Position?</span></span> |<span data-ttu-id="5c0b5-344">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-344">0</span></span> |
| <span data-ttu-id="5c0b5-345">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-345">Default value</span></span> |<span data-ttu-id="5c0b5-346">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-346">none</span></span> |
| <span data-ttu-id="5c0b5-347">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-347">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-349">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="5c0b5-349">Parameter set name</span></span> |<span data-ttu-id="5c0b5-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="5c0b5-351">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-351">Accept wildcard characters?</span></span>   <span data-ttu-id="5c0b5-352">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-352">false</span></span>

<span data-ttu-id="5c0b5-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-354">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-355">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-355">Aliases</span></span> | <span data-ttu-id="5c0b5-356">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-357">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-357">Required?</span></span> |<span data-ttu-id="5c0b5-358">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-358">true</span></span> |
| <span data-ttu-id="5c0b5-359">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-359">Position?</span></span> |<span data-ttu-id="5c0b5-360">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-360">1</span></span> |
| <span data-ttu-id="5c0b5-361">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-361">Default value</span></span> |<span data-ttu-id="5c0b5-362">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-362">none</span></span> |
| <span data-ttu-id="5c0b5-363">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-363">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-365">Имя набора параметров</span><span class="sxs-lookup"><span data-stu-id="5c0b5-365">Parameter set name</span></span> |<span data-ttu-id="5c0b5-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="5c0b5-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="5c0b5-367">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-367">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-368">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-368">false</span></span> |

<span data-ttu-id="5c0b5-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-370">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-371">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-371">Inputs</span></span>
<span data-ttu-id="5c0b5-372">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-373">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-373">Outputs</span></span>
<span data-ttu-id="5c0b5-374">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="5c0b5-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="5c0b5-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="5c0b5-376">Возвращает ключи службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-377">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-378">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-378">Parameters</span></span>
<span data-ttu-id="5c0b5-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-380">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-381">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-381">Aliases</span></span> | <span data-ttu-id="5c0b5-382">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-383">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-383">Required?</span></span> |<span data-ttu-id="5c0b5-384">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-384">true</span></span> |
| <span data-ttu-id="5c0b5-385">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-385">Position?</span></span> |<span data-ttu-id="5c0b5-386">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-386">0</span></span> |
| <span data-ttu-id="5c0b5-387">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-387">Default value</span></span> |<span data-ttu-id="5c0b5-388">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-388">none</span></span> |
| <span data-ttu-id="5c0b5-389">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-389">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-391">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-391">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-392">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-392">false</span></span> |

<span data-ttu-id="5c0b5-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-394">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-395">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-395">Aliases</span></span> | <span data-ttu-id="5c0b5-396">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-397">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-397">Required?</span></span> |<span data-ttu-id="5c0b5-398">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-398">true</span></span> |
| <span data-ttu-id="5c0b5-399">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-399">Position?</span></span> |<span data-ttu-id="5c0b5-400">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-400">1</span></span> |
| <span data-ttu-id="5c0b5-401">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-401">Default value</span></span> |<span data-ttu-id="5c0b5-402">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-402">none</span></span> |
| <span data-ttu-id="5c0b5-403">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-403">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-405">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-405">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-406">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-406">false</span></span> |

<span data-ttu-id="5c0b5-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-408">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-409">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-409">Inputs</span></span>
<span data-ttu-id="5c0b5-410">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-411">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-411">Outputs</span></span>
<span data-ttu-id="5c0b5-412">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="5c0b5-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="5c0b5-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="5c0b5-414">Повторно создает первичный или вторичный ключ службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-415">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-416">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-416">Parameters</span></span>
<span data-ttu-id="5c0b5-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-418">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-419">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-419">Aliases</span></span> | <span data-ttu-id="5c0b5-420">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-421">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-421">Required?</span></span> |<span data-ttu-id="5c0b5-422">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-422">true</span></span> |
| <span data-ttu-id="5c0b5-423">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-423">Position?</span></span> |<span data-ttu-id="5c0b5-424">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-424">0</span></span> |
| <span data-ttu-id="5c0b5-425">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-425">Default value</span></span> |<span data-ttu-id="5c0b5-426">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-426">none</span></span> |
| <span data-ttu-id="5c0b5-427">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-427">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-429">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-429">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-430">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-430">false</span></span> |

<span data-ttu-id="5c0b5-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-432">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-433">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-433">Aliases</span></span> | <span data-ttu-id="5c0b5-434">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-435">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-435">Required?</span></span> |<span data-ttu-id="5c0b5-436">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-436">true</span></span> |
| <span data-ttu-id="5c0b5-437">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-437">Position?</span></span> |<span data-ttu-id="5c0b5-438">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-438">1</span></span> |
| <span data-ttu-id="5c0b5-439">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-439">Default value</span></span> |<span data-ttu-id="5c0b5-440">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-440">none</span></span> |
| <span data-ttu-id="5c0b5-441">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-441">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-443">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-443">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-444">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-444">false</span></span> |

<span data-ttu-id="5c0b5-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="5c0b5-446">Указывает тип ключа этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="5c0b5-447">Первичный или вторичный</span><span class="sxs-lookup"><span data-stu-id="5c0b5-447">Primary or Secondary</span></span>

| <span data-ttu-id="5c0b5-448">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-448">Aliases</span></span> | <span data-ttu-id="5c0b5-449">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-450">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-450">Required?</span></span> |<span data-ttu-id="5c0b5-451">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-451">true</span></span> |
| <span data-ttu-id="5c0b5-452">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-452">Position?</span></span> |<span data-ttu-id="5c0b5-453">2</span><span class="sxs-lookup"><span data-stu-id="5c0b5-453">2</span></span> |
| <span data-ttu-id="5c0b5-454">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-454">Default value</span></span> |<span data-ttu-id="5c0b5-455">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-455">none</span></span> |
| <span data-ttu-id="5c0b5-456">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-456">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-457">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-457">false</span></span> |
| <span data-ttu-id="5c0b5-458">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-458">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-459">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-459">false</span></span> |

<span data-ttu-id="5c0b5-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-461">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-462">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-462">Inputs</span></span>
<span data-ttu-id="5c0b5-463">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-464">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-464">Outputs</span></span>
<span data-ttu-id="5c0b5-465">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="5c0b5-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="5c0b5-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="5c0b5-467">Синхронизирует ключи учетной записи хранения, которая связана с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="5c0b5-468">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5c0b5-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="5c0b5-469">Параметры</span><span class="sxs-lookup"><span data-stu-id="5c0b5-469">Parameters</span></span>
<span data-ttu-id="5c0b5-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-471">Указывает имя группы ресурсов, к которой принадлежит эта служба мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="5c0b5-472">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-472">Aliases</span></span> | <span data-ttu-id="5c0b5-473">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-474">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-474">Required?</span></span> |<span data-ttu-id="5c0b5-475">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-475">true</span></span> |
| <span data-ttu-id="5c0b5-476">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-476">Position?</span></span> |<span data-ttu-id="5c0b5-477">0</span><span class="sxs-lookup"><span data-stu-id="5c0b5-477">0</span></span> |
| <span data-ttu-id="5c0b5-478">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-478">Default value</span></span> |<span data-ttu-id="5c0b5-479">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-479">none</span></span> |
| <span data-ttu-id="5c0b5-480">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-480">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-482">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-482">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-483">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-483">false</span></span> |

<span data-ttu-id="5c0b5-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-485">Указывает имя этой службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="5c0b5-486">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-486">Aliases</span></span> | <span data-ttu-id="5c0b5-487">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-488">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-488">Required?</span></span> |<span data-ttu-id="5c0b5-489">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-489">true</span></span> |
| <span data-ttu-id="5c0b5-490">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-490">Position?</span></span> |<span data-ttu-id="5c0b5-491">1</span><span class="sxs-lookup"><span data-stu-id="5c0b5-491">1</span></span> |
| <span data-ttu-id="5c0b5-492">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-492">Default value</span></span> |<span data-ttu-id="5c0b5-493">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-493">none</span></span> |
| <span data-ttu-id="5c0b5-494">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-494">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-496">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-496">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-497">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-497">false</span></span> |

<span data-ttu-id="5c0b5-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="5c0b5-499">Указывает учетную запись хранения, связанную с этой службой мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="5c0b5-500">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-500">Aliases</span></span> | <span data-ttu-id="5c0b5-501">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="5c0b5-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="5c0b5-502">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-502">Required?</span></span> |<span data-ttu-id="5c0b5-503">Да</span><span class="sxs-lookup"><span data-stu-id="5c0b5-503">true</span></span> |
| <span data-ttu-id="5c0b5-504">Позиция?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-504">Position?</span></span> |<span data-ttu-id="5c0b5-505">2</span><span class="sxs-lookup"><span data-stu-id="5c0b5-505">2</span></span> |
| <span data-ttu-id="5c0b5-506">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="5c0b5-506">Default value</span></span> |<span data-ttu-id="5c0b5-507">Нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-507">none</span></span> |
| <span data-ttu-id="5c0b5-508">Принимает входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-508">Accept pipeline input?</span></span> |<span data-ttu-id="5c0b5-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5c0b5-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="5c0b5-510">Принимает подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="5c0b5-510">Accept wildcard characters?</span></span> |<span data-ttu-id="5c0b5-511">нет</span><span class="sxs-lookup"><span data-stu-id="5c0b5-511">false</span></span> |

<span data-ttu-id="5c0b5-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="5c0b5-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="5c0b5-513">Этот командлет поддерживает общие параметры: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction и -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="5c0b5-514">Входные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-514">Inputs</span></span>
<span data-ttu-id="5c0b5-515">Тип входных данных определяет тип объектов, которые можно передавать в командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="5c0b5-516">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="5c0b5-516">Outputs</span></span>
<span data-ttu-id="5c0b5-517">Тип выходных данных определяет тип объектов, которые будет выдавать командлет.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="5c0b5-518">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c0b5-518">Next step</span></span>
<span data-ttu-id="5c0b5-519">Изучите схемы обучения для служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5c0b5-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c0b5-520">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5c0b5-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

