---
title: "Смена ключей подписывания Azure AD | Документация Майкрософт"
description: "В этой статье рассматриваются рекомендации по смене ключей подписывания для Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="9aed1-103">Смена ключей подписывания Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9aed1-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="9aed1-104">В этом разделе представлены основные сведения об открытых ключах, которые используются в Azure Active Directory (Azure AD) для подписывания маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="9aed1-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="9aed1-105">Важно отметить, что эти ключи периодически меняются и в случае чрезвычайной ситуации могут быть изменены немедленно.</span><span class="sxs-lookup"><span data-stu-id="9aed1-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9aed1-106">Все приложения, использующие Azure AD, должны обладать механизмом программной смены ключей или предоставлять возможность периодически запускать процесс смены ключей вручную.</span><span class="sxs-lookup"><span data-stu-id="9aed1-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="9aed1-107">Здесь вы узнаете принцип действия ключей, а также то, как оценить степень влияния их смены на приложение и как обновить приложение или настроить периодический запуск процесса смены ключей в ручном режиме, чтобы приложение могло обрабатывать этот процесс.</span><span class="sxs-lookup"><span data-stu-id="9aed1-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="9aed1-108">Общие сведения о ключах подписывания в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9aed1-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="9aed1-109">Azure AD использует шифрование с открытым ключом на основе отраслевых стандартов, чтобы устанавливать доверительные отношения с приложениями, использующими этот каталог.</span><span class="sxs-lookup"><span data-stu-id="9aed1-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="9aed1-110">В частности, это происходит следующим образом. Azure AD использует ключ подписывания, состоящий из пары открытого и закрытого ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="9aed1-111">Когда пользователь входит в приложение, использующее Azure AD для проверки подлинности, Azure AD создает токен безопасности, который содержит сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="9aed1-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="9aed1-112">Azure AD подписывает этот токен, используя закрытый ключ, прежде чем отправить токен приложению.</span><span class="sxs-lookup"><span data-stu-id="9aed1-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="9aed1-113">Чтобы убедиться, что маркер является допустимым и получен от Azure AD, приложение должно проверить его подпись с помощью открытого ключа, предоставленного Azure AD, который содержится в [документе обнаружения OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) или [документе метаданных федерации SAML/WS-Fed](active-directory-federation-metadata.md) клиента.</span><span class="sxs-lookup"><span data-stu-id="9aed1-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="9aed1-114">В целях безопасности ключи подписывания Azure AD периодически меняются и в случае чрезвычайной ситуации могут быть изменены немедленно.</span><span class="sxs-lookup"><span data-stu-id="9aed1-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="9aed1-115">Любое приложение, которое интегрируется с Azure AD, должно быть подготовлено к обработке смены ключа независимо от того, насколько часто происходит такая смена.</span><span class="sxs-lookup"><span data-stu-id="9aed1-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="9aed1-116">Если такая логика не предусмотрена и приложение попытается использовать ключ с истекшим сроком действия, чтобы проверить подпись токена, произойдет сбой запроса на вход.</span><span class="sxs-lookup"><span data-stu-id="9aed1-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="9aed1-117">В документе метаданных федерации и документе обнаружения OpenID Connect всегда существует несколько допустимых ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="9aed1-118">Следует подготовить приложение к использованию любого из ключей, указанных в документе, так как один ключ может быть сменен раньше, другой может оказаться его заменой и т. д.</span><span class="sxs-lookup"><span data-stu-id="9aed1-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="9aed1-119">Как оценить степень влияния смены ключей на приложение</span><span class="sxs-lookup"><span data-stu-id="9aed1-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="9aed1-120">Обработка смены ключей в приложении зависит от нескольких переменных, например от типа приложения или используемых протокола идентификации и библиотеки.</span><span class="sxs-lookup"><span data-stu-id="9aed1-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="9aed1-121">В приведенных ниже разделах рассматривается, влияет ли смена ключей на самые распространенные типы приложений, а также содержатся рекомендации по обновлению приложения для поддержки автоматической смены ключей и обновлении ключей вручную.</span><span class="sxs-lookup"><span data-stu-id="9aed1-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="9aed1-122">Собственные клиентские приложения, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="9aed1-123">Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="9aed1-124">Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9aed1-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="9aed1-125">Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed</span><span class="sxs-lookup"><span data-stu-id="9aed1-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="9aed1-126">Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect .NET Core</span><span class="sxs-lookup"><span data-stu-id="9aed1-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="9aed1-127">Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="9aed1-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="9aed1-128">Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9aed1-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="9aed1-129">Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9aed1-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="9aed1-130">Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9aed1-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="9aed1-131">Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9aed1-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="9aed1-132">Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008, 2010 или Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="9aed1-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="9aed1-133">Веб-приложения и интерфейсы API, защищающие ресурсы с помощью других библиотек или ручного внедрения поддерживаемых протоколов</span><span class="sxs-lookup"><span data-stu-id="9aed1-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="9aed1-134">Это руководство **не** применимо к:</span><span class="sxs-lookup"><span data-stu-id="9aed1-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="9aed1-135">приложениям, добавленным из коллекции приложений Azure AD (включая пользовательские), так как для них предусмотрены отдельные правила в отношении ключей подписывания</span><span class="sxs-lookup"><span data-stu-id="9aed1-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> <span data-ttu-id="9aed1-136">[Дополнительные сведения](../active-directory-sso-certs.md).</span><span class="sxs-lookup"><span data-stu-id="9aed1-136">[More information.](../active-directory-sso-certs.md)</span></span>
* <span data-ttu-id="9aed1-137">локальным приложениям, опубликованным через прокси приложения, так как им не требуются ключи подписывания.</span><span class="sxs-lookup"><span data-stu-id="9aed1-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="9aed1-138"><a name="nativeclient"></a>Собственные клиентские приложения, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="9aed1-139">Как правило, приложения, только осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9aed1-140">(например, Microsoft Graph, KeyVault, API Outlook и другие Microsoft API), получают маркеры и передают их владельцу ресурса.</span><span class="sxs-lookup"><span data-stu-id="9aed1-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="9aed1-141">Так как они не защищают ресурсы, они не проверяют токен, а вместе с тем и его подпись.</span><span class="sxs-lookup"><span data-stu-id="9aed1-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="9aed1-142">Собственные клиентские приложения, будь то классические или мобильные, попадают в эту категорию. Поэтому смена ключей не влияет на этот тип приложений.</span><span class="sxs-lookup"><span data-stu-id="9aed1-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="9aed1-143"><a name="webclient"></a>Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="9aed1-144">Как правило, приложения, только осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="9aed1-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="9aed1-145">(например, Microsoft Graph, KeyVault, API Outlook и другие Microsoft API), получают маркеры и передают их владельцу ресурса.</span><span class="sxs-lookup"><span data-stu-id="9aed1-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="9aed1-146">Так как они не защищают ресурсы, они не проверяют токен, а вместе с тем и его подпись.</span><span class="sxs-lookup"><span data-stu-id="9aed1-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="9aed1-147">Веб-приложения и интерфейсы API, использующие поток только для приложений (учетные данные или сертификат клиента), попадают в эту категорию. Поэтому смена ключей не влияет на этот тип приложений.</span><span class="sxs-lookup"><span data-stu-id="9aed1-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="9aed1-148"><a name="appservices"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9aed1-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="9aed1-149">В функциях проверки подлинности и авторизации (EasyAuth) служб приложений Azure уже предусмотрена логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="9aed1-150"><a name="owin"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed</span><span class="sxs-lookup"><span data-stu-id="9aed1-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="9aed1-151">Если в приложении используется ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed, в нем уже предусмотрена логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="9aed1-152">Чтобы проверить это, нужно поискать один из следующих фрагментов кода в файле Startup.cs или Startup.Auth.cs приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="9aed1-153"><a name="owincore"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect.NET Core</span><span class="sxs-lookup"><span data-stu-id="9aed1-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="9aed1-154">Если в приложении используется ПО промежуточного слоя для аутентификации на основе токена носителя JWT или .NET Core OWIN OpenID Connect, в нем уже предусмотрена логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="9aed1-155">Чтобы проверить это, нужно поискать один из следующих фрагментов кода в файле Startup.cs или Startup.Auth.cs приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="9aed1-156"><a name="passport"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="9aed1-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="9aed1-157">Если в приложении используется модуль Node.js passport-ad, в нем уже предусмотрена логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="9aed1-158">Это можно проверить, выполнив поиск следующего фрагмента кода в файле app.js приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="9aed1-159"><a name="vs2015"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9aed1-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="9aed1-160">Если приложение создано в Visual Studio 2015 или Visual Studio 2017 с использованием шаблона веб-приложения и в меню **Изменить способ проверки подлинности** выбран пункт **Рабочие или учебные учетные записи**, в приложении уже есть необходимая логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="9aed1-161">Эта логика, внедренная в ПО промежуточного слоя OWIN OpenID Connect, извлекает ключи из документа обнаружения OpenID Connect, кэширует их и периодически обновляет.</span><span class="sxs-lookup"><span data-stu-id="9aed1-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="9aed1-162">Если проверка подлинности добавлена в решение вручную, в приложении может отсутствовать необходимая логика смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="9aed1-163">Ее понадобится написать самостоятельно или выполнить действия, описанные в разделе [Веб-приложения и интерфейсы API, использующие другие библиотеки или ручное внедрение поддерживаемых протоколов](#other).</span><span class="sxs-lookup"><span data-stu-id="9aed1-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="9aed1-164"><a name="vs2013"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9aed1-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9aed1-165">Если приложение создано в Visual Studio 2013 с использованием шаблона веб-приложения и в меню **Изменить способ проверки подлинности** выбран пункт **Учетные записи организации**, в приложении уже есть необходимая логика для обработки автоматической смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="9aed1-166">Логика хранит уникальный идентификатор организации и сведения о ключе подписывания в двух таблицах базы данных, связанных с проектом.</span><span class="sxs-lookup"><span data-stu-id="9aed1-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="9aed1-167">Строку подключения для базы данных можно найти в файле Web.config проекта.</span><span class="sxs-lookup"><span data-stu-id="9aed1-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="9aed1-168">Если проверка подлинности добавлена в решение вручную, в приложении может отсутствовать необходимая логика смены ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="9aed1-169">Ее понадобится написать самостоятельно или выполнить действия, описанные в разделе [Веб-приложения и интерфейсы API, использующие другие библиотеки или ручное внедрение поддерживаемых протоколов](#other).</span><span class="sxs-lookup"><span data-stu-id="9aed1-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="9aed1-170">Далее представлены шаги, которые помогут проверить правильность работы логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="9aed1-171">В Visual Studio 2013 откройте решение и в окне справа выберите вкладку **Обозреватель серверов** .</span><span class="sxs-lookup"><span data-stu-id="9aed1-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="9aed1-172">Разверните узлы **Подключения данных**, **DefaultConnection**, а затем — **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="9aed1-173">Найдите и щелкните правой кнопкой мыши таблицу **IssuingAuthorityKeys**, а затем выберите **Показать данные таблицы**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="9aed1-174">В таблице **IssuingAuthorityKeys** будет по крайней мере одна строка, соответствующая значению отпечатка для ключа.</span><span class="sxs-lookup"><span data-stu-id="9aed1-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="9aed1-175">Удалите все строки в таблице.</span><span class="sxs-lookup"><span data-stu-id="9aed1-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="9aed1-176">Щелкните правой кнопкой мыши таблицу **Tenants** и выберите **Показать данные таблицы**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="9aed1-177">В таблице **Клиенты** будет по крайней мере одна строка, соответствующая уникальному идентификатору клиента каталога.</span><span class="sxs-lookup"><span data-stu-id="9aed1-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="9aed1-178">Удалите все строки в таблице.</span><span class="sxs-lookup"><span data-stu-id="9aed1-178">Delete any rows in the table.</span></span> <span data-ttu-id="9aed1-179">Если не удалить строки в таблицах **Tenants** и **IssuingAuthorityKeys**, то при выполнении произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="9aed1-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="9aed1-180">Создайте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="9aed1-180">Build and run the application.</span></span> <span data-ttu-id="9aed1-181">Войдя в учетную запись, можно остановить работу приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="9aed1-182">Вернитесь в **обозреватель сервера** и просмотрите значения в таблицах **IssuingAuthorityKeys** и **Tenants**.</span><span class="sxs-lookup"><span data-stu-id="9aed1-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="9aed1-183">Как можно заметить, в них автоматически добавлены соответствующие сведения из документа метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="9aed1-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="9aed1-184"><a name="vs2013"></a>Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9aed1-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="9aed1-185">Если приложение веб-API создано в Visual Studio 2013 с использованием шаблона веб-API и в меню **Изменить способ проверки подлинности** выбран пункт **Учетные записи организации**, в нем уже есть необходимая логика.</span><span class="sxs-lookup"><span data-stu-id="9aed1-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="9aed1-186">Если проверка подлинности настроена вручную, следуйте указаниям ниже, чтобы узнать, как настроить веб-API для автоматического обновления сведений о ключах.</span><span class="sxs-lookup"><span data-stu-id="9aed1-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="9aed1-187">В следующем фрагменте кода показано, как получить последние ключи из документа метаданных федерации, а затем использовать [обработчик маркеров JWT](https://msdn.microsoft.com/library/dn205065.aspx) для проверки маркера.</span><span class="sxs-lookup"><span data-stu-id="9aed1-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="9aed1-188">Во фрагменте кода предполагается, что для сохранения ключа, с помощью которого будет выполняться последующая проверка токенов из Azure AD, будет использоваться собственный механизм кэширования, несмотря на место его хранения (база данных, файл конфигурации или другое расположение).</span><span class="sxs-lookup"><span data-stu-id="9aed1-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="9aed1-189"><a name="vs2012"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9aed1-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="9aed1-190">Если приложение создано в Visual Studio 2012, вероятно, оно настроено с помощью средства Identity and Access Tool.</span><span class="sxs-lookup"><span data-stu-id="9aed1-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="9aed1-191">Кроме того, возможно, используется [проверка реестра имен поставщиков](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="9aed1-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="9aed1-192">VINR отвечает за обслуживание сведений о доверенных поставщиках удостоверений (Azure AD) и ключах, используемых для проверки токенов, которые выдали эти поставщики.</span><span class="sxs-lookup"><span data-stu-id="9aed1-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="9aed1-193">VINR также упрощает автоматическое обновление сведений о ключах, хранящихся в файле Web.config. Для этого скачивается последний документ метаданных федерации, связанный с каталогом, проверяется,не устарела ли конфигурация по сравнению с этим документом, и приложение обновляется для использования нового ключа при необходимости.</span><span class="sxs-lookup"><span data-stu-id="9aed1-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="9aed1-194">Если приложение создано с использованием любого из примеров кода или документации с пошаговыми инструкциями, предоставленных корпорацией Майкрософт, логика смены ключей уже добавлена в проект.</span><span class="sxs-lookup"><span data-stu-id="9aed1-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="9aed1-195">Вы заметите, что код ниже уже есть в проекте.</span><span class="sxs-lookup"><span data-stu-id="9aed1-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="9aed1-196">Если в приложении нет этой логики, выполните следующие шаги, чтобы добавить ее и убедиться в правильности ее работы.</span><span class="sxs-lookup"><span data-stu-id="9aed1-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="9aed1-197">В **обозревателе решений** добавьте ссылку на сборку **System.IdentityModel** для соответствующего проекта.</span><span class="sxs-lookup"><span data-stu-id="9aed1-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="9aed1-198">Откройте файл **Global.asax.cs** и добавьте следующие директивы using:</span><span class="sxs-lookup"><span data-stu-id="9aed1-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="9aed1-199">Добавьте в файл **Global.asax.cs** следующий метод:</span><span class="sxs-lookup"><span data-stu-id="9aed1-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="9aed1-200">Вызовите метод **RefreshValidationSettings()** в методе **Application_Start()** в файле **Global.asax.cs**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9aed1-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="9aed1-201">После выполнения этих шагов файл Web.config приложения обновится с использованием последних сведений документа метаданных федерации, в том числе последних ключей.</span><span class="sxs-lookup"><span data-stu-id="9aed1-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="9aed1-202">Это обновление будет выполняться при каждом перезапуске пула приложений в IIS. По умолчанию в IIS настроен перезапуск приложений через каждые 29 часов.</span><span class="sxs-lookup"><span data-stu-id="9aed1-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="9aed1-203">Выполните следующие шаги, чтобы убедиться, что логика смены ключей работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="9aed1-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="9aed1-204">Убедившись, что приложение использует код, приведенный выше, откройте файл **Web.config**, перейдите к блоку **<issuerNameRegistry>** и найдите следующие несколько строк.</span><span class="sxs-lookup"><span data-stu-id="9aed1-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="9aed1-205">В таблице **<add thumbprint=””>** измените значение отпечатка, заменив любой из знаков другим знаком.</span><span class="sxs-lookup"><span data-stu-id="9aed1-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="9aed1-206">Сохраните файл **Web.config** .</span><span class="sxs-lookup"><span data-stu-id="9aed1-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="9aed1-207">Выполните сборку приложения и запустите его.</span><span class="sxs-lookup"><span data-stu-id="9aed1-207">Build the application, and then run it.</span></span> <span data-ttu-id="9aed1-208">Если у вас получилось войти, приложение успешно обновляет ключ, скачивая необходимые данные из документа метаданных федерации каталога.</span><span class="sxs-lookup"><span data-stu-id="9aed1-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="9aed1-209">Если при входе возникают проблемы, убедитесь, что в приложение внесены правильные изменения. Для этого прочитайте статью [Добавление единого входа в веб-приложение с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) или скачайте и проверьте пример кода в разделе [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b) (Мультитенантное облачное приложение для Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9aed1-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="9aed1-210"><a name="vs2010"></a>Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008 или 2010 и Windows Identity Foundation v1.0 для .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="9aed1-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="9aed1-211">Если приложение создано на платформе Windows Identity Foundation v1.0, в нем не предусмотрен механизм автоматического обновления конфигурации для использования нового ключа.</span><span class="sxs-lookup"><span data-stu-id="9aed1-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="9aed1-212">*проще* всего в пакете SDK для Windows Identity Foundation, с помощью которого можно получить последний документ метаданных и обновить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9aed1-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="9aed1-213">Обновите платформу приложения до версии .NET 4.5, которая содержит новейшую версию Windows Identity Foundation, расположенную в пространстве имен System.</span><span class="sxs-lookup"><span data-stu-id="9aed1-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="9aed1-214">Затем можно использовать [проверку реестра имен поставщиков](https://msdn.microsoft.com/library/dn205067.aspx) , чтобы автоматически обновить конфигурацию приложения.</span><span class="sxs-lookup"><span data-stu-id="9aed1-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="9aed1-215">Запустите процесс смены ключей в ручном режиме согласно инструкциям, приведенным в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="9aed1-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="9aed1-216">Ниже приведены инструкции по использованию FedUtil для обновления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9aed1-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="9aed1-217">Убедитесь, что на компьютере для разработки для Visual Studio 2008 или 2010 установлен пакет SDK для Windows Identity Foundation v1.0.</span><span class="sxs-lookup"><span data-stu-id="9aed1-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="9aed1-218">Если этот пакет не установлен, его можно [скачать отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=4451).</span><span class="sxs-lookup"><span data-stu-id="9aed1-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="9aed1-219">В Visual Studio откройте решение, щелкните соответствующий проект правой кнопкой мыши и выберите пункт **Update federation metadata**(Обновить метаданные федерации).</span><span class="sxs-lookup"><span data-stu-id="9aed1-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="9aed1-220">Если этот параметр недоступен, средство FedUtil и/или пакет SDK для Windows Identity Foundation v1.0 не установлен.</span><span class="sxs-lookup"><span data-stu-id="9aed1-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="9aed1-221">В командной строке выберите **Обновить** , чтобы начать обновление метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="9aed1-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="9aed1-222">При наличии доступа к среде сервера, где размещено приложение, можно использовать [планировщик автоматического обновления метаданных](https://msdn.microsoft.com/library/ee517272.aspx)средства FedUtil.</span><span class="sxs-lookup"><span data-stu-id="9aed1-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="9aed1-223">Нажмите кнопку **Готово** , чтобы завершить обновление.</span><span class="sxs-lookup"><span data-stu-id="9aed1-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="9aed1-224"><a name="other"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с помощью других библиотек или ручного внедрения поддерживаемых протоколов</span><span class="sxs-lookup"><span data-stu-id="9aed1-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="9aed1-225">Если используется другая библиотека или вручную внедрены поддерживаемые протоколы, их необходимо проверить, чтобы убедиться, что ключ извлекается из документа обнаружения OpenID Connect или документа метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="9aed1-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="9aed1-226">Для этого необходимо проверить в коде приложения или коде библиотеки наличие вызовов документа обнаружения OpenID Connect или документа метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="9aed1-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="9aed1-227">Если ключ хранится в другом месте или жестко закодирован в приложении, можно вручную извлечь и обновить его, выполнив смену ключа вручную согласно инструкциям, приведенным в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="9aed1-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="9aed1-228">**настоятельно рекомендуется настроить поддержку автоматической смены ключей в приложении** , используя методы, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9aed1-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="9aed1-229">Тестирование приложения для оценки степени влияния</span><span class="sxs-lookup"><span data-stu-id="9aed1-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="9aed1-230">Чтобы проверить, поддерживается ли автоматическая смена ключей в приложении, необходимо скачать скрипты и выполнить инструкции, описанные [в этом репозитории GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="9aed1-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="9aed1-231">Настройка процедуры смены ключей в ручном режиме, если приложение не поддерживает автоматическую смену ключей</span><span class="sxs-lookup"><span data-stu-id="9aed1-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="9aed1-232">Если приложение **не** поддерживает автоматическую смену ключей, необходимо создать процесс, который будет периодически отслеживать ключи подписывания Azure AD и выполнять смену ключей в ручном режиме соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="9aed1-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="9aed1-233">[Этот репозиторий GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) содержит скрипты и инструкции о том, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="9aed1-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

