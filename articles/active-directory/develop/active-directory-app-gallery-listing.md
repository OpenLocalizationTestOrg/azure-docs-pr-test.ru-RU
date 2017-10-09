---
title: "aaaListing приложения в коллекции приложений Azure Active Directory hello"
description: "Как приложение с поддержкой единого входа в toolist hello коллекция Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="1c6ed-103">Перечисление приложения в коллекции приложений Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="1c6ed-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="1c6ed-104">приложение, поддерживающее единый вход в Azure Active Directory в hello toolist [коллекции Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), приложение hello сначала должно tooimplement один hello следующие режимы интеграции:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="1c6ed-105">**OpenID Connect** — прямая интеграция с Azure AD, используя для проверки подлинности OpenID Connect и hello согласия Azure AD API для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="1c6ed-106">Если приложение не поддерживает SAML только начинает интеграцию, это можно сделать hello. рекомендуется режим.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="1c6ed-107">**SAML** – приложение уже имеет hello возможность tooconfigure сторонних поставщиков с помощью протокола SAML hello.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="1c6ed-108">Список требований для каждого режима приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="1c6ed-109">Интеграция OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="1c6ed-109">OpenID Connect Integration</span></span>
<span data-ttu-id="1c6ed-110">toointegrate приложения в Azure AD, следующие hello [инструкции разработчика](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="1c6ed-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="1c6ed-111">Затем завершить следующих вопросов hello и отправить toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="1c6ed-112">Укажите учетные данные тестового клиента или учетную запись с приложения, которые могут использоваться hello интеграция hello tootest команды Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="1c6ed-113">Содержат инструкции как команды hello Azure AD можно вход и подключиться экземпляр приложения tooyour Azure AD с помощью hello [инфраструктура согласия Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="1c6ed-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="1c6ed-114">Укажите любые дополнительные действия, необходимые для hello Azure AD команды tootest единого входа с приложением.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="1c6ed-115">Укажите информацию hello ниже:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-115">Provide hello info below:</span></span>

> <span data-ttu-id="1c6ed-116">Название организации:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-116">Company Name:</span></span>
> 
> <span data-ttu-id="1c6ed-117">Веб-сайт компании:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-117">Company Website:</span></span>
> 
> <span data-ttu-id="1c6ed-118">Имя приложения:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-118">Application Name:</span></span>
> 
> <span data-ttu-id="1c6ed-119">Описание приложения (не более 200 символов):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="1c6ed-120">Веб-сайт приложения (информационный):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="1c6ed-121">Веб-сайт технической поддержки приложений или контактные сведения:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="1c6ed-122">Идентификатор для приложения hello, как показано в сведения о приложении hello https://portal.azure.com:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="1c6ed-123">URL-адрес регистрации приложения, куда toosign для клиентов и/или приобрести приложения hello:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="1c6ed-124">Выберите категории toothree для вашей toobe приложения, указанные в списке (для доступных категорий см. hello Azure Active Directory Marketplace):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="1c6ed-125">Приложите мелкий значок приложения (PNG-файл, 45 x 45 пикселей, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="1c6ed-126">Приложите крупный значок приложения (PNG-файл, 215 x 215 пикселей, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="1c6ed-127">Приложите логотип приложения (PNG-файл, 150 x 122 пикселя, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="1c6ed-128">Интеграция SAML</span><span class="sxs-lookup"><span data-stu-id="1c6ed-128">SAML Integration</span></span>
<span data-ttu-id="1c6ed-129">Любое приложение, которое поддерживает SAML 2.0 можно интегрировать непосредственно с помощью клиента Azure AD [tooadd эти инструкции прикладной](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1c6ed-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="1c6ed-130">После проверки работы вашей интеграция приложений с Azure AD, отправка слишком следующую информацию hello<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="1c6ed-131">Укажите учетные данные тестового клиента или учетную запись с приложения, которые могут использоваться hello интеграция hello tootest команды Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="1c6ed-132">Указать hello SAML URL-адрес входа, URL-адрес издателя (идентификатор сущности), и URL-адрес ответа (службы обработчика утверждений) значения для вашего приложения, как описано [здесь](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1c6ed-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="1c6ed-133">Если вы обычно предоставляете эти значения как часть файла метаданных SAML, отправьте и его.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="1c6ed-134">Краткое описание того, как tooconfigure Azure AD как поставщика удостоверений в приложения с помощью SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="1c6ed-135">Если приложение поддерживает настройку Azure AD в качестве поставщика удостоверений на портале самообслуживания администратора, затем убедитесь hello учетные данные, приведенные выше включите tooset возможности hello этот вверх.</span><span class="sxs-lookup"><span data-stu-id="1c6ed-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="1c6ed-136">Укажите информацию hello ниже:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-136">Provide hello info below:</span></span>

> <span data-ttu-id="1c6ed-137">Название организации:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-137">Company Name:</span></span>
> 
> <span data-ttu-id="1c6ed-138">Веб-сайт компании:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-138">Company Website:</span></span>
> 
> <span data-ttu-id="1c6ed-139">Имя приложения:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-139">Application Name:</span></span>
> 
> <span data-ttu-id="1c6ed-140">Описание приложения (не более 200 символов):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="1c6ed-141">Веб-сайт приложения (информационный):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="1c6ed-142">Веб-сайт технической поддержки приложений или контактные сведения:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="1c6ed-143">URL-адрес регистрации приложения, куда toosign для клиентов и/или приобрести приложения hello:</span><span class="sxs-lookup"><span data-stu-id="1c6ed-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="1c6ed-144">Выберите категории toothree для вашего приложения toobe, перечисленных в разделе (доступных категорий см. в разделе hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="1c6ed-145">Приложите мелкий значок приложения (PNG-файл, 45 x 45 пикселей, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="1c6ed-146">Приложите крупный значок приложения (PNG-файл, 215 x 215 пикселей, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="1c6ed-147">Приложите логотип приложения (PNG-файл, 150 x 122 пикселя, сплошной цвет фона):</span><span class="sxs-lookup"><span data-stu-id="1c6ed-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

