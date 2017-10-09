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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Использование PowerShell toocreate toouse приложения Azure AD с hello API служб мультимедиа Azure

Узнайте, как toouse PowerShell скрипт toocreate приложения Azure Active Directory (Azure AD) и службы основной tooaccess ресурсы служб мультимедиа Azure.  

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/). 
- Учетная запись служб мультимедиа. Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure в hello портал Azure](media-services-portal-create-account.md).
- Azure PowerShell (версии 0.8.8 или более поздней). Дополнительные сведения см. в разделе [как toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Командлеты Azure Resource Manager.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Создание приложения Azure AD с помощью PowerShell  

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

Дополнительные сведения см. в разделе hello в следующих статьях:

- [Использование Azure PowerShell toocreate ресурсов tooaccess участника службы](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Управление доступом на основе ролей с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Как toomanually настроить управляющую программу приложений с помощью сертификатов](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Дальнейшие действия

Приступая к работе с [передача файлов учетная запись tooyour](media-services-portal-upload-files.md).
