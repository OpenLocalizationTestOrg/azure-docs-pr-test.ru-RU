---
title: "aaaHow tooenable SSO нескольких приложений на iOS с помощью ADAL | Документы Microsoft"
description: "Как функции hello toouse hello tooenable ADAL SDK единого входа для приложения. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="7a7ef-103">Как tooenable SSO нескольких приложений на iOS с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="7a7ef-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="7a7ef-104">Клиенты теперь ожидает предоставления единого входа (SSO), чтобы пользователи tooenter свои учетные данные требуются один раз и иметь эти учетные данные автоматически работать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="7a7ef-105">Введите свое имя пользователя и пароль на небольшом экране, часто раз в сочетании с дополнительный фактор (2FA) как телефонный звонок или текстовые сообщения кода, сложности Hello приведет к неудовлетворенности быстрый, если пользователь имеет toodo это более чем один раз для операционной системы.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="7a7ef-106">Кроме того при применении с платформой удостоверений и другие приложения могут использовать как учетные записи Майкрософт или рабочую учетную запись из Office 365, клиентам ожидать, что эти учетные данные toobe доступных toouse для всех приложений независимо от поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="7a7ef-107">Hello платформы Microsoft Identity, вместе с нашей удостоверение пакеты SDK, не это непростая работа для вас и дает возможность toodelight hello клиентов с помощью единого входа, либо в собственного набора приложений, или как с нашими broker возможности и средства проверки подлинности приложения, по всей устройства hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="7a7ef-108">В этом пошаговом руководстве будет показывают, как это tooconfigure нашего пакета SDK в рамках вашего приложения tooprovide tooyour это преимущество клиентов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="7a7ef-109">Руководство применимо при работе с такими службами:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="7a7ef-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a7ef-110">Azure Active Directory</span></span>
* <span data-ttu-id="7a7ef-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7a7ef-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="7a7ef-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="7a7ef-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="7a7ef-113">Условный доступ к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a7ef-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="7a7ef-114">документ Hello выше предполагается, вы знаете, как слишком[подготовки приложений прежних версий портале hello для Azure Active Directory](active-directory-how-to-integrate.md) и интегрированные приложения hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="7a7ef-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="7a7ef-115">Основные понятия единого входа в hello платформы удостоверений</span><span class="sxs-lookup"><span data-stu-id="7a7ef-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="7a7ef-116">Брокеры Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="7a7ef-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="7a7ef-117">Корпорация Майкрософт предоставляет приложениями для каждой платформы мобильных устройств, которые позволяют к мосту hello учетных данных в приложениях различных поставщиков и позволяет специальные расширенные функции, требующих одного надежное место, откуда toovalidate учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="7a7ef-118">Они называются **брокеры**.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-118">We call these **brokers**.</span></span> <span data-ttu-id="7a7ef-119">В iOS и Android эти брокеры предоставляются через загружаемых приложений, что клиентам установить независимо друг от друга или могут передаваться toohello устройства компании, который управляет некоторые или все устройства hello для своих сотрудников.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="7a7ef-120">Эти брокеры поддерживает управление безопасности только для некоторых приложений или hello всего устройства на основании нужен ИТ-администраторов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="7a7ef-121">В Windows эта функциональность обеспечивается выбора учетной записи, встроенной в toohello операционной системы, технически называется hello веб-брокер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="7a7ef-122">Дополнительные сведения о том, как использовать эти брокеры и как ваши клиенты могут просматривать в их процедуры входа в систему для чтения на платформе Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="7a7ef-123">Способы входа на мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="7a7ef-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="7a7ef-124">Toocredentials доступ на устройствах выполните две основные шаблоны для платформы Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="7a7ef-125">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="7a7ef-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="7a7ef-126">вход с брокером.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="7a7ef-127">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="7a7ef-127">Non-broker assisted logins</span></span>
<span data-ttu-id="7a7ef-128">Имена входа службы помощи брокера не будут возможностей входа, происходит внутри приложения hello и использовать локальное хранилище hello hello устройства для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="7a7ef-129">Это хранилище может быть совместно используемых несколькими приложениями, но учетные данные hello, тесно связанных toohello приложения или набора приложений с помощью этих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="7a7ef-130">Скорее всего знакомы это во многих мобильных приложениях при вводе имени пользователя и пароля в само приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="7a7ef-131">Эти имена входа имеют hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7a7ef-132">Взаимодействие с пользователем существует целиком в пределах приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="7a7ef-133">Учетные данные могут совместно использоваться в приложения, которые должны быть подписаны hello один сертификат, предоставляя tooyour интерфейса единого входа для этих приложений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="7a7ef-134">Управление вокруг hello возможности ведения журнала предусмотрен toohello приложения до и после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="7a7ef-135">Эти имена входа имеют следующие недостатки hello:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7a7ef-136">единый вход будет доступен пользователю не во всех приложениях, в которых используются удостоверения Microsoft Identity, а только для тех удостоверений Microsoft Identity, которые настроены в вашем приложении;</span><span class="sxs-lookup"><span data-stu-id="7a7ef-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="7a7ef-137">Приложение не может использоваться с более сложных функций бизнеса, например условный доступ или использование hello InTune набором продуктов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7a7ef-138">приложение не поддерживает аутентификацию бизнес-пользователей на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="7a7ef-139">Вот представление принципов работы hello удостоверение пакеты SDK с хранилищем общих hello из вашего приложения tooenable единого входа:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="7a7ef-140">Вход с брокером</span><span class="sxs-lookup"><span data-stu-id="7a7ef-140">Broker assisted logins</span></span>
<span data-ttu-id="7a7ef-141">Вспомогательная Broker имена входа будут возможностей входа, которые происходят в приложении broker hello и используют hello хранения и безопасности учетных данных tooshare broker hello для всех приложений на устройстве hello применимые платформы Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="7a7ef-142">Это означает, что приложения зависят от пользователей toosign broker hello в.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="7a7ef-143">В iOS и Android эти брокеры предоставляются через загружаемых приложений, что клиентам устанавливать независимо друг от друга или могут передаваться toohello устройства компании, который управляет устройством hello для своих пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="7a7ef-144">Пример приложения такого типа является приложением проверки подлинности Microsoft hello в iOS.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="7a7ef-145">В Windows эта функциональность обеспечивается выбора учетной записи, встроенной в toohello операционной системы, технически называется hello веб-брокер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="7a7ef-146">взаимодействие Hello зависит от платформы и иногда может быть критическими toousers случае правильного управления.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="7a7ef-147">Вы, вероятно, наиболее знакомы с этим шаблоном, если установлено приложение Facebook hello и использовать Facebook Connect из другого приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="7a7ef-148">Hello использует платформу Microsoft Identity hello таким шаблоном.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="7a7ef-149">Для iOS это порождает анимация «изменения» tooa которой приложение отправляется фона toohello во время проверки подлинности Microsoft приложения hello поставляется toohello переднего плана для пользователя tooselect hello учетную запись, которая как toosign с.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="7a7ef-150">Для Android и Windows учетная запись hello выбора отображается поверх вашего приложения, которое находится так сильно мешают toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="7a7ef-151">Получает вызов hello broker</span><span class="sxs-lookup"><span data-stu-id="7a7ef-151">How hello broker gets invoked</span></span>
<span data-ttu-id="7a7ef-152">Если совместимые broker установлено на устройстве hello, как hello приложения проверки подлинности Microsoft, hello пакеты SDK удостоверение будет автоматически hello рабочих вызова hello broker автоматически, когда пользователь указывает, что ими toolog любой учетной записью из Платформа Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="7a7ef-153">Это может быть личная учетная запись Майкрософт, рабочая или учебная учетная запись либо любая другая учетная запись, которую вы предоставили и разместили в Azure с использованием продуктов B2C и B2B.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="7a7ef-154">Как мы обеспечиваем hello приложения является допустимым</span><span class="sxs-lookup"><span data-stu-id="7a7ef-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="7a7ef-155">необходимость Hello tooensure удостоверением hello hello вызовов приложения-посредника является ключевым toohello безопасности, предоставляемых нами в входа компонента service broker вспомогательная.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="7a7ef-156">Не iOS и Android обеспечивает уникальные идентификаторы, которые допустимы только для данного приложения, вредоносные программы могут «спуфинг» идентификатор легальных приложений и получать токены hello предназначены для допустимых приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="7a7ef-157">tooensure, которым мы всегда связываются с правом приложения hello во время выполнения, мы просим tooprovide developer Привет пользовательских redirectURI при регистрации своих приложений с корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="7a7ef-158">**Ниже подробно описано, как разработчикам следует создавать этот универсальный код ресурса (URI) для перенаправления.**</span><span class="sxs-lookup"><span data-stu-id="7a7ef-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="7a7ef-159">Этот пользовательский redirectURI содержит hello ИД набора приложения hello и гарантируется toobe уникальный toohello приложения hello Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="7a7ef-160">Когда broker hello вызовов приложения, hello broker задает hello операций ввода-вывода операционной системы tooprovide его с Здравствуйте, идентификатор пакета, который вызывается hello broker.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="7a7ef-161">Hello broker предоставляет tooMicrosoft этот идентификатор пакета в системы удостоверений tooour вызов hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="7a7ef-162">Если hello ИД набора приложения hello не соответствует ИД набора предоставленного toous разработчиком hello во время регистрации приветствия, мы будет запрещать доступ toohello маркеры для запрашивает приложение hello hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="7a7ef-163">Эта проверка гарантирует, только приложение hello, зарегистрированные разработчиком hello получение маркеров.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="7a7ef-164">**Разработчик Hello имеет hello выбор, если hello пакет SDK для Microsoft Identity вызывает hello broker или использует службы помощи потока без посредника hello.**</span><span class="sxs-lookup"><span data-stu-id="7a7ef-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="7a7ef-165">Однако если hello разработчик выбирает не toouse hello вспомогательная broker потока потеряют hello преимущество использования учетных данных единого входа этого пользователя hello может уже присутствует на устройстве hello и предотвращает их приложения не могут использоваться с бизнес-функций Microsoft предоставляет клиентам как условного доступа, возможности управления Intune и проверку подлинности на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="7a7ef-166">Эти имена входа имеют hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7a7ef-167">Пользователь получает единого входа для всех приложений независимо от поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="7a7ef-168">Приложения можно использовать расширенные возможности бизнеса, например условный доступ или hello InTune набором продуктов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7a7ef-169">приложение может поддерживать аутентификацию бизнес-пользователей на основе сертификата;</span><span class="sxs-lookup"><span data-stu-id="7a7ef-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="7a7ef-170">Намного безопаснее входа пользователей как hello удостоверения приложения hello и hello пользователя проверяются hello broker приложения с помощью шифрования и алгоритмы дополнительной безопасности.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="7a7ef-171">Эти имена входа имеют следующие недостатки hello:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7a7ef-172">В iOS hello пользователь перешел из взаимодействие приложения пока выбираются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="7a7ef-173">Потеря toomanage hello hello возможность входа взаимодействия для клиентов в приложении.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="7a7ef-174">Вот представление как hello SDK удостоверений Майкрософт работают с hello компонента service broker приложения tooenable единого входа:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="7a7ef-175">Используя эти сведения в фоновом режиме должен быть toobetter может в изучении и реализации единого входа в приложении с помощью платформы Microsoft Identity hello и пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="7a7ef-176">Включение единого входа в нескольких приложениях с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="7a7ef-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="7a7ef-177">Здесь мы используем hello ADAL iOS SDK для:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="7a7ef-178">включение единого входа без помощи брокера для набора приложений;</span><span class="sxs-lookup"><span data-stu-id="7a7ef-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="7a7ef-179">включить поддержку единого входа с помощью брокера.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="7a7ef-180">Включение единого входа без брокера</span><span class="sxs-lookup"><span data-stu-id="7a7ef-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="7a7ef-181">Без посредника интерактивную единый вход для приложения hello пакеты SDK удостоверение управляет значительную часть сложности hello единого входа для.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="7a7ef-182">Сюда входят поиска правой пользователя hello в кэше hello и список пользователей, вошедший в систему для вас tooquery обслуживание.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="7a7ef-183">tooenable единого входа в приложениях, владеющих требуется hello toodo следующие:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="7a7ef-184">Убедитесь, все вашего приложения пользователя hello же идентификатор клиента или идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="7a7ef-185">Убедитесь, что все общей папке вашего приложения hello, же сертификатом для подписи у Apple, чтобы вы можете совместно использовать цепочки ключей</span><span class="sxs-lookup"><span data-stu-id="7a7ef-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="7a7ef-186">Запрос hello же правах цепочки ключей для всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="7a7ef-187">Сообщите, пакеты SDK удостоверение hello о цепочке ключей совместно hello что нам toouse.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="7a7ef-188">С помощью hello таким же Идентификатором клиента / идентификатор приложения для всех hello приложений в наборе приложений</span><span class="sxs-lookup"><span data-stu-id="7a7ef-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="7a7ef-189">Чтобы tooknow платформы Microsoft Identity hello допустимость его tooshare токены в приложениях каждое приложение потребуется hello tooshare же идентификатор клиента или идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="7a7ef-190">Это уникальный идентификатор hello, предоставленный tooyou при регистрации первого приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="7a7ef-191">Может возникнуть вопрос определяет различные приложения hello toohello службы Microsoft Identity, если он использует же идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="7a7ef-192">получен ответ Hello с hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="7a7ef-193">Каждое приложение может иметь несколько URI перенаправления зарегистрирован в портале адаптации hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="7a7ef-194">Каждое приложение в наборе получит уникальный код URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="7a7ef-195">Вот как это выглядит:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-195">An example of how this looks is below:</span></span>

