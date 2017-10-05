---
title: "Управление именами личных доменов в Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="47495-103">Управление личными доменными именами в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47495-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="47495-104">Доменное имя может выступать важным идентификатором для многих ресурсов каталога как часть:</span><span class="sxs-lookup"><span data-stu-id="47495-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="47495-105">имени или адреса электронной почты пользователя;</span><span class="sxs-lookup"><span data-stu-id="47495-105">A user name or email address for a user</span></span>
* <span data-ttu-id="47495-106">адреса группы;</span><span class="sxs-lookup"><span data-stu-id="47495-106">The address for a group</span></span>
* <span data-ttu-id="47495-107">URI идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="47495-107">The app ID URI for an application</span></span>

<span data-ttu-id="47495-108">Для использования в ресурсе Azure Active Directory (Azure AD) доменное имя должно принадлежать каталогу, содержащему ресурс.</span><span class="sxs-lookup"><span data-stu-id="47495-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="47495-109">Задачи управления доменами в Azure AD может выполнять только глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="47495-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47495-110">Для управления службой Azure AD мы рекомендуем использовать [Центр администрирования Azure AD](https://aad.portal.azure.com) на портале Azure, а не классический портал Azure, который упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="47495-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="47495-111">Сведения об управлении доменными именами в центре администрирования Azure AD см. в статье [Управление личными доменными именами в Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47495-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="47495-112">Установка основного доменного имени для каталога Azure AD</span><span class="sxs-lookup"><span data-stu-id="47495-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="47495-113">При создании каталога исходное доменное имя, например "contoso.onmicrosoft.com", также становится основным именем домена для каталога.</span><span class="sxs-lookup"><span data-stu-id="47495-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="47495-114">При создании нового пользователя на [классическом портале Azure](https://manage.windowsazure.com/)или на других порталах, таких как портал администрирования Office 365, основной домен становится доменным именем по умолчанию для пользователя.</span><span class="sxs-lookup"><span data-stu-id="47495-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="47495-115">Это упрощает процесс создания новых пользователей на портале для администратора.</span><span class="sxs-lookup"><span data-stu-id="47495-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="47495-116">Чтобы изменить основное доменное имя для каталога, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="47495-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="47495-117">Войдите на [классический портал Azure](https://manage.windowsazure.com/) как глобальный администратор каталога Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47495-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="47495-118">В области навигации слева выберите **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47495-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="47495-119">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="47495-119">Open your directory.</span></span>
4. <span data-ttu-id="47495-120">Перейдите на вкладку **Домены** .</span><span class="sxs-lookup"><span data-stu-id="47495-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="47495-121">Нажмите кнопку **Изменить основной** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="47495-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="47495-122">Выберите домен, который вы хотите назначить новым основным доменом каталога.</span><span class="sxs-lookup"><span data-stu-id="47495-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="47495-123">В качестве основного домена для каталога можно указать любой проверенный личный домен, который не является федеративным.</span><span class="sxs-lookup"><span data-stu-id="47495-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="47495-124">При изменении основного домена для каталога имена существующих пользователей не изменятся.</span><span class="sxs-lookup"><span data-stu-id="47495-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="47495-125">Добавление личных доменых имен в Azure AD</span><span class="sxs-lookup"><span data-stu-id="47495-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="47495-126">В каждый каталог Azure AD можно добавить до 900 личных доменых имен.</span><span class="sxs-lookup"><span data-stu-id="47495-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="47495-127">Процесс [добавления дополнительного личного домена](active-directory-add-domain.md) аналогичен добавлению первого личного домена.</span><span class="sxs-lookup"><span data-stu-id="47495-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="47495-128">Добавление поддоменов для личного домена</span><span class="sxs-lookup"><span data-stu-id="47495-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="47495-129">Если вы хотите добавить в ваш каталог доменное имя третьего уровня, например "europe.contoso.com", необходимо сначала добавить и проверить домен второго уровня, например "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="47495-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="47495-130">Поддомен будет проверен Azure AD автоматически.</span><span class="sxs-lookup"><span data-stu-id="47495-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="47495-131">Чтобы увидеть, проверен ли добавленный поддомен, обновите страницу со списком доменов в каталоге.</span><span class="sxs-lookup"><span data-stu-id="47495-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="47495-132">Что делать, если вы изменили регистратор DNS для пользовательского доменного имени</span><span class="sxs-lookup"><span data-stu-id="47495-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="47495-133">При изменении регистратора DNS для личного доменного имени это имя можно продолжать использовать в Azure AD без перерывов в обслуживании и без дополнительных настроек.</span><span class="sxs-lookup"><span data-stu-id="47495-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="47495-134">Если личное доменное имя используется в Office 365, Intune или других службах, которым необходимы личные домены в Azure AD, обратитесь к документации для этих служб.</span><span class="sxs-lookup"><span data-stu-id="47495-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="47495-135">Удаление имени личного домена</span><span class="sxs-lookup"><span data-stu-id="47495-135">Delete a custom domain name</span></span>
<span data-ttu-id="47495-136">Имя личного домена можно удалить из Azure AD, если ваша организация не использует его или если это доменное имя необходимо использовать с другой службой Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47495-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="47495-137">Перед удалением личного доменного имени необходимо убедиться, что от этого имени не зависят никакие ресурсы в каталоге.</span><span class="sxs-lookup"><span data-stu-id="47495-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="47495-138">Доменное имя невозможно удалить из каталога в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="47495-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="47495-139">Какой-либо пользователь имеет имя пользователя, адрес электронной почты или адрес прокси-сервера, которые включают это доменное имя.</span><span class="sxs-lookup"><span data-stu-id="47495-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="47495-140">Какая-либо группа имеет адрес электронной почты или адрес прокси-сервера, которые включают это доменное имя.</span><span class="sxs-lookup"><span data-stu-id="47495-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="47495-141">Какое-либо приложение в Azure AD имеет URI идентификатора приложения, который включает это доменное имя.</span><span class="sxs-lookup"><span data-stu-id="47495-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="47495-142">Перед удалением личного доменного имени необходимо изменить или удалить каждый такой ресурс в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47495-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="47495-143">Использование PowerShell или API Graph для управления доменными именами</span><span class="sxs-lookup"><span data-stu-id="47495-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="47495-144">Большинство задач по управлению доменными именами в Azure Active Directory также можно выполнить с помощью Microsoft PowerShell или программными средствами с помощью API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47495-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="47495-145">Управление доменными именами в Azure AD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="47495-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="47495-146">Управление именами доменов в Azure AD с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="47495-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="47495-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47495-147">Next steps</span></span>
* [<span data-ttu-id="47495-148">Дополнительные сведения об именах доменов в Azure AD</span><span class="sxs-lookup"><span data-stu-id="47495-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="47495-149">Управление именами пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="47495-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

