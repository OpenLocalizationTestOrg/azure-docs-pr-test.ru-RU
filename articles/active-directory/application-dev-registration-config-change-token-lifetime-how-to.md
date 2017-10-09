---
title: "время существования маркера hello aaaHow toochange по умолчанию для приложения, разработанного | Документы Microsoft"
description: "Как политики tooupdate время существования маркера для приложения, которое вы разрабатываете в Azure AD"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="0bb27-103">Как время существования маркера hello toochange по умолчанию для приложения, разработанного</span><span class="sxs-lookup"><span data-stu-id="0bb27-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="0bb27-104">Azure AD Premium позволяет разработчикам приложений и клиента администраторов tooconfigure hello временем существования маркеры, выпущенные для конфиденциальные клиентов.</span><span class="sxs-lookup"><span data-stu-id="0bb27-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="0bb27-105">Время существования маркера политики задаются на уровне клиента или hello ресурсов, к которому выполняется доступ.</span><span class="sxs-lookup"><span data-stu-id="0bb27-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="0bb27-106">tooset политику времени существования маркера необходимо toodownload hello [модуля Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="0bb27-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="0bb27-107">Запустите hello **Connect AzureAD-Подтверждение** команды.</span><span class="sxs-lookup"><span data-stu-id="0bb27-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="0bb27-108">Ниже приведен пример политики, задает токен обновления дисперсионный max-age hello.</span><span class="sxs-lookup"><span data-stu-id="0bb27-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="0bb27-109">Создайте политику hello.```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="0bb27-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="0bb27-110">Извлечение hello [время существования маркера Настройка](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) документа как toolearn toocreate другие пользовательские.</span><span class="sxs-lookup"><span data-stu-id="0bb27-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bb27-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bb27-111">Next steps</span></span>
[<span data-ttu-id="0bb27-112">Настройка времени существования токенов</span><span class="sxs-lookup"><span data-stu-id="0bb27-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="0bb27-113">Справочник по токенам в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bb27-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