<span data-ttu-id="7a7ef-196">URI перенаправления App1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="7a7ef-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="7a7ef-197">URI перенаправления App2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="7a7ef-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="7a7ef-198">URI перенаправления App3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="7a7ef-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="7a7ef-199">....</span><span class="sxs-lookup"><span data-stu-id="7a7ef-199">....</span></span>

<span data-ttu-id="7a7ef-200">Они располагаются под hello же идентификатор клиента и идентификатор приложения и hello найденное на основе URI перенаправления, который возвращается toous в конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="7a7ef-201">*Обратите внимание, что формат эти URI перенаправления hello описаны ниже. Может использовать любой URI перенаправления, если не нужно toosupport hello брокера, в противном случае они должны выглядеть примерно следующим образом выше hello*</span><span class="sxs-lookup"><span data-stu-id="7a7ef-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="7a7ef-202">Создание общей цепочки ключей между приложениями</span><span class="sxs-lookup"><span data-stu-id="7a7ef-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="7a7ef-203">Включение общего доступа к цепочке ключей выходит за рамки данного документа hello и связанная с Apple в своем документе [Добавление возможностей](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="7a7ef-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="7a7ef-204">Важно решить, какие действия следует к цепочке ключей, toobe вызывается и добавить эту возможность для всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="7a7ef-205">При наличии прав, настроить правильно, вы должны увидеть файл в папке проекта под названием `entitlements.plist` , содержащий нечто, похожее на следующее hello:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="7a7ef-206">Когда у вас есть права в цепочке ключей hello включен в каждое приложение и будут готовы toouse единого входа, расскажите hello пакет SDK для Microsoft Identity о цепочке ключей с помощью hello следующий параметр в вашей `ADAuthenticationSettings` с hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="7a7ef-207">При совместном использовании цепочке ключей в приложениях любого приложения можно удалить пользователей или хуже удалить все маркеры hello всего приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="7a7ef-208">Это особенно катастрофические при наличии приложений, использующих hello токены toodo фоновой работы.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="7a7ef-209">Общий доступ к цепочке ключей означает, что необходимо быть крайне внимательно в все Удаление операции с помощью пакетов SDK удостоверений Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="7a7ef-210">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="7a7ef-210">That's it!</span></span> <span data-ttu-id="7a7ef-211">пакет SDK для Microsoft Identity Hello теперь будут совместно использовать учетные данные для всех приложений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="7a7ef-212">список пользователей Hello также использоваться несколькими экземплярами приложений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="7a7ef-213">Включение единого входа с брокером</span><span class="sxs-lookup"><span data-stu-id="7a7ef-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="7a7ef-214">Здравствуйте, возможность toouse приложения является любой брокера, установленного на устройстве hello **отключена по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="7a7ef-215">Чтобы toouse приложения с помощью посредника hello необходимо выполнить дополнительные настройки и добавить некоторые приложения tooyour кода.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="7a7ef-216">Hello toofollow шаги являются:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="7a7ef-217">Включите режим брокера в код приложения вызов toohello MS SDK.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="7a7ef-218">Установить новый URI перенаправления, приложение hello tooboth и регистрации вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="7a7ef-219">Регистрация схемы URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="7a7ef-220">Поддержка iOS9: добавить файл info.plist tooyour разрешений.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="7a7ef-221">Шаг 1. Включение режима брокера в приложении</span><span class="sxs-lookup"><span data-stu-id="7a7ef-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="7a7ef-222">При создании hello «контекст» или начальной настройки проверки подлинности объекта включена возможность Hello broker hello toouse вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="7a7ef-223">Она выполняется путем настройки типа учетных данных в коде.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="7a7ef-224">Hello `AD_CREDENTIALS_AUTO` параметр разрешает toocall tootry пакет SDK для Microsoft Identity hello out toohello broker `AD_CREDENTIALS_EMBEDDED` предотвратит вызов toohello broker hello пакет SDK для Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="7a7ef-225">Шаг 2. Регистрация схемы URL-адреса</span><span class="sxs-lookup"><span data-stu-id="7a7ef-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="7a7ef-226">Платформа Microsoft Identity Hello использует broker hello tooinvoke URL-адреса и задней tooyour приложение затем возвращаемого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="7a7ef-227">toofinish этого цикла обработки требуется схема URL-адресов, зарегистрированных для приложения, hello известно о платформе Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="7a7ef-228">Это может быть также tooany других схем приложения, могут уже зарегистрированы с приложением.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="7a7ef-229">Рекомендуется, чтобы URL-адрес схемы довольно уникальный toominimize hello шансы на другое приложение, с помощью hello hello та же схема URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="7a7ef-230">Apple не обеспечивает уникальности hello схемы URL-адресов, которые зарегистрированы в хранилище приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="7a7ef-231">Ниже представлен пример того, как это показано в конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="7a7ef-232">Также это можно сделать в XCode:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="7a7ef-233">Шаг 3. Установка нового URI перенаправления в схеме URL-адреса</span><span class="sxs-lookup"><span data-stu-id="7a7ef-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="7a7ef-234">В tooensure порядке, что мы всегда возвращает правильного приложения toohello токены hello учетных данных мы должны toomake том, что мы обратного вызова, можно проверить tooyour приложения, в результате которого hello операционной системы iOS.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="7a7ef-235">Hello отчеты операционной системы iOS toohello приложений broker Майкрософт hello ИД набора приложения hello, его вызов.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="7a7ef-236">Стороннее приложение не может подделать его.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="7a7ef-237">Таким образом мы задействуем это вместе с URI нашей tooensure приложения брокера, возврат toohello правильного приложения hello токены hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="7a7ef-238">Нам требуется вы tooestablish этот уникальный URI, как в приложении и набор перенаправления как URI перенаправления в наших портала для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="7a7ef-239">В URI перенаправления должен быть hello правильный формат:</span><span class="sxs-lookup"><span data-stu-id="7a7ef-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="7a7ef-240">Пример: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="7a7ef-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="7a7ef-241">Этот URI перенаправления должен toobe, указанный в регистрации вашего приложения, с помощью hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7a7ef-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7a7ef-242">Дополнительные сведения о регистрации приложения Azure AD см. в статье, посвященной [интеграции с Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="7a7ef-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="7a7ef-243">Шаг 3a: Добавление URI перенаправления в приложении "и" Разработка портала toosupport на основе сертификатов проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="7a7ef-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="7a7ef-244">Проверка подлинности на основе сертификатов toosupport второй «msauth» должен toobe, зарегистрированные в приложении и hello [портал Azure](https://portal.azure.com/) toohandle при желании tooadd проверки подлинности сертификата, которые поддерживают в приложении.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="7a7ef-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="7a7ef-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="7a7ef-246">Шаг 4: iOS9: Добавление приложения tooyour параметр конфигурации</span><span class="sxs-lookup"><span data-stu-id="7a7ef-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="7a7ef-247">ADAL использует — canOpenURL: toocheck Если брокер hello установлен на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="7a7ef-248">В iOS 9 Apple заблокированы схемы, которые может запрашивать приложение.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="7a7ef-249">Вам потребуется tooadd «msauth» toohello LSApplicationQueriesSchemes части вашего `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="7a7ef-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="7a7ef-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="7a7ef-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="7a7ef-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="7a7ef-252">Вы настроили единый вход!</span><span class="sxs-lookup"><span data-stu-id="7a7ef-252">You've configured SSO!</span></span>
<span data-ttu-id="7a7ef-253">Теперь hello пакет SDK для Microsoft Identity автоматически и совместное использование учетных данных в приложениях и вызова неуправляемого кода hello broker при наличии на устройстве.</span><span class="sxs-lookup"><span data-stu-id="7a7ef-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

