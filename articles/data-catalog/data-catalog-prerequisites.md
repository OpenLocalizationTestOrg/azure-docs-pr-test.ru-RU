---
title: "Необходимые компоненты каталога данных Azure | Документация Майкрософт"
description: "Сведения о необходимых компонентах, которые нужны для начала работы с каталогом данных Azure."
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
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="35a67-103">Предварительные условия для работы с каталогом данных Azure</span><span class="sxs-lookup"><span data-stu-id="35a67-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="35a67-104">Перед настройкой каталога данных Azure следует решить несколько вопросов.</span><span class="sxs-lookup"><span data-stu-id="35a67-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="35a67-105">Не беспокойтесь, этот процесс не займет много времени.</span><span class="sxs-lookup"><span data-stu-id="35a67-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="35a67-106">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="35a67-106">Azure subscription</span></span>
<span data-ttu-id="35a67-107">Чтобы настроить каталог данных, необходимо быть владельцем или совладельцем подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="35a67-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="35a67-108">Подписки Azure помогают организовать доступ к ресурсам облачных служб, таких как каталог данных.</span><span class="sxs-lookup"><span data-stu-id="35a67-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="35a67-109">Они также позволяют управлять составлением отчетов об использовании ресурса, выставлением счетов за использование и их оплатой.</span><span class="sxs-lookup"><span data-stu-id="35a67-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="35a67-110">Каждая подписка может иметь отдельные настройки для выставления счетов и их оплаты, поэтому у вас могут быть разные подписки и тарифные планы для разных отделов, проектов, региональных офисов и т. д.</span><span class="sxs-lookup"><span data-stu-id="35a67-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="35a67-111">Каждая облачная служба привязана к подписке, поэтому необходимо иметь подписку перед настройкой каталога данных.</span><span class="sxs-lookup"><span data-stu-id="35a67-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="35a67-112">Дополнительные сведения см. в статье [Связь между подписками Azure и службой Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="35a67-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="35a67-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35a67-113">Azure Active Directory</span></span>
<span data-ttu-id="35a67-114">Для настройки каталога данных необходимо выполнить вход с помощью учетной записи пользователя Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35a67-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="35a67-115">Azure AD предоставляет компаниям простой способ управления удостоверениями и доступом не только в облаке, но и локально.</span><span class="sxs-lookup"><span data-stu-id="35a67-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="35a67-116">Пользователи могут использовать единую рабочую или учебную учетную запись для единого входа во все облачные и локальные веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="35a67-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="35a67-117">Каталог данных использует Azure AD для проверки подлинности входа.</span><span class="sxs-lookup"><span data-stu-id="35a67-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="35a67-118">Дополнительные сведения см. в статье [Что такое Azure Active Directory](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35a67-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="35a67-119">Пользователи могут входить на [портал Azure](http://portal.azure.com/) с помощью личной учетной записи Майкрософт, а также рабочей или учебной учетной записи Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35a67-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="35a67-120">Чтобы настроить каталог данных с помощью портала Azure или [портала каталога данных](http://www.azuredatacatalog.com), необходимо войти с помощью учетной записью Azure Active Directory, а не личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="35a67-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="35a67-121">Настройка политики Active Directory</span><span class="sxs-lookup"><span data-stu-id="35a67-121">Active Directory policy configuration</span></span>
<span data-ttu-id="35a67-122">Бывает, что пользователь может войти на портал каталога данных, но при попытке входа в средство регистрации источника данных отображается сообщение об ошибке, которая запрещает вход в систему.</span><span class="sxs-lookup"><span data-stu-id="35a67-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="35a67-123">Эта ошибка может происходить только в том случае, если пользователь находится в локальной сети, или только в том случае, если пользователь подключается из-за пределов сети компании.</span><span class="sxs-lookup"><span data-stu-id="35a67-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="35a67-124">Средство регистрации источника данных использует проверку подлинности форм для проверки учетных данных пользователя в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35a67-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="35a67-125">Для успешного входа в систему администратор Azure Active Directory должен включить проверку подлинности на основе форм в глобальной политике проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="35a67-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="35a67-126">Глобальная политика проверки подлинности позволяет включать методы проверки подлинности отдельно для подключений в интрасети и экстрасети, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="35a67-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="35a67-127">Ошибки входа в систему могут возникать, если не включена проверка подлинности на основе форм для сети, из которой подключается пользователь.</span><span class="sxs-lookup"><span data-stu-id="35a67-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Глобальная политика аутентификации AD FS](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="35a67-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35a67-129">Next steps</span></span>
<span data-ttu-id="35a67-130">Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="35a67-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
