---
title: "Необходимые условия для каталога данных aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о предварительных требованиях hello, необходимые tooget работы с помощью каталога данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="b01f3-103">Предварительные условия для работы с каталогом данных Azure</span><span class="sxs-lookup"><span data-stu-id="b01f3-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="b01f3-104">Перед настройкой каталога данных Azure необходимо tootake заботиться о несколько вещей.</span><span class="sxs-lookup"><span data-stu-id="b01f3-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="b01f3-105">Не беспокойтесь, этот процесс не займет много времени.</span><span class="sxs-lookup"><span data-stu-id="b01f3-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="b01f3-106">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="b01f3-106">Azure subscription</span></span>
<span data-ttu-id="b01f3-107">tooset копирование каталога данных, необходимо быть hello владелец или совладелец подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="b01f3-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="b01f3-108">Azure подписки позволяют упорядочивать доступ службы toocloud ресурсы, такие как каталог данных.</span><span class="sxs-lookup"><span data-stu-id="b01f3-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="b01f3-109">Они также позволяют управлять составлением отчетов об использовании ресурса, выставлением счетов за использование и их оплатой.</span><span class="sxs-lookup"><span data-stu-id="b01f3-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="b01f3-110">Каждая подписка может иметь отдельные настройки для выставления счетов и их оплаты, поэтому у вас могут быть разные подписки и тарифные планы для разных отделов, проектов, региональных офисов и т. д.</span><span class="sxs-lookup"><span data-stu-id="b01f3-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="b01f3-111">Каждая облачная служба привязана tooa подписки и необходимость toohave подписки перед настройкой каталога данных.</span><span class="sxs-lookup"><span data-stu-id="b01f3-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="b01f3-112">toolearn более, в разделе [управление учетными записями, подписками и административные роли](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b01f3-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="b01f3-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b01f3-113">Azure Active Directory</span></span>
<span data-ttu-id="b01f3-114">tooset копирование каталога данных, необходимо войти с учетной записью пользователя Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b01f3-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="b01f3-115">Azure AD предоставляет простой способ для вашего бизнеса toomanage удостоверениями и доступом в облаке hello и локальных.</span><span class="sxs-lookup"><span data-stu-id="b01f3-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="b01f3-116">Пользователи могут использовать одну рабочую или учебную учетную запись для одной tooany облака и локальных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b01f3-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="b01f3-117">Каталог данных использует Azure AD tooauthenticate вход.</span><span class="sxs-lookup"><span data-stu-id="b01f3-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="b01f3-118">toolearn более, в разделе [что такое Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b01f3-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b01f3-119">С помощью hello [портал Azure](http://portal.azure.com/), вы можете войти с использованием личную учетную запись Майкрософт или Azure Active Directory рабочая или учебная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="b01f3-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="b01f3-120">либо hello tooset копию данных каталога с помощью портала Azure или hello [портала каталога данных](http://www.azuredatacatalog.com), необходимо войти в систему с учетной записью Azure Active Directory не личную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b01f3-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="b01f3-121">Настройка политики Active Directory</span><span class="sxs-lookup"><span data-stu-id="b01f3-121">Active Directory policy configuration</span></span>
<span data-ttu-id="b01f3-122">Может возникнуть ситуация, где вы сможете войти в портал toohello каталога данных, но при попытке toosign в средство регистрации источника данных toohello, возникает сообщение об ошибке, которая запрещает вход.</span><span class="sxs-lookup"><span data-stu-id="b01f3-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="b01f3-123">Это проблема может произойти только в том случае, если вы в сети компании hello или возможны только при подключении из hello вне корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="b01f3-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="b01f3-124">Средство регистрации источника данных Hello использует toovalidate форм проверки подлинности учетных данных пользователя в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b01f3-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="b01f3-125">toohelp при входе в успешно, администратор Active Directory необходимо включить проверку подлинности форм в hello глобальной политики проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b01f3-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="b01f3-126">Hello глобальной политики проверки подлинности методы проверки подлинности может быть отдельно для интрасети и экстрасети подключения, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="b01f3-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="b01f3-127">Если не включена проверка подлинности форм для hello сети, из которого вы подключаетесь, могут возникать ошибки входа.</span><span class="sxs-lookup"><span data-stu-id="b01f3-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Глобальная политика аутентификации AD FS](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="b01f3-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b01f3-129">Next steps</span></span>
<span data-ttu-id="b01f3-130">Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="b01f3-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
