---
title: "aaaManaging пользовательские имена доменов в Azure Active Directory | Документы Microsoft"
description: "Основные принципы и указания по управлению личными доменами в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="48eed-103">Управление личными доменными именами в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48eed-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="48eed-104">Доменное имя может выступать важным идентификатором для многих ресурсов каталога как часть:</span><span class="sxs-lookup"><span data-stu-id="48eed-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="48eed-105">имени или адреса электронной почты пользователя;</span><span class="sxs-lookup"><span data-stu-id="48eed-105">A user name or email address for a user</span></span>
* <span data-ttu-id="48eed-106">адрес Hello для группы</span><span class="sxs-lookup"><span data-stu-id="48eed-106">hello address for a group</span></span>
* <span data-ttu-id="48eed-107">приложение Hello URI идентификатора приложения</span><span class="sxs-lookup"><span data-stu-id="48eed-107">hello app ID URI for an application</span></span>

<span data-ttu-id="48eed-108">Ресурс в Azure Active Directory (Azure AD) может включать имя домена, которое уже проверена, что владельцем toobe hello каталог, содержащий ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="48eed-109">Задачи управления доменами в Azure AD может выполнять только глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="48eed-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48eed-110">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="48eed-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="48eed-111">Как toomanage домена имена в центре администрирования hello Azure AD, в разделе [управление пользовательские имена доменов в Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48eed-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="48eed-112">Задайте имя основного домена hello для вашего каталога Azure AD</span><span class="sxs-lookup"><span data-stu-id="48eed-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="48eed-113">При создании каталога hello исходное имя домена, например «contoso.onmicrosoft.com», также является именем основного домена hello для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="48eed-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="48eed-114">Основной домен Hello — hello по умолчанию доменное имя для нового пользователя, при создании нового пользователя в hello [классический портал Azure](https://manage.windowsazure.com/), или других порталов, такие как портал администрирования Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="48eed-115">Это упрощает процесс hello для администратора toocreate новых пользователей на портале hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="48eed-116">Имя основного домена hello toochange для каталога:</span><span class="sxs-lookup"><span data-stu-id="48eed-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="48eed-117">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетной записью пользователя, который является глобальным администратором каталога Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48eed-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="48eed-118">Выберите **Active Directory** на левой навигационной панели hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="48eed-119">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="48eed-119">Open your directory.</span></span>
4. <span data-ttu-id="48eed-120">Выберите hello **домены** вкладки.</span><span class="sxs-lookup"><span data-stu-id="48eed-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="48eed-121">Выберите hello **изменение основной** кнопки на панели команд hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="48eed-122">Выберите домен hello, что требуется toobe hello новый основной домен для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="48eed-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="48eed-123">Можно изменить hello основное имя домена для вашего каталога toobe проверенный пользовательский домен, который не является федеративным.</span><span class="sxs-lookup"><span data-stu-id="48eed-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="48eed-124">Изменение основного домена hello для вашего каталога не изменит приветствия имен пользователей для всех существующих пользователей.</span><span class="sxs-lookup"><span data-stu-id="48eed-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="48eed-125">Добавить tooyour имена пользовательских доменов Azure AD</span><span class="sxs-lookup"><span data-stu-id="48eed-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="48eed-126">Можно добавить пользовательский домен имена too900 tooeach-каталог Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48eed-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="48eed-127">Здравствуйте процесса слишком[добавить дополнительные пользовательские доменные имена](active-directory-add-domain.md) hello одинаково для hello первое имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="48eed-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="48eed-128">Добавление поддоменов для личного домена</span><span class="sxs-lookup"><span data-stu-id="48eed-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="48eed-129">Tooadd имя домена третьего уровня, например «europe.contoso.com» tooyour каталога следует сначала следует добавить и проверить hello домена второго уровня, например contoso.com. Hello поддомен проверяются автоматически с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48eed-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="48eed-130">проверил toosee, hello поддомен, который вы только что добавили hello страницу в браузере hello, список доменов hello в вашем каталоге.</span><span class="sxs-lookup"><span data-stu-id="48eed-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="48eed-131">Какие toodo при изменении hello регистратора DNS для пользовательского имени домена</span><span class="sxs-lookup"><span data-stu-id="48eed-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="48eed-132">Если изменить hello регистратора DNS для пользовательского имени домена, вы можете продолжить toouse пользовательское имя домена с Azure AD без прерывания работы и дополнительные задачи по настройке.</span><span class="sxs-lookup"><span data-stu-id="48eed-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="48eed-133">При использовании настраиваемого имени домена с Office 365, Intune и других служб, использующих пользовательские имена доменов в Azure AD см. документацию toohello для этих служб.</span><span class="sxs-lookup"><span data-stu-id="48eed-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="48eed-134">Удаление имени личного домена</span><span class="sxs-lookup"><span data-stu-id="48eed-134">Delete a custom domain name</span></span>
<span data-ttu-id="48eed-135">Пользовательское доменное имя можно удалить из Azure AD, если ваша организация больше не использует это имя домена, или в том случае, если требуется toouse этого доменного имени в другой Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48eed-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="48eed-136">toodelete пользовательского имени домена, сначала убедитесь, что нет ресурсов в вашем каталоге зависят от hello доменное имя.</span><span class="sxs-lookup"><span data-stu-id="48eed-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="48eed-137">Доменное имя невозможно удалить из каталога в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="48eed-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="48eed-138">Любой пользователь получает имя пользователя, адрес электронной почты или адрес прокси-сервера, включают hello доменное имя.</span><span class="sxs-lookup"><span data-stu-id="48eed-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="48eed-139">Любая группа имеет адрес электронной почты или адрес прокси-сервера, который включает имя домена hello.</span><span class="sxs-lookup"><span data-stu-id="48eed-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="48eed-140">Любое приложение в Azure AD имеет идентификатор URI, который включает hello имя домена приложения.</span><span class="sxs-lookup"><span data-stu-id="48eed-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="48eed-141">Необходимо изменить или удалить любой такой ресурс в каталоге Azure AD, перед удалением hello пользовательское имя домена.</span><span class="sxs-lookup"><span data-stu-id="48eed-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="48eed-142">Используйте PowerShell или Graph API toomanage доменных имен</span><span class="sxs-lookup"><span data-stu-id="48eed-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="48eed-143">Большинство задач по управлению доменными именами в Azure Active Directory также можно выполнить с помощью Microsoft PowerShell или программными средствами с помощью API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48eed-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="48eed-144">С помощью PowerShell toomanage доменных имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48eed-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="48eed-145">С помощью Graph API toomanage доменных имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48eed-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="48eed-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48eed-146">Next steps</span></span>
* [<span data-ttu-id="48eed-147">Дополнительные сведения об именах доменов в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48eed-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="48eed-148">Управление именами пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="48eed-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

