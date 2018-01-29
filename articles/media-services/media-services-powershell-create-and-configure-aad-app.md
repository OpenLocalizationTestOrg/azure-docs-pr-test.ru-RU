---
title: "Создание приложения Azure AD для доступа к API служб мультимедиа Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как использовать PowerShell, чтобы создать приложение Azure Active Directory (Azure AD) и настроить его для доступа к API служб мультимедиа Azure."
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
ms.openlocfilehash: eea0f3a03dd77ce56484f32b192299bd97c05300
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a>Создание приложения Azure AD для работы с API служб мультимедиа Azure с помощью PowerShell

Узнайте, как с помощью сценария PowerShell создать приложение Azure Active Directory (Azure AD) и участник-службу для доступа к ресурсам служб мультимедиа Azure.  

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/). 
- Учетная запись служб мультимедиа. Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).
- Azure PowerShell (версии 0.8.8 или более поздней). Дополнительные сведения см. в разделе [об использовании Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
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
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Дополнительные сведения см. в следующих статьях:

- [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Управление доступом на основе ролей с помощью Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad) (Ручная настройка аутентификации приложений управляющей программы в Azure AD с помощью сертификатов)

## <a name="next-steps"></a>Дальнейшие действия

Приступите к [передаче файлов в учетную запись](media-services-portal-upload-files.md).
