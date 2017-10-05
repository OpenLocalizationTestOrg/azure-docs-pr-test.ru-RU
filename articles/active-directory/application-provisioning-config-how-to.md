---
title: "Как настроить подготовку пользователей для приложения из коллекции Azure AD | Документы Майкрософт"
description: "В этой статье описано, как быстро настроить подготовку и отмену подготовки учетных записей для приложений из коллекции приложений Azure AD."
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
ms.openlocfilehash: 2e38fcb30ea7632339a3ba8815a536872cfcc69e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-user-provisioning-to-an-azure-ad-gallery-application"></a><span data-ttu-id="fc8fa-103">Как настроить подготовку пользователей для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc8fa-103">How to configure user provisioning to an Azure AD Gallery application</span></span>

<span data-ttu-id="fc8fa-104">*Подготовка учетной записи пользователя* — это создание, обновление или отключение записей для учетных записей пользователя в локальном хранилище профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-104">*User account provisioning* is the act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="fc8fa-105">В большинстве облачных приложений и приложений SaaS разрешения и роли пользователей хранятся в собственном локальном хранилище профилей пользователей, и для настройки единого входа и доступа *необходимо* наличие такой записи о пользователе.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-105">Most cloud and SaaS applications store the users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access to work.</span></span>

<span data-ttu-id="fc8fa-106">На вкладке **Подготовка**, расположенной в портале Azure на панели навигации слева, отображаются поддерживаемые режимы подготовки для корпоративного приложения.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-106">In the Azure portal, the **Provisioning** tab in the left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="fc8fa-107">На ней может быть указано одно из двух значений:</span><span class="sxs-lookup"><span data-stu-id="fc8fa-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="fc8fa-108">Настройка приложения для подготовки вручную</span><span class="sxs-lookup"><span data-stu-id="fc8fa-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="fc8fa-109">Подготовка *вручную* означает, что учетные записи пользователей необходимо создать вручную с использованием методов, предоставляемых этим приложением.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-109">*Manual* provisioning means that user accounts must be created manually using the methods provided by that app.</span></span> <span data-ttu-id="fc8fa-110">Например, может потребоваться войти на портал администратора для этого приложения и добавить пользователей с помощью веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="fc8fa-111">Или отправить электронную таблицу со сведениями об учетной записи пользователя с помощью соответствующего механизма, который предоставляется приложением.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="fc8fa-112">Чтобы определить доступные механизмы, обратитесь к документации по приложению или свяжитесь с разработчиком приложения.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-112">Consult the documentation provided by the app, or contact the app developer to determine wat mechanisms are available.</span></span>

<span data-ttu-id="fc8fa-113">Если для приложения отображается только ручной режим, это означает, что для приложения еще не был создан соединитель для подготовки в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-113">If Manual is the only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for the app yet.</span></span> <span data-ttu-id="fc8fa-114">Это также может означать, что приложение не поддерживает необходимый API-интерфейс управления пользователями, на основании которого создается автоматический соединитель для развертывания.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-114">Or it means the app does not support the pre-requisite user management API upon which to build an automated provisioning connector.</span></span>

<span data-ttu-id="fc8fa-115">Если вы хотите запросить поддержку автоматической подготовки приложения, отправьте запрос на веб-сайт <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-115">If you would like to request support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="fc8fa-116">Настройка приложения для автоматической подготовки</span><span class="sxs-lookup"><span data-stu-id="fc8fa-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="fc8fa-117">*Автоматическая подготовка* означает, что для этого приложения был разработан соединитель для подготовки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="fc8fa-118">Дополнительные сведения о службе подготовки Azure AD и о том, как она работает, см. в разделе [Автоматическая подготовка пользователей и отмена подготовки для приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="fc8fa-118">For more information on the Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="fc8fa-119">Дополнительные сведения о подготовке определенных пользователей и групп для приложения см. в статье [Управление подготовкой учетных записей пользователей для корпоративных приложений](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="fc8fa-119">For more information on how to provision specific users and groups to an application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="fc8fa-120">Фактические действия, необходимые для включения и настройки автоматической подготовки, зависят от приложения.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-120">The actual steps required to enable and configure automatic provisioning vary depending on the application.</span></span>

>[!NOTE]
><span data-ttu-id="fc8fa-121">Для начала найдите руководство по настройке подготовки для вашего приложения и выполните инструкции по настройке соединителя для подготовки в приложении и в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-121">You should start by finding the setup tutorial specific to setting up provisioning for your application, and following those steps to configure both the app and Azure AD to create the provisioning connection.</span></span> 
>
>

<span data-ttu-id="fc8fa-122">Руководства по настройке для приложений можно найти в [Списке руководств по интеграции приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="fc8fa-122">App tutorials can be found at [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="fc8fa-123">При настройке подготовки важно просмотреть и настроить сопоставления атрибутов и рабочие процессы, которые определяют, какие свойства пользователя (или группы) передаются из Azure AD в приложение.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-123">An important thing to consider when setting up provisioning be to review and configure the attribute mappings and workflows that define which user (or group) properties flow from Azure AD to the application.</span></span> <span data-ttu-id="fc8fa-124">К ним относится "свойство сопоставления", используемое для уникальной идентификации и сопоставления пользователей или групп между двумя системами.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-124">This includes setting the “matching property” that be used to uniquely identify and match users/groups between the two systems.</span></span> <span data-ttu-id="fc8fa-125">Дополнительные сведения об этом важном процессе см. в разделах, указанных ниже.</span><span class="sxs-lookup"><span data-stu-id="fc8fa-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc8fa-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc8fa-126">Next steps</span></span>
[<span data-ttu-id="fc8fa-127">Настройка сопоставлений атрибутов для подготовки пользователей для приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc8fa-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

