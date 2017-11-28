---
title: "Предоставление разрешения на доступ к хранилищу ключей Azure нескольким приложениям | Документация Майкрософт"
description: "Узнайте, как нескольким приложениям предоставить разрешение на доступ к хранилищу ключей"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="efd5d-103">Предоставление разрешения на доступ к хранилищу ключей нескольким приложениям</span><span class="sxs-lookup"><span data-stu-id="efd5d-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="efd5d-104">В. У меня много приложений (свыше 16), которым требуется доступ к хранилищу ключей.</span><span class="sxs-lookup"><span data-stu-id="efd5d-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="efd5d-105">Так как хранилище ключей разрешает доступ только 16 приложениям, как получить доступ остальным приложениям?</span><span class="sxs-lookup"><span data-stu-id="efd5d-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="efd5d-106">Политика контроля доступа хранилища ключей поддерживает не более 16 приложений.</span><span class="sxs-lookup"><span data-stu-id="efd5d-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="efd5d-107">Однако вы можете создать группу безопасности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efd5d-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="efd5d-108">Добавьте все связанные субъекты-службы в эту группу безопасности, а затем предоставьте доступ данной группе безопасности к хранилищу ключей.</span><span class="sxs-lookup"><span data-stu-id="efd5d-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="efd5d-109">Необходимые компоненты для установки:</span><span class="sxs-lookup"><span data-stu-id="efd5d-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="efd5d-110">[Установка модуля PowerShell V2 для Azure Active Directory](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="efd5d-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="efd5d-111">[Установка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efd5d-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="efd5d-112">Чтобы выполнить следующие команды, необходимо получить разрешение на создание и изменение групп в клиенте Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efd5d-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="efd5d-113">Если у вас нет разрешений, обратитесь к администратору Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efd5d-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="efd5d-114">Теперь в PowerShell выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="efd5d-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="efd5d-115">Если группе приложений необходимо предоставить другой набор разрешений, создайте для таких приложений отдельную группу безопасности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="efd5d-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efd5d-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="efd5d-116">Next steps</span></span>

<span data-ttu-id="efd5d-117">Дополнительные сведения см. в статье [Защита хранилища ключей](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="efd5d-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
