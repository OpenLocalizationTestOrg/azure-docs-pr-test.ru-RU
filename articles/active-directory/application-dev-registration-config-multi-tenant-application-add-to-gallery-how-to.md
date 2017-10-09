---
title: "aaaHow tooadd коллекции приложений Azure AD toohello многопользовательского приложения | Документы Microsoft"
description: "Объясняет, как можно получить список пользовательских развитых мультитенантного приложения в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 2dc6e0d783835d2639a7e6dda172110ee860a977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-multi-tenant-application-toohello-azure-ad-application-gallery"></a><span data-ttu-id="38265-103">Как tooadd коллекции приложений Azure AD toohello многопользовательского приложения</span><span class="sxs-lookup"><span data-stu-id="38265-103">How tooadd a multi-tenant application toohello Azure AD application gallery</span></span>

## <a name="what-is-hello-azure-ad-application-gallery"></a><span data-ttu-id="38265-104">Что такое hello коллекции приложений Azure AD?</span><span class="sxs-lookup"><span data-stu-id="38265-104">What is hello Azure AD Application Gallery?</span></span>

<span data-ttu-id="38265-105">Коллекция приложений Hello Azure AD является хорошим способом tooget приложение перед все hello миллионам влияние hello toobroaden клиентов Azure Active Directory и достичь приложения hello рынке.</span><span class="sxs-lookup"><span data-stu-id="38265-105">hello Azure AD Application Gallery is a great way tooget your application in front of all hello millions of Azure Active Directory customers toobroaden hello impact and reach of your application in hello marketplace.</span></span> <span data-ttu-id="38265-106">Hello шаги, описанные ниже объясняется, как можно получить список приложения в коллекции приложений Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="38265-106">hello below steps explain how you can list your application in hello Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="38265-107">Если приложение поддерживает SAML или OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="38265-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="38265-108">Если мультитенантное приложение хотелось бы toolist в hello коллекции приложений Azure AD, сначала необходимо убедиться, что приложение поддерживает один из следующих технологий-hello.</span><span class="sxs-lookup"><span data-stu-id="38265-108">If you have a multi-tenant application you'd like toolist in hello Azure AD Application Gallery, you must first make sure that your application supports one of hello following single sign-on technologies:</span></span>

1. <span data-ttu-id="38265-109">**OpenID Connect** — прямая интеграция с Azure AD, используя для проверки подлинности OpenID Connect и hello согласия Azure AD API для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="38265-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="38265-110">Если приложение не поддерживает SAML только начинает интеграцию, это можно сделать hello. рекомендуется режим.</span><span class="sxs-lookup"><span data-stu-id="38265-110">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
2. <span data-ttu-id="38265-111">**SAML** – приложение уже имеет hello возможность tooconfigure сторонних поставщиков с помощью протокола SAML hello.</span><span class="sxs-lookup"><span data-stu-id="38265-111">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="38265-112">Если приложение поддерживает один из следующих режимов единого входа и хотелось бы toolist ваше мультитенантное приложение hello коллекции приложений Azure AD можно выполнить действия hello в документе hello ниже.</span><span class="sxs-lookup"><span data-stu-id="38265-112">If your application supports one of these single sign-on modes and you'd like toolist your multi-tenant application in hello Azure AD Application Gallery, you can follow hello steps in hello document below.</span></span> <span data-ttu-id="38265-113">быстро начать tooget отправить сообщение электронной почты слишком**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="38265-113">tooget started quickly send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="38265-114">Если приложение не поддерживает SAML или OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="38265-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="38265-115">Даже если приложение не поддерживает один из этих режимов, мы по-прежнему можем интегрировать его в свою коллекцию, применив технологию единого входа по паролю.</span><span class="sxs-lookup"><span data-stu-id="38265-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="38265-116">Если вы хотите tooexplore этого параметра можно отправить сообщение электронной почты слишком**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="38265-116">If you'd like tooexplore this option, you can send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38265-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38265-117">Next steps</span></span>
[<span data-ttu-id="38265-118">Как toolist приложения в коллекции приложений Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="38265-118">How toolist your application in hello Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
