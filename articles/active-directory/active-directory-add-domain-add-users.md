---
title: "Назначение пользователей для личного домена в Azure Active Directory | Документация Майкрософт"
description: "Инструкции по заполнению пользовательского домена в Azure Active Directory учетными записями пользователей."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="f9d04-103">Назначение пользователей пользовательскому домену</span><span class="sxs-lookup"><span data-stu-id="f9d04-103">Assign users to a custom domain</span></span>
<span data-ttu-id="f9d04-104">Добавив пользовательский домен в Azure Active Directory, вам нужно добавить учетные записи пользователей этого домена, чтобы затем начать проверку их подлинности.</span><span class="sxs-lookup"><span data-stu-id="f9d04-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9d04-105">Для управления службой Azure AD мы рекомендуем использовать [Центр администрирования Azure AD](https://aad.portal.azure.com) на портале Azure, а не классический портал Azure, который упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f9d04-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="f9d04-106">Сведения об управлении доменными именами в центре администрирования Azure AD см. в статье [Управление личными доменными именами в Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f9d04-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="f9d04-107">Пользователи, синхронизированные из локального каталога</span><span class="sxs-lookup"><span data-stu-id="f9d04-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="f9d04-108">Если вы уже настроили связь между локальным каталогом Active Directory и Azure Active Directory, учетные записи будут добавлены во время синхронизации.</span><span class="sxs-lookup"><span data-stu-id="f9d04-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="f9d04-109">Дополнительные сведения о синхронизации Azure Active Directory с локальным каталогом Active Directory см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f9d04-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="f9d04-110">Пользователи добавляются и управляются в облаке</span><span class="sxs-lookup"><span data-stu-id="f9d04-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="f9d04-111">Изменение домена для существующей учетной записи пользователя:</span><span class="sxs-lookup"><span data-stu-id="f9d04-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="f9d04-112">Откройте классический портал Azure под учетной записью глобального администратора или администратора пользователей.</span><span class="sxs-lookup"><span data-stu-id="f9d04-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="f9d04-113">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="f9d04-113">Open your directory.</span></span>
3. <span data-ttu-id="f9d04-114">Перейдите на вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="f9d04-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="f9d04-115">Выберите пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="f9d04-115">Select the user from the list.</span></span>
5. <span data-ttu-id="f9d04-116">Измените домен для пользователя и выберите параметр **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f9d04-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="f9d04-117">То же самое можно сделать с помощью [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) или [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="f9d04-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="f9d04-118">Выбор пользовательского домена при создании пользователя</span><span class="sxs-lookup"><span data-stu-id="f9d04-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="f9d04-119">Откройте классический портал Azure под учетной записью глобального администратора или администратора пользователей.</span><span class="sxs-lookup"><span data-stu-id="f9d04-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="f9d04-120">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="f9d04-120">Open your directory.</span></span>
3. <span data-ttu-id="f9d04-121">Перейдите на вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="f9d04-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="f9d04-122">На панели команд нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f9d04-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="f9d04-123">При добавлении имени пользователя выберите пользовательский домен из списка доменов.</span><span class="sxs-lookup"><span data-stu-id="f9d04-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="f9d04-124">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f9d04-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9d04-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9d04-125">Next steps</span></span>
* [<span data-ttu-id="f9d04-126">Использование пользовательских доменных имен для упрощения входа пользователей в систему</span><span class="sxs-lookup"><span data-stu-id="f9d04-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="f9d04-127">Управление именами пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="f9d04-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="f9d04-128">Общие сведения об управлении доменами в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9d04-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

