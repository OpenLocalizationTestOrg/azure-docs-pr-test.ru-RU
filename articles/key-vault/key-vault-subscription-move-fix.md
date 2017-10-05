---
title: "Изменение идентификатора клиента хранилища ключей после перемещения подписки | Документация Майкрософт"
description: "Узнайте, как изменить идентификатор клиента хранилища ключей после перемещения подписки в другой клиент."
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="3d2f2-103">Изменение идентификатора клиента хранилища ключей после перемещения подписки</span><span class="sxs-lookup"><span data-stu-id="3d2f2-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="3d2f2-104">В. Моя подписка перемещена из клиента А в клиент Б. Как изменить идентификатор клиента имеющегося хранилища ключей и настроить правильные списки ACL для субъектов в клиенте Б?</span><span class="sxs-lookup"><span data-stu-id="3d2f2-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="3d2f2-105">При создании хранилища ключей в подписке оно автоматически привязывается к идентификатору клиента Azure Active Directory по умолчанию для этой подписки.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="3d2f2-106">Все записи политики доступа также привязываются к этому идентификатору клиента.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="3d2f2-107">При перемещении подписки Azure из клиента A в клиент Б существующие хранилища ключей недоступны для субъектов (пользователей и приложений) в клиенте Б. Вот как устранить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="3d2f2-108">Измените идентификатор клиента, связанный со всеми существующими хранилищами ключей в этой подписке, для клиента Б.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="3d2f2-109">Удалите все существующие записи политики доступа.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="3d2f2-110">Добавьте новые записи политики доступа, связанные с клиентом Б.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="3d2f2-111">Например, при наличии хранилища ключей myvault в подписке, которая была перенесена из клиента A в клиент Б, необходимо изменить идентификатор клиента для этого хранилища ключей и удалить старые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="3d2f2-112">Так как это хранилище находилось в клиенте A перед перемещением, исходное значение **$vault.Properties.TenantId** является клиентом А, в то время как значение **(Get-AzureRmContext).Tenant.TenantId** — это клиент Б.</span><span class="sxs-lookup"><span data-stu-id="3d2f2-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="3d2f2-113">Теперь, когда хранилище связано с правильным идентификатором клиента и старые записи политики доступа удалены, можно настроить новые записи политики доступа с помощью командлета [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d2f2-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d2f2-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d2f2-114">Next steps</span></span>
<span data-ttu-id="3d2f2-115">Если у вас возникли вопросы о хранилище ключей Azure, посетите [форумы хранилища ключей Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)</span><span class="sxs-lookup"><span data-stu-id="3d2f2-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

