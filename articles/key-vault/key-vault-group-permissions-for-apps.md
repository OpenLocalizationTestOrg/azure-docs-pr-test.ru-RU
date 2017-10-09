---
title: "aaaGrant разрешение toomany приложений tooaccess хранилище ключей Azure | Документы Microsoft"
description: "Узнайте, как toogrant разрешение toomany приложений tooaccess ключ в хранилище"
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
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="0cf43-103">Предоставьте разрешение toomany приложений tooaccess хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0cf43-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="0cf43-104">Вопрос. у меня несколько приложений (16), которые должны tooaccess хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0cf43-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="0cf43-105">Так как хранилище ключей разрешает доступ только 16 приложениям, как получить доступ остальным приложениям?</span><span class="sxs-lookup"><span data-stu-id="0cf43-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="0cf43-106">Политика контроля доступа хранилища ключей поддерживает не более 16 приложений.</span><span class="sxs-lookup"><span data-stu-id="0cf43-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="0cf43-107">Однако вы можете создать группу безопасности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0cf43-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="0cf43-108">Добавьте все hello связанная группа безопасности toothis участников службы, а затем предоставьте доступ toothis безопасности группы tooKey хранилища.</span><span class="sxs-lookup"><span data-stu-id="0cf43-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="0cf43-109">Ниже приведены необходимые компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="0cf43-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="0cf43-110">[Установка модуля PowerShell V2 для Azure Active Directory](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="0cf43-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="0cf43-111">[Установите Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0cf43-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0cf43-112">toorun hello следующими командами, требуются разрешения toocreate или изменение группы в клиенте Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="0cf43-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="0cf43-113">Если у вас нет разрешений, может потребоваться toocontact администратору Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0cf43-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="0cf43-114">Теперь выполните следующие команды в PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0cf43-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="0cf43-115">Если вам требуется toogrant другой набор разрешений tooa группу приложений, создайте отдельную группу безопасности Azure Active Directory для таких приложений.</span><span class="sxs-lookup"><span data-stu-id="0cf43-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cf43-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cf43-116">Next steps</span></span>

<span data-ttu-id="0cf43-117">Дополнительные сведения о том, как слишком[безопасного хранилища ключей](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0cf43-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
