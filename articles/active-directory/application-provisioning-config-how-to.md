---
title: "Подготовка приложения Azure AD tooan коллекции пользователей tooconfigure aaaHow | Документы Microsoft"
description: "Как можно быстро настроить многофункциональном пользовательском запись подготовки и отзыва tooapplications уже присутствует в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="d5509-103">Способ подготовки приложения Azure AD tooan коллекции пользователей tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d5509-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="d5509-104">*Подготовка учетной записи пользователя* это hello act, создание, обновление или отключение учетных записях пользователя в хранилище профилей локальных пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="d5509-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="d5509-105">Большинство облака и приложений SaaS сохранить hello роли пользователей и разрешения в магазин профиль локального пользователя и наличие такой записи пользователя в локальном хранилище является *необходимые* для единого входа и доступа toowork.</span><span class="sxs-lookup"><span data-stu-id="d5509-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="d5509-106">В hello портал Azure, hello **Provisioning** вкладке hello левой панели навигации для корпоративного приложения отображаются какие подготовки режимы поддерживаются для данного приложения.</span><span class="sxs-lookup"><span data-stu-id="d5509-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="d5509-107">На ней может быть указано одно из двух значений:</span><span class="sxs-lookup"><span data-stu-id="d5509-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="d5509-108">Настройка приложения для подготовки вручную</span><span class="sxs-lookup"><span data-stu-id="d5509-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="d5509-109">*Вручную* подготовки означает, что учетные записи пользователей должна быть создана вручную с помощью hello методы, предоставляемые этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d5509-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="d5509-110">Например, может потребоваться войти на портал администратора для этого приложения и добавить пользователей с помощью веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d5509-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="d5509-111">Или отправить электронную таблицу со сведениями об учетной записи пользователя с помощью соответствующего механизма, который предоставляется приложением.</span><span class="sxs-lookup"><span data-stu-id="d5509-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="d5509-112">В документации hello предоставляемых приложение hello, или приложение hello контакта разработчика toodetermine wat механизмы доступны.</span><span class="sxs-lookup"><span data-stu-id="d5509-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="d5509-113">Если вручную только режим hello отображается для данного приложения, это означает, что был создан без подготовки соединитель автоматического Azure AD для приложения hello еще.</span><span class="sxs-lookup"><span data-stu-id="d5509-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="d5509-114">Или это означает, что приложение hello не не поддержки hello необходимого пользователя API управления после какие toobuild соединителя автоматической подготовки.</span><span class="sxs-lookup"><span data-stu-id="d5509-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="d5509-115">Если требуется поддержка toorequest автоматическую подготовку для данного приложения, можете заполнить запрос на <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="d5509-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="d5509-116">Настройка приложения для автоматической подготовки</span><span class="sxs-lookup"><span data-stu-id="d5509-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="d5509-117">*Автоматическая подготовка* означает, что для этого приложения был разработан соединитель для подготовки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5509-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="d5509-118">Дополнительные сведения о hello Azure AD на подготовку службы и как он работает, в разделе [tooSaaS автоматизировать подготовку пользователей и их отзыва приложений с Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="d5509-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="d5509-119">Дополнительные сведения о статье tooprovision определенных пользователей и групп tooan приложения, [управление Подготовка учетной записи пользователя для корпоративных приложений](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="d5509-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="d5509-120">Здравствуйте tooenable необходимые процедуры и настройте автоматическую подготовку различаются в зависимости от приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d5509-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="d5509-121">Необходимо начать с поиск hello установки учебника конкретных toosetting копирование подготовки для приложения и после этих шагов tooconfigure приложение hello и Azure AD toocreate hello инициализации подключения.</span><span class="sxs-lookup"><span data-stu-id="d5509-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="d5509-122">Учебники приложения можно найти на [список учебников по tooIntegrate приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="d5509-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="d5509-123">Tooconsider важно при настройке подготовки быть tooreview и настроить сопоставления атрибутов hello и рабочие процессы, определяющие, какой поток свойства пользователь (или группа) из toohello приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5509-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="d5509-124">Сюда входят свойства hello «сопоставления», будет использоваться toouniquely определить, соответствуют пользователи и группы, между системами двух hello.</span><span class="sxs-lookup"><span data-stu-id="d5509-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="d5509-125">Дополнительные сведения об этом важном процессе см. в разделах, указанных ниже.</span><span class="sxs-lookup"><span data-stu-id="d5509-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5509-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5509-126">Next steps</span></span>
[<span data-ttu-id="d5509-127">Настройка сопоставлений атрибутов для подготовки пользователей для приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5509-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

