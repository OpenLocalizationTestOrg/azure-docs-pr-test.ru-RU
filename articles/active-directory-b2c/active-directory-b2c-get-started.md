---
title: "Azure Active Directory B2C: создание клиента Azure Active Directory B2C | Документация Майкрософт"
description: "Как для клиента Azure Active Directory B2C toocreate на раздел"
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="c1f98-103">Создание клиента Azure Active Directory B2C в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c1f98-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="c1f98-104">Редактировать Sipi.</span><span class="sxs-lookup"><span data-stu-id="c1f98-104">Edited by Sipi.</span></span>

<span data-ttu-id="c1f98-105">Из этого краткого руководства вы узнаете, как создать клиент Microsoft Azure Active Directory (Azure AD) B2C за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c1f98-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="c1f98-106">Когда закончите, у вас toouse клиента B2C для регистрации приложений B2C.</span><span class="sxs-lookup"><span data-stu-id="c1f98-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1f98-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c1f98-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="c1f98-108">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="c1f98-108">Log in tooAzure</span></span>

<span data-ttu-id="c1f98-109">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c1f98-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="c1f98-110">Создание клиента Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c1f98-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="c1f98-111">Возможности B2C невозможно включить в имеющихся клиентах.</span><span class="sxs-lookup"><span data-stu-id="c1f98-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="c1f98-112">Необходимо toocreate клиент Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c1f98-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="c1f98-113">Поздравляем! Вы создали клиент Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c1f98-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="c1f98-114">Вы являетесь глобальным администратором клиента hello.</span><span class="sxs-lookup"><span data-stu-id="c1f98-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="c1f98-115">При необходимости можно добавить других глобальных администраторов.</span><span class="sxs-lookup"><span data-stu-id="c1f98-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="c1f98-116">tooswitch tooyour нового клиента, щелкните hello *управлять вашей новой связи клиента*.</span><span class="sxs-lookup"><span data-stu-id="c1f98-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Ссылка для управления новым клиентом](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="c1f98-118">Если вы планируете toouse клиента B2C для рабочего приложения, прочтите статью hello на [Масштабирование рабочей и предварительной версии B2C клиентов](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="c1f98-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="c1f98-119">Существуют известные проблемы при удалении существующей B2C клиента и создать его повторно с hello таким же именем домена.</span><span class="sxs-lookup"><span data-stu-id="c1f98-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="c1f98-120">Необходимо toocreate клиента B2C с именем другого домена.</span><span class="sxs-lookup"><span data-stu-id="c1f98-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="c1f98-121">Связи подписки tooyour клиента</span><span class="sxs-lookup"><span data-stu-id="c1f98-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="c1f98-122">Требуется toolink к Azure AD B2C клиента все функциональные возможности B2C tooenable tooyour подписки Azure и платить за сборам за использование.</span><span class="sxs-lookup"><span data-stu-id="c1f98-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="c1f98-123">лучше, ознакомьтесь с toolearn [в этой статье](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="c1f98-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="c1f98-124">Если не связать ваш tooyour клиента Azure AD B2C подписки Azure, заблокированы некоторые функциональные возможности, и вы увидите предупреждение («подписка, не связанный toothis B2C клиента или hello подписки должен внимания.») в параметрах hello B2C.</span><span class="sxs-lookup"><span data-stu-id="c1f98-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="c1f98-125">Важно выполнить этот шаг, прежде чем переводить приложения в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="c1f98-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="c1f98-126">Простой доступ toosettings</span><span class="sxs-lookup"><span data-stu-id="c1f98-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="c1f98-127">Можно также доступ к колонке hello, введя `Azure AD B2C` в **Найдите ресурсы** hello верхней части портала hello.</span><span class="sxs-lookup"><span data-stu-id="c1f98-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="c1f98-128">В списке результатов hello выберите **Azure AD B2C** tooaccess hello колонку параметров B2C.</span><span class="sxs-lookup"><span data-stu-id="c1f98-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1f98-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1f98-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1f98-130">Azure Active Directory B2C: регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="c1f98-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
