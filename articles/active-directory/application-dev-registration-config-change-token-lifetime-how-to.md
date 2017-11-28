---
title: "Как изменить стандартное время существования токена для специально разработанного приложения | Документы Майкрософт"
description: "Обновление политик времени существования токена для приложения, разрабатываемого в Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="d20c4-103">Как изменить стандартное время существования токена для специально разработанного приложения</span><span class="sxs-lookup"><span data-stu-id="d20c4-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="d20c4-104">Azure AD Premium позволяет разработчикам приложений и администраторам клиентов настраивать время существования токенов, выпущенных для клиентов, не входящих в число конфиденциальных.</span><span class="sxs-lookup"><span data-stu-id="d20c4-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="d20c4-105">Политики времени существования токенов настраиваются на уровне клиента или ресурсов, к которым осуществляется доступ.</span><span class="sxs-lookup"><span data-stu-id="d20c4-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="d20c4-106">Чтобы задать политику времени существования токена, нужно скачать [модуль Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="d20c4-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="d20c4-107">Выполните команду **Connect-AzureAD-Confirm**.</span><span class="sxs-lookup"><span data-stu-id="d20c4-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="d20c4-108">Ниже приведен пример политики, в котором задается токен обновления максимального возраста с одним фактором.</span><span class="sxs-lookup"><span data-stu-id="d20c4-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="d20c4-109">Создайте политику: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```.</span><span class="sxs-lookup"><span data-stu-id="d20c4-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="d20c4-110">Дополнительные сведения о создании пользовательских параметров см. в документе [Настройка времени существования токенов](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes).</span><span class="sxs-lookup"><span data-stu-id="d20c4-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d20c4-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d20c4-111">Next steps</span></span>
[<span data-ttu-id="d20c4-112">Настройка времени существования токенов</span><span class="sxs-lookup"><span data-stu-id="d20c4-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="d20c4-113">Справочник по токенам в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d20c4-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

