---
title: "ИД клиента hello хранилища ключей aaaChange после перемещения подписки | Документы Microsoft"
description: "Дополнительные сведения, перемещение другой клиент tooa ИД клиента hello tooswitch для хранилища ключей после подписки"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Изменение идентификатора клиента хранилища ключей после перемещения подписки
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>Вопрос. у моего подписки был перемещен из клиента A tootenant б. Как изменить hello ИД клиента для моей существующего хранилища ключей и установленным правильные списки управления доступом для участников в клиенте B?
При создании нового ключа хранилища в подписке, это идентификатор клиента Azure Active Directory автоматически равноценных toohello по умолчанию для этой подписки. Все операции политики доступа также являются идентификатора равноценных toothis клиента. При перемещении вашей подписке Azure из клиента tootenant B, ваш существующий ключ, который они недоступны для хранилищ Здравствуйте субъекты (пользователи и приложения) в toofix клиента б. эту проблему, необходимо:

* Измените идентификатор клиента hello, связанный с все существующие хранилища ключей в этой подписке tootenant б.
* Удалите все существующие записи политики доступа.
* Добавьте новые записи политики доступа, связанные с клиентом Б.

Например, при наличии хранилища ключей «myvault» в подписке, которая была перенесена в клиента A tootenant B, здесь как toochange hello идентификатор клиента для этого ключа хранилища и удалить старые политики доступа.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

За это хранилище в клиенте A перед перемещением hello hello исходное значение **$vault. Properties.TenantId** -A клиента while **(Get-AzureRmContext). Tenant.TenantId** клиента б.

Теперь, когда ваше хранилище связано с Идентификатором hello правильный клиента и удаляются старые записи политики доступа, задать новый доступ записи политики с [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Дальнейшие действия
Если у вас есть вопросы о хранилище ключей Azure, посетите hello [форумы хранилище ключей Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

