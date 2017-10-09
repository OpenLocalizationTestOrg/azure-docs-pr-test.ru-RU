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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Предоставьте разрешение toomany приложений tooaccess хранилища ключей

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>Вопрос. у меня несколько приложений (16), которые должны tooaccess хранилища ключей. Так как хранилище ключей разрешает доступ только 16 приложениям, как получить доступ остальным приложениям?

Политика контроля доступа хранилища ключей поддерживает не более 16 приложений. Однако вы можете создать группу безопасности Azure Active Directory. Добавьте все hello связанная группа безопасности toothis участников службы, а затем предоставьте доступ toothis безопасности группы tooKey хранилища.

Ниже приведены необходимые компоненты hello.
* [Установка модуля PowerShell V2 для Azure Active Directory](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Установите Azure PowerShell](/powershell/azure/overview).
* toorun hello следующими командами, требуются разрешения toocreate или изменение группы в клиенте Azure Active Directory hello. Если у вас нет разрешений, может потребоваться toocontact администратору Azure Active Directory.

Теперь выполните следующие команды в PowerShell hello.

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

Если вам требуется toogrant другой набор разрешений tooa группу приложений, создайте отдельную группу безопасности Azure Active Directory для таких приложений.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о том, как слишком[безопасного хранилища ключей](key-vault-secure-your-key-vault.md).
