---
title: "Конечная точка v2.0 Active Directory aaaAzure | Документы Microsoft"
description: "Приложения toobuilding введение учетной записи Майкрософт и Azure Active Directory входа в систему."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="ce57a-103">Вход для пользователей учетных записей Майкрософт и Azure AD в одном приложении</span><span class="sxs-lookup"><span data-stu-id="ce57a-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="ce57a-104">В hello за разработчик приложения, которые хотели toosupport оба личные учетные записи Майкрософт и рабочих учетных записей из Azure Active Directory была необходимые toointegrate с двумя отдельными системами.</span><span class="sxs-lookup"><span data-stu-id="ce57a-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="ce57a-105">Hello **конечная точка Azure AD v2.0** предлагает новый вариант проверки подлинности API, позволяющая toosign в обоих типов учетных записей с помощью одной простой интеграции.</span><span class="sxs-lookup"><span data-stu-id="ce57a-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="ce57a-106">Приложения, использующие конечной точки v2.0 hello также может использовать API-интерфейс REST из hello [Microsoft Graph](https://graph.microsoft.io) с помощью любого типа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ce57a-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ce57a-107">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="ce57a-107">Getting Started</span></span>
<span data-ttu-id="ce57a-108">Выберите избранные платформу из hello после списка toobuild приложения с помощью наших библиотеки с открытым исходным кодом и платформ.</span><span class="sxs-lookup"><span data-stu-id="ce57a-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="ce57a-109">Кроме того можно использовать наши toosend документации протокола OAuth 2.0 и OpenID Connect & принимают сообщения протокола напрямую без использования библиотеки проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ce57a-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="ce57a-110">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="ce57a-110">What's New</span></span>
<span data-ttu-id="ce57a-111">здесь сведения Hello будет полезен для понимания, что такое & что невозможна с конечной точкой v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="ce57a-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="ce57a-112">Дополнительные сведения о hello [типов приложений, можно построить с конечной точкой v2.0 hello](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="ce57a-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="ce57a-113">Понимать hello [ограничения, ограничения и ограничения](active-directory-v2-limitations.md) с конечной точкой v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="ce57a-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="ce57a-114">См. в этом обзоре видео для конечной точки v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="ce57a-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="ce57a-115">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="ce57a-115">Reference</span></span>
<span data-ttu-id="ce57a-116">Эти ссылки будут использоваться для изучения платформы hello подробно:</span><span class="sxs-lookup"><span data-stu-id="ce57a-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="ce57a-117">Справочник по протоколу версии 2.0</span><span class="sxs-lookup"><span data-stu-id="ce57a-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="ce57a-118">Справочник по маркерам версии 2.0</span><span class="sxs-lookup"><span data-stu-id="ce57a-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="ce57a-119">Справочник по библиотеке версии 2.0</span><span class="sxs-lookup"><span data-stu-id="ce57a-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="ce57a-120">Области и согласие в конечной точке v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="ce57a-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="ce57a-121">Hello Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ce57a-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="ce57a-122">Справка и поддержка</span><span class="sxs-lookup"><span data-stu-id="ce57a-122">Help & Support</span></span>
<span data-ttu-id="ce57a-123">Это hello наиболее местах tooget справки по разработке в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ce57a-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="ce57a-124">Stack Overflow`azure-active-directory` и `adal`теги</span><span class="sxs-lookup"><span data-stu-id="ce57a-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="ce57a-125">Отзывы об Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce57a-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="ce57a-126">Если требуется только toosign в работу и учебную учетные записи из Azure Active Directory, следует начать с нашей [руководство разработчика Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ce57a-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="ce57a-127">Конечная точка v2.0 Hello предназначен для использования разработчиками, которые явно требуется toosign в личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ce57a-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

