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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="cd9a6-103">Изменение идентификатора клиента хранилища ключей после перемещения подписки</span><span class="sxs-lookup"><span data-stu-id="cd9a6-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="cd9a6-104">Вопрос. у моего подписки был перемещен из клиента A tootenant б. Как изменить hello ИД клиента для моей существующего хранилища ключей и установленным правильные списки управления доступом для участников в клиенте B?</span><span class="sxs-lookup"><span data-stu-id="cd9a6-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="cd9a6-105">При создании нового ключа хранилища в подписке, это идентификатор клиента Azure Active Directory автоматически равноценных toohello по умолчанию для этой подписки.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="cd9a6-106">Все операции политики доступа также являются идентификатора равноценных toothis клиента.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="cd9a6-107">При перемещении вашей подписке Azure из клиента tootenant B, ваш существующий ключ, который они недоступны для хранилищ Здравствуйте субъекты (пользователи и приложения) в toofix клиента б. эту проблему, необходимо:</span><span class="sxs-lookup"><span data-stu-id="cd9a6-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="cd9a6-108">Измените идентификатор клиента hello, связанный с все существующие хранилища ключей в этой подписке tootenant б.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="cd9a6-109">Удалите все существующие записи политики доступа.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="cd9a6-110">Добавьте новые записи политики доступа, связанные с клиентом Б.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="cd9a6-111">Например, при наличии хранилища ключей «myvault» в подписке, которая была перенесена в клиента A tootenant B, здесь как toochange hello идентификатор клиента для этого ключа хранилища и удалить старые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="cd9a6-112">За это хранилище в клиенте A перед перемещением hello hello исходное значение **$vault. Properties.TenantId** -A клиента while **(Get-AzureRmContext). Tenant.TenantId** клиента б.</span><span class="sxs-lookup"><span data-stu-id="cd9a6-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="cd9a6-113">Теперь, когда ваше хранилище связано с Идентификатором hello правильный клиента и удаляются старые записи политики доступа, задать новый доступ записи политики с [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd9a6-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd9a6-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd9a6-114">Next steps</span></span>
<span data-ttu-id="cd9a6-115">Если у вас есть вопросы о хранилище ключей Azure, посетите hello [форумы хранилище ключей Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="cd9a6-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

