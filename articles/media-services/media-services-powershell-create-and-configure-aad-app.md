---
title: "Здравствуйте, toocreate PowerShell aaaUse tooaccess приложения Azure AD API служб мультимедиа Azure | Документы Microsoft"
description: "Узнайте, как toocreate PowerShell toouse приложения Azure Active Directory (Azure AD) и настройте hello tooaccess API служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="78c1a-103">Использование PowerShell toocreate toouse приложения Azure AD с hello API служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="78c1a-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="78c1a-104">Узнайте, как toouse PowerShell скрипт toocreate приложения Azure Active Directory (Azure AD) и службы основной tooaccess ресурсы служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="78c1a-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="78c1a-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="78c1a-105">Prerequisites</span></span>

- <span data-ttu-id="78c1a-106">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="78c1a-106">An Azure account.</span></span> <span data-ttu-id="78c1a-107">Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78c1a-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="78c1a-108">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="78c1a-108">A Media Services account.</span></span> <span data-ttu-id="78c1a-109">Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure в hello портал Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="78c1a-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="78c1a-110">Azure PowerShell (версии 0.8.8 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="78c1a-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="78c1a-111">Дополнительные сведения см. в разделе [как toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78c1a-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="78c1a-112">Командлеты Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="78c1a-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="78c1a-113">Создание приложения Azure AD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="78c1a-113">Create an Azure AD app by using PowerShell</span></span>  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

<span data-ttu-id="78c1a-114">Дополнительные сведения см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="78c1a-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="78c1a-115">Использование Azure PowerShell toocreate ресурсов tooaccess участника службы</span><span class="sxs-lookup"><span data-stu-id="78c1a-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="78c1a-116">Управление доступом на основе ролей с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78c1a-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="78c1a-117">Как toomanually настроить управляющую программу приложений с помощью сертификатов</span><span class="sxs-lookup"><span data-stu-id="78c1a-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="78c1a-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78c1a-118">Next steps</span></span>

<span data-ttu-id="78c1a-119">Приступая к работе с [передача файлов учетная запись tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="78c1a-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
