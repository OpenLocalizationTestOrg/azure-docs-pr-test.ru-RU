---
title: "Azure Active Directory B2C: создание клиента Azure Active Directory B2C | Документация Майкрософт"
description: "Инструкции по созданию клиента Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 8a1d4935397f59e5813afc6f04559e471187a779
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="38140-103">Создание клиента Azure Active Directory B2C на портале Azure</span><span class="sxs-lookup"><span data-stu-id="38140-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="38140-104">Из этого краткого руководства вы узнаете, как создать клиент Microsoft Azure Active Directory (Azure AD) B2C за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="38140-104">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="38140-105">По завершении у вас будет клиент B2C для регистрации приложений B2C.</span><span class="sxs-lookup"><span data-stu-id="38140-105">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38140-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38140-106">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="38140-107">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="38140-107">Log in to Azure</span></span>

<span data-ttu-id="38140-108">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38140-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="38140-109">Создание клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="38140-109">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="38140-110">Возможности B2C невозможно включить в имеющихся клиентах.</span><span class="sxs-lookup"><span data-stu-id="38140-110">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="38140-111">Нужно создать клиент Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="38140-111">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="38140-112">Поздравляем! Вы создали клиент Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="38140-112">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="38140-113">Теперь вы — глобальный администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="38140-113">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="38140-114">При необходимости можно добавить других глобальных администраторов.</span><span class="sxs-lookup"><span data-stu-id="38140-114">You can add other Global Administrators as required.</span></span> <span data-ttu-id="38140-115">Чтобы переключиться к новому клиенту, щелкните *ссылку для управления новым клиентом*.</span><span class="sxs-lookup"><span data-stu-id="38140-115">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Ссылка для управления новым клиентом](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="38140-117">Если вы планируете использовать B2C клиент для рабочего приложения, см. статью, в которой [сравниваются рабочая версия и предварительная версия клиента B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="38140-117">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="38140-118">При удалении существующего клиента B2C и его повторном создании с тем же доменным именем могут возникнуть известные проблемы.</span><span class="sxs-lookup"><span data-stu-id="38140-118">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="38140-119">Создавайте клиент B2C с другим доменным именем.</span><span class="sxs-lookup"><span data-stu-id="38140-119">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="38140-120">Привязка клиента к подписке</span><span class="sxs-lookup"><span data-stu-id="38140-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="38140-121">Клиент Azure AD B2C нужно связать с подпиской Azure, чтобы включить все возможности B2C и вносить плату за использование.</span><span class="sxs-lookup"><span data-stu-id="38140-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="38140-122">Дополнительные сведения см. в [этой статье](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="38140-122">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="38140-123">Если не связать клиент Azure AD B2C с подпиской Azure, некоторые возможности будут заблокированы, а в колонке параметров B2C отобразится предупреждение No Subscription linked to this B2C tenant or the Subscription needs your attention (С этим клиентом B2C не связана ни одна подписка, или подписка требует вашего внимания).</span><span class="sxs-lookup"><span data-stu-id="38140-123">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="38140-124">Важно выполнить этот шаг, прежде чем переводить приложения в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="38140-124">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="38140-125">Простой доступ к параметрам</span><span class="sxs-lookup"><span data-stu-id="38140-125">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="38140-126">Чтобы получить доступ к колонке, можно также ввести `Azure AD B2C` в поле **Поиск ресурсов** в верхней части портала.</span><span class="sxs-lookup"><span data-stu-id="38140-126">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="38140-127">В списке результатов выберите **Azure AD B2C** для доступа к колонке параметров B2C.</span><span class="sxs-lookup"><span data-stu-id="38140-127">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38140-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38140-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38140-129">Azure Active Directory B2C: регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="38140-129">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)