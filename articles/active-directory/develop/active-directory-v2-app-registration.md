---
title: "приложения с конечной точкой v2.0 hello Azure AD, с помощью портала hello aaaRegister | Документы Microsoft"
description: "Как tooregister приложение с Microsoft для включения вход и доступ к Microsoft службы с помощью конечной точки v2.0 hello"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="ceba8-103">Как tooregister приложения с конечной точкой v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="ceba8-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="ceba8-104">приложение, которое принимает MSA & Azure AD toobuild входа в систему понадобится сначала tooregister приложение с Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ceba8-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="ceba8-105">В настоящее время не будет иметь возможности toouse любые существующие приложения с Azure AD может быть или MSA - потребуется toocreate марку новый.</span><span class="sxs-lookup"><span data-stu-id="ceba8-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="ceba8-106">Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="ceba8-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="ceba8-107">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ceba8-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="ceba8-108">Посетите портал регистрации приложения Microsoft hello</span><span class="sxs-lookup"><span data-stu-id="ceba8-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="ceba8-109">Начните сначала - перейдите слишком[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="ceba8-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="ceba8-110">Это новый портал регистрации приложений, где вы можете управлять своими приложениями Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ceba8-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="ceba8-111">Войти с помощью личной, рабочей или учебной учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ceba8-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="ceba8-112">Если у вас нет учетной записи, зарегистрируйтесь для получения личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ceba8-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="ceba8-113">Вперед, это не займет много времени.</span><span class="sxs-lookup"><span data-stu-id="ceba8-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="ceba8-114">Готово?</span><span class="sxs-lookup"><span data-stu-id="ceba8-114">Done?</span></span> <span data-ttu-id="ceba8-115">Теперь вы должны увидеть список своих приложений Майкрософт, который, вероятно, пуст.</span><span class="sxs-lookup"><span data-stu-id="ceba8-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="ceba8-116">Изменим это.</span><span class="sxs-lookup"><span data-stu-id="ceba8-116">Let's change that.</span></span>

<span data-ttu-id="ceba8-117">Щелкните **Добавить приложение**и присвойте приложению имя.</span><span class="sxs-lookup"><span data-stu-id="ceba8-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="ceba8-118">Hello портала будет назначать глобальный уникальный идентификатор приложения, которое будет использоваться в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="ceba8-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="ceba8-119">Если приложение включает в себя серверный компонент, требующий токены доступа для вызова API (подумать: Office, Azure или ваши собственные веб-API), вам потребуется toocreate **секрет приложения** таким же образом.</span><span class="sxs-lookup"><span data-stu-id="ceba8-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="ceba8-120">Затем добавьте hello платформы, используемые вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="ceba8-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="ceba8-121">Для веб-приложений укажите **универсальный код ресурса (URI) перенаправления** для отправки сообщений о входе.</span><span class="sxs-lookup"><span data-stu-id="ceba8-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="ceba8-122">Для мобильных приложений uri, автоматически создается перенаправления копирования вниз по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ceba8-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="ceba8-123">При необходимости можно настроить hello внешний вид и поведение в hello профиля страницы входа.</span><span class="sxs-lookup"><span data-stu-id="ceba8-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="ceba8-124">Убедитесь, что tooclick **Сохранить** прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="ceba8-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="ceba8-125">При создании приложения с помощью [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), в клиенте домашней hello hello учетной записи используется toosign hello портал будет зарегистрировано приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ceba8-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="ceba8-126">Это означает, что нельзя зарегистрировать приложение в клиенте Azure AD с помощью личной учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ceba8-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="ceba8-127">Если явно нужно tooregister приложения в конкретного клиента, войдите под учетной записью создан этого клиента.</span><span class="sxs-lookup"><span data-stu-id="ceba8-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="ceba8-128">Создание приложения быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="ceba8-128">Build a quick start app</span></span>
<span data-ttu-id="ceba8-129">Теперь, когда у вас есть приложение Майкрософт, вы можете изучить один из кратких учебников по версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="ceba8-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="ceba8-130">Вот несколько рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="ceba8-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

