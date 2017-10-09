---
title: "aaaAssign пользователи tooa пользовательского домена в Azure Active Directory | Документы Microsoft"
description: "Как toopopulate пользовательского домена в Azure Active Directory с учетными записями пользователей."
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="af3db-103">Назначить пользователей tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="af3db-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="af3db-104">После добавления tooAzure ваш пользовательский домен Active Directory, необходимо добавить hello учетные записи пользователей для этого домена, чтобы можно было начать они проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="af3db-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af3db-105">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="af3db-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="af3db-106">Как toomanage домена имена в центре администрирования hello Azure AD, в разделе [управление пользовательские имена доменов в Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af3db-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="af3db-107">Пользователи, синхронизированные из локального каталога</span><span class="sxs-lookup"><span data-stu-id="af3db-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="af3db-108">Если вы уже настроили подключение между вашей локальной Active Directory и Azure Active Directory, синхронизации можно заполнить hello учетных записей.</span><span class="sxs-lookup"><span data-stu-id="af3db-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="af3db-109">Дополнительные сведения о том, как toosynchronize Azure Active Directory с локальными службами Active Directory, см. [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="af3db-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="af3db-110">Пользователи добавляются и управляются в облаке hello</span><span class="sxs-lookup"><span data-stu-id="af3db-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="af3db-111">домен hello toochange для существующей учетной записи пользователя:</span><span class="sxs-lookup"><span data-stu-id="af3db-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="af3db-112">Откройте hello классический портал Azure, используя учетную запись глобального администратора или администратора пользователей.</span><span class="sxs-lookup"><span data-stu-id="af3db-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="af3db-113">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="af3db-113">Open your directory.</span></span>
3. <span data-ttu-id="af3db-114">Выберите hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="af3db-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="af3db-115">Выберите hello пользователя из списка hello.</span><span class="sxs-lookup"><span data-stu-id="af3db-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="af3db-116">Изменить домен hello hello пользователя, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af3db-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="af3db-117">Это также может быть сделано с помощью [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) или hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="af3db-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="af3db-118">Выбор пользовательского домена при создании пользователя</span><span class="sxs-lookup"><span data-stu-id="af3db-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="af3db-119">Откройте hello классический портал Azure, используя учетную запись глобального администратора или администратора пользователей.</span><span class="sxs-lookup"><span data-stu-id="af3db-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="af3db-120">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="af3db-120">Open your directory.</span></span>
3. <span data-ttu-id="af3db-121">Выберите hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="af3db-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="af3db-122">В панели команд hello, выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="af3db-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="af3db-123">При добавлении имени пользователя hello выберите hello пользовательского домена из списка доменов hello.</span><span class="sxs-lookup"><span data-stu-id="af3db-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="af3db-124">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="af3db-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af3db-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af3db-125">Next steps</span></span>
* [<span data-ttu-id="af3db-126">С помощью пользовательских доменных имен toosimplify hello входа в систему для пользователей</span><span class="sxs-lookup"><span data-stu-id="af3db-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="af3db-127">Управление именами пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="af3db-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="af3db-128">Общие сведения об управлении доменами в Azure AD</span><span class="sxs-lookup"><span data-stu-id="af3db-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

