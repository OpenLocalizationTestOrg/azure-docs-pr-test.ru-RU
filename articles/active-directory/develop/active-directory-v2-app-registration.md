---
title: "Регистрация приложения в конечной точке Azure AD версии 2.0 с помощью портала | Документация Майкрософт"
description: "Как зарегистрировать приложение в корпорации Майкрософт, чтобы использовать вход и доступ к службам Майкрософт с помощью конечной точки версии 2.0."
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
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="284b0-103">Как зарегистрировать приложение с использованием конечной точки версии 2.0</span><span class="sxs-lookup"><span data-stu-id="284b0-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="284b0-104">Для создания приложения, которое поддерживает единый вход MSA b Azure AD вход, сначала необходимо зарегистрировать приложение в Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="284b0-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="284b0-105">На данном этапе вы не сможете использовать любые существующие приложения с Azure AD или учетными записями Майкрософт, необходимо будет создать новое приложение.</span><span class="sxs-lookup"><span data-stu-id="284b0-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="284b0-106">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="284b0-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="284b0-107">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="284b0-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="284b0-108">Посетите портал регистрации приложения Майкрософт</span><span class="sxs-lookup"><span data-stu-id="284b0-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="284b0-109">Для начала перейдите на страницу [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="284b0-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="284b0-110">Это новый портал регистрации приложений, где вы можете управлять своими приложениями Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="284b0-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="284b0-111">Войти с помощью личной, рабочей или учебной учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="284b0-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="284b0-112">Если у вас нет учетной записи, зарегистрируйтесь для получения личной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="284b0-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="284b0-113">Вперед, это не займет много времени.</span><span class="sxs-lookup"><span data-stu-id="284b0-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="284b0-114">Готово?</span><span class="sxs-lookup"><span data-stu-id="284b0-114">Done?</span></span> <span data-ttu-id="284b0-115">Теперь вы должны увидеть список своих приложений Майкрософт, который, вероятно, пуст.</span><span class="sxs-lookup"><span data-stu-id="284b0-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="284b0-116">Изменим это.</span><span class="sxs-lookup"><span data-stu-id="284b0-116">Let's change that.</span></span>

<span data-ttu-id="284b0-117">Щелкните **Добавить приложение**и присвойте приложению имя.</span><span class="sxs-lookup"><span data-stu-id="284b0-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="284b0-118">Портал назначит приложению глобальный уникальный идентификатор, который вы используете в коде в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="284b0-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="284b0-119">Если приложение содержит серверный компонент, которому требуются маркеры доступа для вызова интерфейсов API (например, Office, Azure или собственного веб-API), вам необходимо также создать **секрет приложения** .</span><span class="sxs-lookup"><span data-stu-id="284b0-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="284b0-120">Добавьте платформы, которые будет использовать приложение.</span><span class="sxs-lookup"><span data-stu-id="284b0-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="284b0-121">Для веб-приложений укажите **универсальный код ресурса (URI) перенаправления** для отправки сообщений о входе.</span><span class="sxs-lookup"><span data-stu-id="284b0-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="284b0-122">Для мобильных приложений скопируйте автоматически созданный для вас универсальный код ресурса (URI) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="284b0-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="284b0-123">При необходимости можно настроить внешний вид страницы входа в разделе "Профиль".</span><span class="sxs-lookup"><span data-stu-id="284b0-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="284b0-124">Нажмите кнопку **Сохранить** перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="284b0-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="284b0-125">При создании приложения с помощью [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) оно будет зарегистрировано в главном клиенте учетной записи, которая используется для входа на портал.</span><span class="sxs-lookup"><span data-stu-id="284b0-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="284b0-126">Это означает, что нельзя зарегистрировать приложение в клиенте Azure AD с помощью личной учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="284b0-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="284b0-127">Если требуется явно зарегистрировать приложение в конкретном клиенте, войдите с помощью учетной записи, первоначально созданной в этом клиенте.</span><span class="sxs-lookup"><span data-stu-id="284b0-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="284b0-128">Создание приложения быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="284b0-128">Build a quick start app</span></span>
<span data-ttu-id="284b0-129">Теперь, когда у вас есть приложение Майкрософт, вы можете изучить один из кратких учебников по версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="284b0-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="284b0-130">Вот несколько рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="284b0-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

