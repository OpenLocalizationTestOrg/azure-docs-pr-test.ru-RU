---
title: "aaaSigning смене ключей в Azure AD | Документы Microsoft"
description: "В этой статье описывается hello подписи смены ключей советы и рекомендации для Azure Active Directory"
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
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="70664-103">Смена ключей подписывания Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70664-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="70664-104">В этом разделе рассматриваются необходимые tooknow о hello открытые ключи, которые используются в токенах безопасности toosign Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70664-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="70664-105">Это важные toonote, эти ключи меняются каждые периодически и в случае чрезвычайной ситуации удалось перезаписаны немедленно.</span><span class="sxs-lookup"><span data-stu-id="70664-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="70664-106">Все приложения, которые используют Azure AD необходимо процесс смены ключей hello дескриптора может tooprogrammatically или определение процесса периодической смены вручную.</span><span class="sxs-lookup"><span data-stu-id="70664-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="70664-107">Продолжить чтение toounderstand как ключи hello работают, как tooassess hello влияние приложения tooyour продолжения hello и как tooupdate приложения или установить периодической смены вручную смены ключей процесса toohandle при необходимости.</span><span class="sxs-lookup"><span data-stu-id="70664-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="70664-108">Общие сведения о ключах подписывания в Azure AD</span><span class="sxs-lookup"><span data-stu-id="70664-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="70664-109">Azure AD использует шифрование с открытым ключом лежит отраслевых стандартов tooestablish доверия между собой и hello приложений, которые его используют.</span><span class="sxs-lookup"><span data-stu-id="70664-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="70664-110">На практике это работает hello следующими способами: Azure AD использует ключ подписывания, состоящий из пары открытого и закрытого ключей.</span><span class="sxs-lookup"><span data-stu-id="70664-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="70664-111">Когда пользователь входит в tooan приложение, использующее Azure AD для проверки подлинности, Azure AD создает маркер безопасности, содержащий сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="70664-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="70664-112">Этот маркер подписывается с помощью Azure AD, используя свой закрытый ключ, перед отправкой приложения toohello назад.</span><span class="sxs-lookup"><span data-stu-id="70664-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="70664-113">tooverify, hello токен действителен и получен из Azure AD, hello приложение должно проверить подпись токена hello, с помощью hello открытого ключа, предоставленного Azure AD, который содержится в клиенте hello [OpenID Connect документ обнаружения](http://openid.net/specs/openid-connect-discovery-1_0.html) или SAML, WS-Fed [документа метаданных федерации](active-directory-federation-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="70664-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="70664-114">В целях безопасности Azure AD подписывание ключей выполняется накат периодически и в случае чрезвычайной hello удалось следует развертывать по немедленно.</span><span class="sxs-lookup"><span data-stu-id="70664-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="70664-115">Любое приложение, которое интегрируется с Azure AD должен быть подготовлен toohandle событие смены ключа независимо от того, насколько часто эта проблема может возникнуть.</span><span class="sxs-lookup"><span data-stu-id="70664-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="70664-116">Если это не так, и ваше приложение попытается toouse hello tooverify с истекшим сроком действия ключа подписи в токене, hello вход запрос завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="70664-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="70664-117">В документе discovery OpenID Connect hello и документа метаданных федерации hello доступен более чем один допустимый ключ.</span><span class="sxs-lookup"><span data-stu-id="70664-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="70664-118">Приложение должно быть подготовлено toouse все ключи hello указывать в документе hello, так как один ключ может быть сменен раньше, другой может оказаться его заменой и т. д.</span><span class="sxs-lookup"><span data-stu-id="70664-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="70664-119">Как tooassess Если повлияет на приложения и какие toodo о нем</span><span class="sxs-lookup"><span data-stu-id="70664-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="70664-120">Как приложение обрабатывает смены ключей зависит от переменных, например приложения или использовался какие протокол идентификации и библиотеки типа hello.</span><span class="sxs-lookup"><span data-stu-id="70664-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="70664-121">в следующих разделах Hello оцениваться hello наиболее распространенных типов приложений затрагивает hello смены ключей, а также сведения о tooupdate автоматическую смену toosupport приложения hello, или вручную обновить ключ hello.</span><span class="sxs-lookup"><span data-stu-id="70664-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="70664-122">Собственные клиентские приложения, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="70664-123">Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="70664-124">Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure</span><span class="sxs-lookup"><span data-stu-id="70664-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="70664-125">Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed</span><span class="sxs-lookup"><span data-stu-id="70664-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="70664-126">Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect .NET Core</span><span class="sxs-lookup"><span data-stu-id="70664-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="70664-127">Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="70664-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="70664-128">Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="70664-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="70664-129">Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="70664-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="70664-130">Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="70664-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="70664-131">Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="70664-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="70664-132">Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008, 2010 или Windows Identity Foundation</span><span class="sxs-lookup"><span data-stu-id="70664-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="70664-133">Веб-приложений и защите ресурсов API-интерфейсов с помощью любого другие библиотеки или вручную реализации любого из hello поддерживаются протоколы</span><span class="sxs-lookup"><span data-stu-id="70664-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="70664-134">Это руководство **не** применимо к:</span><span class="sxs-lookup"><span data-stu-id="70664-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="70664-135">Приложения, добавленные из коллекции Azure AD приложения (включая пользовательские) имеют отдельные инструкции с ключами toosigning отношении.</span><span class="sxs-lookup"><span data-stu-id="70664-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> <span data-ttu-id="70664-136">[Дополнительные сведения](../active-directory-sso-certs.md).</span><span class="sxs-lookup"><span data-stu-id="70664-136">[More information.](../active-directory-sso-certs.md)</span></span>
* <span data-ttu-id="70664-137">Локальных приложений, опубликованных через прокси-сервер приложения нет tooworry о ключей подписывания.</span><span class="sxs-lookup"><span data-stu-id="70664-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="70664-138"><a name="nativeclient"></a>Собственные клиентские приложения, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="70664-139">Как правило, приложения, только осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="70664-140">Microsoft Graph, KeyVault, API-Интерфейс Outlook и другие API-интерфейсы Microsoft) обычно только получение токена и передать его дальше toohello владельца ресурса.</span><span class="sxs-lookup"><span data-stu-id="70664-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="70664-141">Учитывая, что они не используются для защиты всех ресурсов, они не проверять токен hello и не требуется tooensure, которые он подписан должным образом.</span><span class="sxs-lookup"><span data-stu-id="70664-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="70664-142">Собственные клиентские приложения, ли настольных компьютеров или мобильных устройств, попадают в эту категорию и таким образом не затронуты hello продолжения.</span><span class="sxs-lookup"><span data-stu-id="70664-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="70664-143"><a name="webclient"></a>Веб-приложения и интерфейсы API, осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="70664-144">Как правило, приложения, только осуществляющие доступ к ресурсам</span><span class="sxs-lookup"><span data-stu-id="70664-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="70664-145">Microsoft Graph, KeyVault, API-Интерфейс Outlook и другие API-интерфейсы Microsoft) обычно только получение токена и передать его дальше toohello владельца ресурса.</span><span class="sxs-lookup"><span data-stu-id="70664-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="70664-146">Учитывая, что они не используются для защиты всех ресурсов, они не проверять токен hello и не требуется tooensure, которые он подписан должным образом.</span><span class="sxs-lookup"><span data-stu-id="70664-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="70664-147">Веб-приложений и веб-API, в которых используется только для приложений потока hello (учетные данные клиента и сертификат клиента), попадают в эту категорию и, таким образом не подвержены hello продолжения.</span><span class="sxs-lookup"><span data-stu-id="70664-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="70664-148"><a name="appservices"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные с помощью служб приложений Azure</span><span class="sxs-lookup"><span data-stu-id="70664-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="70664-149">Проверка подлинности Azure службы приложений и функциональные возможности авторизации (EasyAuth) уже имеет смены ключей toohandle необходимую логику hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="70664-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="70664-150"><a name="owin"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации Microsoft Azure Active Directory, .NET OWIN OpenID Connect или WS-Fed</span><span class="sxs-lookup"><span data-stu-id="70664-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="70664-151">Если приложение использует hello .NET OWIN OpenID Connect, WS-Fed или WindowsAzureActiveDirectoryBearerAuthentication по промежуточного слоя, он уже имеется смены ключей toohandle необходимую логику hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="70664-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="70664-152">Убедитесь, что приложение использует любой из этих ищет все следующие фрагменты кода в файле Startup.cs или Startup.Auth.cs приложения hello</span><span class="sxs-lookup"><span data-stu-id="70664-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="70664-153"><a name="owincore"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с использованием ПО промежуточного слоя для аутентификации на основе токена носителя JWT или OpenID Connect.NET Core</span><span class="sxs-lookup"><span data-stu-id="70664-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="70664-154">Если приложение использует .NET Core OWIN OpenID Connect hello или JwtBearerAuthentication по промежуточного слоя, он уже имеется смены ключей toohandle необходимую логику hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="70664-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="70664-155">Убедитесь, что приложение использует любой из этих ищет все следующие фрагменты кода в файле Startup.cs или Startup.Auth.cs приложения hello</span><span class="sxs-lookup"><span data-stu-id="70664-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="70664-156"><a name="passport"></a>Веб-приложения и интерфейсы API, защищающие ресурсы с помощью модуля Node.js passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="70664-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="70664-157">Если приложение использует модуль passport ad Node.js hello, он уже имеется смены ключей toohandle необходимую логику hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="70664-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="70664-158">Вы можете убедитесь, что приложение passport рекламы, выполняя поиск следующий фрагмент кода в файле app.js приложения hello</span><span class="sxs-lookup"><span data-stu-id="70664-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="70664-159"><a name="vs2015"></a>Защищающие ресурсы веб-приложения и интерфейсы API, созданные в Visual Studio 2015 или Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="70664-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="70664-160">Если приложение создано с помощью шаблона веб-приложения в Visual Studio 2015 или Visual Studio 2017 г. и выбрано **рабочих и учебных учетных записей** из hello **изменить аутентификацию** меню, он уже автоматически имеет смены ключей toohandle необходимую логику hello.</span><span class="sxs-lookup"><span data-stu-id="70664-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="70664-161">Эта логика, внедренных в hello OWIN OpenID Connect по промежуточного слоя, получает и кэширует hello ключи из документа обнаружения OpenID Connect hello и периодически обновляет их.</span><span class="sxs-lookup"><span data-stu-id="70664-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="70664-162">Если вручную добавлен решение tooyour проверки подлинности, приложение может не иметь hello необходимая логика смены ключей.</span><span class="sxs-lookup"><span data-stu-id="70664-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="70664-163">Вам потребуется toowrite его самостоятельно, либо hello выполните шаги в [веб-приложений и протоколы, поддерживаемые интерфейсы API используются любые другие библиотеки или вручную реализации любого из hello.](#other).</span><span class="sxs-lookup"><span data-stu-id="70664-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="70664-164"><a name="vs2013"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="70664-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="70664-165">Если приложение создано с помощью шаблона веб-приложения в Visual Studio 2013 и вы выбрали **учетные записи организации** из hello **изменить проверку подлинности** меню, оно уже имеет необходимости hello Логика toohandle ключа продолжения автоматически.</span><span class="sxs-lookup"><span data-stu-id="70664-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="70664-166">Логика хранит уникальный идентификатор вашей организации и подписи ключевые данные в двух таблицах базы данных, связанные с проектом hello hello.</span><span class="sxs-lookup"><span data-stu-id="70664-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="70664-167">Hello строку подключения для базы данных hello можно найти в файле Web.config проекта hello.</span><span class="sxs-lookup"><span data-stu-id="70664-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="70664-168">Если вручную добавлен решение tooyour проверки подлинности, приложение может не иметь hello необходимая логика смены ключей.</span><span class="sxs-lookup"><span data-stu-id="70664-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="70664-169">Вам потребуется toowrite его самостоятельно, либо hello выполните шаги в [веб-приложений и протоколы, поддерживаемые интерфейсы API используются любые другие библиотеки или вручную реализации любого из hello.](#other).</span><span class="sxs-lookup"><span data-stu-id="70664-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="70664-170">Hello следующие шаги помогут проверить правильность работы логики hello в приложении.</span><span class="sxs-lookup"><span data-stu-id="70664-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="70664-171">В Visual Studio 2013 откройте решение hello и щелкните hello **обозревателя серверов** вкладку в правом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="70664-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="70664-172">Разверните узлы **Подключения данных**, **DefaultConnection**, а затем — **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="70664-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="70664-173">Найдите hello **IssuingAuthorityKeys** , щелкните его правой кнопкой мыши, а затем выберите пункт **Показать таблицу данных**.</span><span class="sxs-lookup"><span data-stu-id="70664-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="70664-174">В hello **IssuingAuthorityKeys** таблицы, будут существовать по крайней мере одна строка, соответствующая toohello отпечатка для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="70664-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="70664-175">Удаляет все строки в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="70664-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="70664-176">Щелкните правой кнопкой мыши hello **клиентов** , а затем выберите пункт **Показать таблицу данных**.</span><span class="sxs-lookup"><span data-stu-id="70664-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="70664-177">В hello **клиентов** таблицы, будут существовать по крайней мере одна строка, соответствующая tooa уникальному идентификатору клиента каталога.</span><span class="sxs-lookup"><span data-stu-id="70664-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="70664-178">Удаляет все строки в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="70664-178">Delete any rows in hello table.</span></span> <span data-ttu-id="70664-179">Если вы не удалите hello строк в обоих hello **клиентов** таблицы и **IssuingAuthorityKeys** таблицы, вы получите ошибку во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="70664-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="70664-180">Постройте и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="70664-180">Build and run hello application.</span></span> <span data-ttu-id="70664-181">После входа в учетную запись tooyour, можно остановить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="70664-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="70664-182">Вернуть toohello **обозревателя серверов** и просмотрите значения hello в hello **IssuingAuthorityKeys** и **клиентов** таблицы.</span><span class="sxs-lookup"><span data-stu-id="70664-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="70664-183">Вы заметите, что они были автоматически повторно с hello нужные сведения из документа метаданных федерации hello.</span><span class="sxs-lookup"><span data-stu-id="70664-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="70664-184"><a name="vs2013"></a>Защищающие ресурсы веб-интерфейсы, созданные в Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="70664-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="70664-185">Если создать веб-API в Visual Studio 2013 с помощью шаблона веб-API hello и последующего выбора **учетные записи организации** из hello **изменить аутентификацию** меню, вы уже имеют hello необходимую логику в приложение.</span><span class="sxs-lookup"><span data-stu-id="70664-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="70664-186">Если вы настроили проверку подлинности вручную, следуйте инструкциям hello ниже toolearn как tooconfigure вашего веб-API tooautomatically обновить сведения о его.</span><span class="sxs-lookup"><span data-stu-id="70664-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="70664-187">Hello следующий фрагмент кода демонстрирует способ tooget hello последние ключи из документа метаданных федерации hello, а затем использовать hello [обработчик токенов JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello маркер.</span><span class="sxs-lookup"><span data-stu-id="70664-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="70664-188">фрагмент кода Hello предполагается, что необходимо использовать собственный механизм для сохранения будущих toovalidate ключа hello кэширования токены из Azure AD ли в базе данных, файл конфигурации или в другом месте.</span><span class="sxs-lookup"><span data-stu-id="70664-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
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

### <span data-ttu-id="70664-189"><a name="vs2012"></a>Защищающие ресурсы веб-приложения, созданные в Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="70664-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="70664-190">Если приложение создано в Visual Studio 2012, вы вероятно использовали hello удостоверений и средства доступа к tooconfigure приложения.</span><span class="sxs-lookup"><span data-stu-id="70664-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="70664-191">Вероятно, что вы используете hello [проверки издателя имя реестра (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span><span class="sxs-lookup"><span data-stu-id="70664-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="70664-192">Hello VINR отвечает за поддержание сведений о доверенных поставщиках удостоверений (Azure AD) и использования выданных ими токенов toovalidate hello ключей.</span><span class="sxs-lookup"><span data-stu-id="70664-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="70664-193">Hello VINR также упрощает легко tooautomatically hello ключевые сведения об обновлении хранятся в файле Web.config, загрузив hello последнего документа метаданных федерации связанной с вашим каталогом, проверки конфигурации hello устарела с hello последняя версия документ и обновить hello приложения toouse hello новый ключ при необходимости.</span><span class="sxs-lookup"><span data-stu-id="70664-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="70664-194">Если вы создали приложение с помощью любого из примеров кода hello или пошаговой документации, предоставляемой корпорацией Майкрософт, логика смены ключей hello уже включены в проект.</span><span class="sxs-lookup"><span data-stu-id="70664-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="70664-195">Обратите внимание, что приведенный ниже код hello уже существует в проекте.</span><span class="sxs-lookup"><span data-stu-id="70664-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="70664-196">Если приложение не имеет этой логики, действуйте hello ниже tooadd его и tooverify, в которой он работает правильно.</span><span class="sxs-lookup"><span data-stu-id="70664-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="70664-197">В **обозревателе решений**, добавьте toohello ссылки **System.IdentityModel** сборки для hello соответствующий проект.</span><span class="sxs-lookup"><span data-stu-id="70664-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="70664-198">Откройте hello **Global.asax.cs** файл и добавьте следующее hello директивы using:</span><span class="sxs-lookup"><span data-stu-id="70664-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="70664-199">Добавьте следующий метод toohello hello **Global.asax.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="70664-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="70664-200">Вызвать hello **RefreshValidationSettings()** метод в hello **Application_Start()** метод в **Global.asax.cs** следующим:</span><span class="sxs-lookup"><span data-stu-id="70664-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="70664-201">После выполнения этих действий файл Web.config приложения будет обновляться с последними сведениями hello из документа метаданных федерации hello, включая последние ключи hello.</span><span class="sxs-lookup"><span data-stu-id="70664-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="70664-202">Это обновление будет выполняться каждый раз при перезапуске пула приложений в IIS; по умолчанию службы IIS установлен toorecycle приложения каждые 29 часов.</span><span class="sxs-lookup"><span data-stu-id="70664-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="70664-203">Выполните действия hello ниже tooverify работы логики смены ключей hello.</span><span class="sxs-lookup"><span data-stu-id="70664-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="70664-204">После проверки ваше приложение использует кода hello выше, откройте hello **Web.config** файл и перейдите toohello  **<issuerNameRegistry>**  блок специально hello следующие несколько строк:</span><span class="sxs-lookup"><span data-stu-id="70664-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="70664-205">В hello  **<add thumbprint=””>**  измените значение отпечатка hello, заменив любой символ на другой.</span><span class="sxs-lookup"><span data-stu-id="70664-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="70664-206">Сохранить hello **Web.config** файла.</span><span class="sxs-lookup"><span data-stu-id="70664-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="70664-207">Создание приложения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="70664-207">Build hello application, and then run it.</span></span> <span data-ttu-id="70664-208">Если вы можете завершить процесс входа hello, приложение успешно обновляет ключ hello, загрузив hello необходимые сведения из документа метаданных федерации вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="70664-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="70664-209">Если возникли проблемы со входом, обеспечивают hello изменений в приложении правильный, считывая hello [Добавление входа tooYour Web приложения с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) разделе, или загрузка и проверка hello следующий образец кода: [ Многопользовательского облачного приложения для Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span><span class="sxs-lookup"><span data-stu-id="70664-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="70664-210"><a name="vs2010"></a>Защищающие ресурсы веб-приложения, созданные с помощью Visual Studio 2008 или 2010 и Windows Identity Foundation v1.0 для .NET 3.5</span><span class="sxs-lookup"><span data-stu-id="70664-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="70664-211">При построении приложения на платформе WIF 1.0 нет tooautomatically не предоставленного механизм обновления конфигурации приложения toouse новый ключ.</span><span class="sxs-lookup"><span data-stu-id="70664-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="70664-212">*Наиболее простым способом* использовать hello fedutil, включенное в hello WIF SDK, который можно получить hello последнего документа метаданных и обновить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="70664-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="70664-213">Обновление вашего приложения too.NET 4.5, включая hello новейшую версию WIF, расположенных в пространстве имен System hello.</span><span class="sxs-lookup"><span data-stu-id="70664-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="70664-214">Затем можно использовать hello [проверки издателя имя реестра (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform автоматические обновления конфигурации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="70664-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="70664-215">Выполните вручную продолжения согласно инструкциям, приведенным hello в конце hello в этом документе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="70664-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="70664-216">Инструкции toouse hello FedUtil tooupdate конфигурации:</span><span class="sxs-lookup"><span data-stu-id="70664-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="70664-217">Убедитесь, что hello WIF 1.0 SDK, установленный на компьютере разработки для Visual Studio 2008 или 2010.</span><span class="sxs-lookup"><span data-stu-id="70664-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="70664-218">Если этот пакет не установлен, его можно [скачать отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=4451).</span><span class="sxs-lookup"><span data-stu-id="70664-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="70664-219">В Visual Studio откройте решение hello, а затем щелкните правой кнопкой мыши соответствующий проект hello и выберите **обновление метаданных федерации**.</span><span class="sxs-lookup"><span data-stu-id="70664-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="70664-220">Если этот параметр недоступен, FedUtil и (или) hello WIF 1.0 SDK не установлен.</span><span class="sxs-lookup"><span data-stu-id="70664-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="70664-221">В строке приветствия выберите **обновление** toobegin обновление метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="70664-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="70664-222">При наличии доступа к toohello серверной среде, где размещается приложение hello, при необходимости можно использовать в FedUtil [планировщик метаданных автоматического обновления](https://msdn.microsoft.com/library/ee517272.aspx).</span><span class="sxs-lookup"><span data-stu-id="70664-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="70664-223">Нажмите кнопку **Готово** процесс обновления toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="70664-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="70664-224"><a name="other"></a>Веб-приложений и защите ресурсов API-интерфейсов с помощью любого другие библиотеки или вручную реализации любого из hello поддерживаются протоколы</span><span class="sxs-lookup"><span data-stu-id="70664-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="70664-225">Если вы используете другой библиотеки или вручную реализовать один из поддерживаемых hello протоколов, вам потребуется tooreview hello библиотеки или вашей tooensure реализацию, hello ключ извлекается из документа обнаружения OpenID Connect hello или hello документ метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="70664-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="70664-226">Одним из способов toocheck для этого является toodo поиск в коде или в код библиотеки hello все вызовы tooeither hello OpenID обнаружения документа или документа метаданных федерации hello.</span><span class="sxs-lookup"><span data-stu-id="70664-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="70664-227">Если ключ хранятся в другом или жестко задано в приложении, можно вручную извлечь ключ hello и его соответствующим образом выполнять вручную продолжения согласно инструкциям, приведенным hello в конце hello в этом документе инструкции update.</span><span class="sxs-lookup"><span data-stu-id="70664-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="70664-228">**Настоятельно рекомендуется усилить автоматическую смену toosupport приложения** с помощью любого hello приближается структуры в этой статье tooavoid будущих перебои и служебных данных, если Azure AD увеличивает периодичности переключения или аварийный продолжения по каналу.</span><span class="sxs-lookup"><span data-stu-id="70664-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="70664-229">Как tootest toodetermine вашего приложения, если будут затронуты</span><span class="sxs-lookup"><span data-stu-id="70664-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="70664-230">Вы можете проверить, является ли ваше приложение поддерживает автоматическую смену ключей, загрузив hello сценариев и следуйте инструкциям hello в [этот репозиторий GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="70664-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="70664-231">Как tooperform вручную продолжения, если после этого приложение не поддерживает автоматическую смену</span><span class="sxs-lookup"><span data-stu-id="70664-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="70664-232">Если приложение **не** поддерживает автоматическую смену, вы должны будете tooestablish процесс, который периодически подписывающий мониторы Azure AD, ключи и выполняет вручную продолжения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="70664-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="70664-233">[Этот репозиторий GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) содержит сценарии и инструкции о том, как toodo это.</span><span class="sxs-lookup"><span data-stu-id="70664-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

