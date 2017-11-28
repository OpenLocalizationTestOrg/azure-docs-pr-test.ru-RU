---
title: "aaaHow tooenable нескольких приложений единого входа в Android с помощью ADAL | Документы Microsoft"
description: "Как функции hello toouse hello tooenable ADAL SDK единого входа для приложения. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="d133a-103">Как tooenable нескольких приложений единого входа в Android с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="d133a-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="d133a-104">Клиенты теперь ожидает предоставления единого входа (SSO), чтобы пользователи tooenter свои учетные данные требуются один раз и иметь эти учетные данные автоматически работать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="d133a-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="d133a-105">Введите свое имя пользователя и пароль на небольшом экране, часто раз в сочетании с дополнительный фактор (2FA) как телефонный звонок или текстовые сообщения кода, сложности Hello приведет к неудовлетворенности быстрый, если пользователь имеет toodo это более чем один раз для операционной системы.</span><span class="sxs-lookup"><span data-stu-id="d133a-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="d133a-106">Кроме того при применении с платформой удостоверений и другие приложения могут использовать как учетные записи Майкрософт или рабочую учетную запись из Office 365, клиентам ожидать, что эти учетные данные toobe доступных toouse для всех приложений независимо от поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="d133a-107">Hello платформы Microsoft Identity, вместе с нашей удостоверение пакеты SDK, не это непростая работа для вас и дает возможность toodelight hello клиентов с помощью единого входа, либо в собственного набора приложений, или как с нашими broker возможности и средства проверки подлинности приложения, по всей устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="d133a-108">В этом пошаговом руководстве будет показывают, как это tooconfigure нашего пакета SDK в рамках вашего приложения tooprovide tooyour это преимущество клиентов.</span><span class="sxs-lookup"><span data-stu-id="d133a-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="d133a-109">Руководство применимо при работе с такими службами:</span><span class="sxs-lookup"><span data-stu-id="d133a-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="d133a-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d133a-110">Azure Active Directory</span></span>
* <span data-ttu-id="d133a-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d133a-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="d133a-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d133a-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="d133a-113">Условный доступ к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d133a-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="d133a-114">документ Hello выше предполагается, вы знаете, как слишком[подготовки приложений прежних версий портале hello для Azure Active Directory](active-directory-how-to-integrate.md) и интегрированные приложения hello [Microsoft Identity пакета SDK для Android](https://github.com/AzureAD/azure-activedirectory-library-for-android) .</span><span class="sxs-lookup"><span data-stu-id="d133a-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="d133a-115">Основные понятия единого входа в hello платформы удостоверений</span><span class="sxs-lookup"><span data-stu-id="d133a-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="d133a-116">Брокеры Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="d133a-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="d133a-117">Корпорация Майкрософт предоставляет приложениями для каждой платформы мобильных устройств, которые позволяют к мосту hello учетных данных в приложениях различных поставщиков и позволяет специальные расширенные функции, требующих одного надежное место, откуда toovalidate учетные данные.</span><span class="sxs-lookup"><span data-stu-id="d133a-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="d133a-118">Они называются **брокеры**.</span><span class="sxs-lookup"><span data-stu-id="d133a-118">We call these **brokers**.</span></span> <span data-ttu-id="d133a-119">В iOS и Android они предоставляются через загружаемых приложений, что клиентам установить независимо друг от друга или могут передаваться toohello устройства компании, который управляет некоторые или все устройства hello для своих сотрудников.</span><span class="sxs-lookup"><span data-stu-id="d133a-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="d133a-120">Эти брокеры поддерживает управление безопасности только для некоторых приложений или hello всего устройства на основании нужен ИТ-администраторов.</span><span class="sxs-lookup"><span data-stu-id="d133a-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="d133a-121">В Windows эта функциональность обеспечивается выбора учетной записи, встроенной в toohello операционной системы, технически называется hello веб-брокер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d133a-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="d133a-122">Дополнительные сведения о том, как использовать эти брокеры и как ваши клиенты могут просматривать в их процедуры входа в систему для чтения на платформе Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="d133a-123">Способы входа на мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="d133a-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="d133a-124">Toocredentials доступ на устройствах выполните две основные шаблоны для платформы Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="d133a-125">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="d133a-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="d133a-126">вход с брокером.</span><span class="sxs-lookup"><span data-stu-id="d133a-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="d133a-127">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="d133a-127">Non-broker assisted logins</span></span>
<span data-ttu-id="d133a-128">Имена входа службы помощи брокера не будут возможностей входа, происходит внутри приложения hello и использовать локальное хранилище hello hello устройства для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="d133a-129">Это хранилище может быть совместно используемых несколькими приложениями, но учетные данные hello, тесно связанных toohello приложения или набора приложений с помощью этих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d133a-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="d133a-130">Скорее всего знакомы это во многих мобильных приложениях при вводе имени пользователя и пароля в само приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="d133a-131">Эти имена входа имеют hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d133a-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="d133a-132">Взаимодействие с пользователем существует целиком в пределах приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="d133a-133">Учетные данные могут совместно использоваться в приложения, которые должны быть подписаны hello один сертификат, предоставляя tooyour интерфейса единого входа для этих приложений.</span><span class="sxs-lookup"><span data-stu-id="d133a-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="d133a-134">Управление вокруг hello возможности ведения журнала предусмотрен toohello приложения до и после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="d133a-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="d133a-135">Эти имена входа имеют следующие недостатки hello:</span><span class="sxs-lookup"><span data-stu-id="d133a-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="d133a-136">единый вход будет доступен пользователю не во всех приложениях, в которых используются удостоверения Microsoft Identity, а только для тех удостоверений Microsoft Identity, которые настроены в вашем приложении;</span><span class="sxs-lookup"><span data-stu-id="d133a-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="d133a-137">Приложение не может использоваться с более сложных функций бизнеса, например условный доступ или использование hello InTune набором продуктов.</span><span class="sxs-lookup"><span data-stu-id="d133a-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="d133a-138">приложение не поддерживает аутентификацию бизнес-пользователей на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="d133a-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="d133a-139">Вот представление принципов работы hello удостоверение пакеты SDK с хранилищем общих hello из вашего приложения tooenable единого входа:</span><span class="sxs-lookup"><span data-stu-id="d133a-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="d133a-140">Вход с брокером</span><span class="sxs-lookup"><span data-stu-id="d133a-140">Broker assisted logins</span></span>
<span data-ttu-id="d133a-141">Вспомогательная Broker имена входа будут возможностей входа, которые происходят в приложении broker hello и используют hello хранения и безопасности учетных данных tooshare broker hello для всех приложений на устройстве hello применимые платформы Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="d133a-142">Это означает, что приложения зависят от пользователей toosign broker hello в.</span><span class="sxs-lookup"><span data-stu-id="d133a-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="d133a-143">В iOS и Android эти брокеры предоставляются через загружаемых приложений, что клиентам устанавливать независимо друг от друга или могут передаваться toohello устройства компании, который управляет устройством hello для своих пользователей.</span><span class="sxs-lookup"><span data-stu-id="d133a-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="d133a-144">Пример приложения такого типа является приложением проверки подлинности Microsoft hello в iOS.</span><span class="sxs-lookup"><span data-stu-id="d133a-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="d133a-145">В Windows эта функциональность обеспечивается выбора учетной записи, встроенной в toohello операционной системы, технически называется hello веб-брокер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d133a-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="d133a-146">взаимодействие Hello зависит от платформы и иногда может быть критическими toousers случае правильного управления.</span><span class="sxs-lookup"><span data-stu-id="d133a-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="d133a-147">Вы, вероятно, наиболее знакомы с этим шаблоном, если установлено приложение Facebook hello и использовать Facebook Connect из другого приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="d133a-148">Hello использует платформу Microsoft Identity hello таким шаблоном.</span><span class="sxs-lookup"><span data-stu-id="d133a-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="d133a-149">Для iOS это порождает анимация «изменения» tooa которой приложение отправляется фона toohello во время проверки подлинности Microsoft приложения hello поставляется toohello переднего плана для пользователя tooselect hello учетную запись, которая как toosign с.</span><span class="sxs-lookup"><span data-stu-id="d133a-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="d133a-150">Для Android и Windows учетная запись hello выбора отображается поверх вашего приложения, которое находится так сильно мешают toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="d133a-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="d133a-151">Получает вызов hello broker</span><span class="sxs-lookup"><span data-stu-id="d133a-151">How hello broker gets invoked</span></span>
<span data-ttu-id="d133a-152">Если совместимые broker установлено на устройстве hello, как hello приложения проверки подлинности Microsoft, hello пакеты SDK удостоверение будет автоматически hello рабочих вызова hello broker автоматически, когда пользователь указывает, что ими toolog любой учетной записью из Платформа Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="d133a-153">Это может быть личная учетная запись Майкрософт, рабочая или учебная учетная запись либо любая другая учетная запись, которую вы предоставили и разместили в Azure с использованием продуктов B2C и B2B.</span><span class="sxs-lookup"><span data-stu-id="d133a-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="d133a-154">Как мы обеспечиваем hello приложения является допустимым</span><span class="sxs-lookup"><span data-stu-id="d133a-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="d133a-155">необходимость Hello tooensure удостоверением hello hello вызовов приложения-посредника является ключевым toohello безопасности, предоставляемых нами в входа компонента service broker вспомогательная.</span><span class="sxs-lookup"><span data-stu-id="d133a-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="d133a-156">Не iOS и Android обеспечивает уникальные идентификаторы, которые допустимы только для данного приложения, вредоносные программы могут «спуфинг» идентификатор легальных приложений и получать токены hello предназначены для допустимых приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="d133a-157">tooensure, которым мы всегда связываются с правом приложения hello во время выполнения, мы просим tooprovide developer Привет пользовательских redirectURI при регистрации своих приложений с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d133a-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="d133a-158">**Ниже подробно описано, как разработчикам следует создавать этот универсальный код ресурса (URI) для перенаправления.**</span><span class="sxs-lookup"><span data-stu-id="d133a-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="d133a-159">Этот пользовательский redirectURI содержит отпечаток сертификата hello приложения hello и гарантируется toobe уникальный toohello приложения hello магазина Google Play.</span><span class="sxs-lookup"><span data-stu-id="d133a-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="d133a-160">Когда приложение вызывает hello broker hello broker запрашивает hello операционной системы Android tooprovide его с hello отпечаток сертификата, что брокер вызываемой hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="d133a-161">Hello broker предоставляет этот tooMicrosoft отпечаток сертификата в системы удостоверений tooour вызов hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="d133a-162">Если сертификат hello отпечаток приложения hello не соответствует отпечаток сертификата hello toous разработчиком hello во время регистрации, мы будет запрещать доступ toohello маркеры для запрашивает приложение hello hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d133a-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="d133a-163">Эта проверка гарантирует, только приложение hello, зарегистрированные разработчиком hello получение маркеров.</span><span class="sxs-lookup"><span data-stu-id="d133a-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="d133a-164">**Разработчик Hello имеет hello выбор, если hello пакет SDK для Microsoft Identity вызывает hello broker или использует службы помощи потока без посредника hello.**</span><span class="sxs-lookup"><span data-stu-id="d133a-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="d133a-165">Однако если hello разработчик выбирает не toouse hello вспомогательная broker потока потеряют hello преимущество использования учетных данных единого входа этого пользователя hello может уже присутствует на устройстве hello и предотвращает их приложения не могут использоваться с бизнес-функций Microsoft предоставляет клиентам как условного доступа, возможности управления Intune и проверку подлинности на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="d133a-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="d133a-166">Эти имена входа имеют hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d133a-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="d133a-167">Пользователь получает единого входа для всех приложений независимо от поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="d133a-168">Приложения можно использовать расширенные возможности бизнеса, например условный доступ или hello InTune набором продуктов.</span><span class="sxs-lookup"><span data-stu-id="d133a-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="d133a-169">приложение может поддерживать аутентификацию бизнес-пользователей на основе сертификата;</span><span class="sxs-lookup"><span data-stu-id="d133a-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="d133a-170">Намного безопаснее входа пользователей как hello удостоверения приложения hello и hello пользователя проверяются hello broker приложения с помощью шифрования и алгоритмы дополнительной безопасности.</span><span class="sxs-lookup"><span data-stu-id="d133a-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="d133a-171">Эти имена входа имеют следующие недостатки hello:</span><span class="sxs-lookup"><span data-stu-id="d133a-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="d133a-172">В iOS hello пользователь перешел из взаимодействие приложения пока выбираются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="d133a-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="d133a-173">Потеря toomanage hello hello возможность входа взаимодействия для клиентов в приложении.</span><span class="sxs-lookup"><span data-stu-id="d133a-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="d133a-174">Вот представление как hello SDK удостоверений Майкрософт работают с hello компонента service broker приложения tooenable единого входа:</span><span class="sxs-lookup"><span data-stu-id="d133a-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="d133a-175">Используя эти сведения в фоновом режиме должен быть toobetter может в изучении и реализации единого входа в приложении с помощью платформы Microsoft Identity hello и пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="d133a-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="d133a-176">Включение единого входа в нескольких приложениях с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="d133a-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="d133a-177">Здесь мы используем hello ADAL пакета SDK для Android для:</span><span class="sxs-lookup"><span data-stu-id="d133a-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="d133a-178">включение единого входа без помощи брокера для набора приложений;</span><span class="sxs-lookup"><span data-stu-id="d133a-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="d133a-179">включить поддержку единого входа с помощью брокера.</span><span class="sxs-lookup"><span data-stu-id="d133a-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="d133a-180">Включение единого входа без брокера</span><span class="sxs-lookup"><span data-stu-id="d133a-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="d133a-181">Без посредника интерактивную единый вход для приложения hello пакеты SDK удостоверение управляет значительную часть сложности hello единого входа для.</span><span class="sxs-lookup"><span data-stu-id="d133a-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="d133a-182">Сюда входят поиска правой пользователя hello в кэше hello и список пользователей, вошедший в систему для вас tooquery обслуживание.</span><span class="sxs-lookup"><span data-stu-id="d133a-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="d133a-183">tooenable единого входа в приложениях, владеющих требуется hello toodo следующие:</span><span class="sxs-lookup"><span data-stu-id="d133a-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="d133a-184">Убедитесь, все вашего приложения пользователя hello же идентификатор клиента или идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="d133a-185">Убедитесь, что все приложения должны задать же SharedUserID hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="d133a-186">Убедитесь, что все из общей папки вашего приложения hello, же подписи сертификат из Google Play hello хранилища, чтобы общий доступ к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="d133a-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="d133a-187">Шаг 1: С помощью hello таким же Идентификатором клиента / идентификатор приложения для всех hello приложений в наборе приложений</span><span class="sxs-lookup"><span data-stu-id="d133a-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="d133a-188">Чтобы tooknow платформы Microsoft Identity hello допустимость его tooshare токены в приложениях каждое приложение потребуется hello tooshare же идентификатор клиента или идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="d133a-189">Это уникальный идентификатор hello, предоставленный tooyou при регистрации первого приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="d133a-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="d133a-190">Может возникнуть вопрос определяет различные приложения hello toohello службы Microsoft Identity, если он использует же идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="d133a-191">получен ответ Hello с hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="d133a-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="d133a-192">Каждое приложение может иметь несколько URI перенаправления зарегистрирован в портале адаптации hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="d133a-193">Каждое приложение в наборе получит уникальный код URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="d133a-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="d133a-194">Вот как это выглядит:</span><span class="sxs-lookup"><span data-stu-id="d133a-194">An example of how this looks is below:</span></span>

<span data-ttu-id="d133a-195">URI перенаправления App1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="d133a-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="d133a-196">URI перенаправления App2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="d133a-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="d133a-197">URI перенаправления App3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="d133a-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="d133a-198">....</span><span class="sxs-lookup"><span data-stu-id="d133a-198">....</span></span>

<span data-ttu-id="d133a-199">Они располагаются под hello же идентификатор клиента и идентификатор приложения и hello найденное на основе URI перенаправления, который возвращается toous в конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="d133a-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="d133a-200">*Обратите внимание, что формат эти URI перенаправления hello описаны ниже. Может использовать любой URI перенаправления, если не нужно toosupport hello брокера, в противном случае они должны выглядеть примерно следующим образом выше hello*</span><span class="sxs-lookup"><span data-stu-id="d133a-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="d133a-201">Шаг 2. Настройка общего хранилища в Android</span><span class="sxs-lookup"><span data-stu-id="d133a-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="d133a-202">Параметр hello `SharedUserID` выходит за рамки данного документа hello, но могут быть получены путем чтения hello документации Google Android на hello [манифеста](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="d133a-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="d133a-203">Важно, что именно вы решаете, как следует назвать идентификатор sharedUserID, и используете его во всех ваших приложениях.</span><span class="sxs-lookup"><span data-stu-id="d133a-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="d133a-204">При наличии hello `SharedUserID` во всех приложениях будут готовы toouse единого входа.</span><span class="sxs-lookup"><span data-stu-id="d133a-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="d133a-205">При совместном использовании хранилища для приложений любого приложения можно удалить пользователей или хуже удалить все маркеры hello всего приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="d133a-206">Это особенно катастрофические при наличии приложений, использующих hello токены toodo фоновой работы.</span><span class="sxs-lookup"><span data-stu-id="d133a-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="d133a-207">Совместное использование хранилища означает, что вы должны быть особой осторожностью удалить все операции с помощью hello SDK Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="d133a-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="d133a-208">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="d133a-208">That's it!</span></span> <span data-ttu-id="d133a-209">пакет SDK для Microsoft Identity Hello теперь будут совместно использовать учетные данные для всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d133a-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="d133a-210">список пользователей Hello также использоваться несколькими экземплярами приложений.</span><span class="sxs-lookup"><span data-stu-id="d133a-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="d133a-211">Включение единого входа с брокером</span><span class="sxs-lookup"><span data-stu-id="d133a-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="d133a-212">Здравствуйте, возможность toouse приложения является любой брокера, установленного на устройстве hello **отключена по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="d133a-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="d133a-213">Чтобы toouse приложения с помощью посредника hello необходимо выполнить дополнительные настройки и добавить некоторые приложения tooyour кода.</span><span class="sxs-lookup"><span data-stu-id="d133a-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="d133a-214">Hello toofollow шаги являются:</span><span class="sxs-lookup"><span data-stu-id="d133a-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="d133a-215">Включить режим брокера в код приложения вызов toohello MS SDK</span><span class="sxs-lookup"><span data-stu-id="d133a-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="d133a-216">Установить новый URI перенаправления, а также предоставляют tooboth приложение hello и регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="d133a-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="d133a-217">Настройка hello необходимые разрешения из манифеста Android hello</span><span class="sxs-lookup"><span data-stu-id="d133a-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="d133a-218">Шаг 1. Включение режима брокера в приложении</span><span class="sxs-lookup"><span data-stu-id="d133a-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="d133a-219">При создании hello «параметры» или начальной настройки проверки подлинности экземпляра включена возможность Hello broker hello toouse вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d133a-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="d133a-220">Это можно сделать, настроив тип ApplicationSettings в коде.</span><span class="sxs-lookup"><span data-stu-id="d133a-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="d133a-221">Шаг 2. Настройка нового кода URI перенаправления в схеме URL-адреса</span><span class="sxs-lookup"><span data-stu-id="d133a-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="d133a-222">В tooensure порядке, что мы всегда возвращает правильного приложения toohello токены hello учетных данных мы должны убедиться, что мы обратного вызова, можно проверить tooyour приложения, в результате которого hello операционной системы Android toomake.</span><span class="sxs-lookup"><span data-stu-id="d133a-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="d133a-223">Hello Android операционная система использует hello хэш сертификата hello в hello магазина Google Play.</span><span class="sxs-lookup"><span data-stu-id="d133a-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="d133a-224">Стороннее приложение не может подделать его.</span><span class="sxs-lookup"><span data-stu-id="d133a-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="d133a-225">Таким образом мы задействуем это вместе с URI нашей tooensure приложения брокера, возврат toohello правильного приложения hello токены hello.</span><span class="sxs-lookup"><span data-stu-id="d133a-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="d133a-226">Нам требуется вы tooestablish этот уникальный URI, как в приложении и набор перенаправления как URI перенаправления в наших портала для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="d133a-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="d133a-227">В URI перенаправления должен быть hello правильный формат:</span><span class="sxs-lookup"><span data-stu-id="d133a-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="d133a-228">Например, *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="d133a-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="d133a-229">Этот URI перенаправления должен toobe, указанный в регистрации вашего приложения, с помощью hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d133a-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d133a-230">Дополнительные сведения о регистрации приложения Azure AD см. в статье, посвященной [интеграции с Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="d133a-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="d133a-231">Шаг 3: Настройка разрешений в вашем приложении hello</span><span class="sxs-lookup"><span data-stu-id="d133a-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="d133a-232">Broker приложения в Android использует функцию диспетчера учетных записей hello учетные данные toomanage ОС Android hello в приложениях.</span><span class="sxs-lookup"><span data-stu-id="d133a-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="d133a-233">Посредник hello toouse заказа в Android манифест приложения должен иметь учетные записи AccountManager toouse разрешения.</span><span class="sxs-lookup"><span data-stu-id="d133a-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="d133a-234">Это подробно рассматривается в hello [Google документацию для диспетчера учетных записей](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="d133a-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="d133a-235">Речь идет о следующих разрешениях:</span><span class="sxs-lookup"><span data-stu-id="d133a-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="d133a-236">Вы настроили единый вход!</span><span class="sxs-lookup"><span data-stu-id="d133a-236">You've configured SSO!</span></span>
<span data-ttu-id="d133a-237">Теперь hello пакет SDK для Microsoft Identity автоматически и совместное использование учетных данных в приложениях и вызова неуправляемого кода hello broker при наличии на устройстве.</span><span class="sxs-lookup"><span data-stu-id="d133a-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

