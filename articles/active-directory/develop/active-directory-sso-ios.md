---
title: "Включение единого входа в нескольких приложениях в iOS с помощью ADAL | Документация Майкрософт"
description: "Использование функций ADAL SDK для включения единого входа в приложениях. "
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
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="4b9bf-103">Включение единого входа в нескольких приложениях iOS с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="4b9bf-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="4b9bf-104">Современные клиенты ожидают предоставления возможности единого входа, которая позволяет пользователям ввести учетные данные только один раз, после чего они смогут автоматически входить в разные приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="4b9bf-105">Сложность ввода имени пользователя и пароля на маленьком экране, часто с дополнительной проверкой подлинности, например посредством звонка по телефону или кода в SMS, приводит к неудовлетворенности пользователя, если ему приходится это делать больше одного раза.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="4b9bf-106">Кроме того, если вы используете платформу удостоверений, которую могут использовать другие приложения, например учетные записи Майкрософт или рабочую учетную запись Office 365, пользователи ожидают, что эти учетные данные будут доступны во всех приложениях любых поставщиков.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="4b9bf-107">Платформа Microsoft Identity вместе с пакетом SDK для этой платформы делают всю сложную работу за вас, предоставляя пользователям возможность единого входа во все используемые вами приложения либо на всем устройстве (с помощью брокера и приложений Authenticator).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="4b9bf-108">В этом пошаговом руководстве описывается, как настроить пакет SDK в приложении, чтобы ваши пользователи смогли воспользоваться этими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="4b9bf-109">Руководство применимо при работе с такими службами:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="4b9bf-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b9bf-110">Azure Active Directory</span></span>
* <span data-ttu-id="4b9bf-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="4b9bf-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="4b9bf-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="4b9bf-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="4b9bf-113">Условный доступ к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b9bf-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="4b9bf-114">В представленном выше документе предполагается, что вам известно, как [подготовить приложения на устаревшем портале для Azure Active Directory](active-directory-how-to-integrate.md), и вы уже интегрировали приложение с [пакетом SDK iOS для Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="4b9bf-115">Концепции единого входа на платформе Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="4b9bf-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="4b9bf-116">Брокеры Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="4b9bf-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="4b9bf-117">Корпорация Майкрософт предоставляет приложения для всех мобильных платформ, которые позволяют привязывать учетные данные к приложениям разных поставщиков и использовать специальные расширенные возможности, требующие единого безопасного расположения для проверки учетных данных.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="4b9bf-118">Они называются **брокеры**.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-118">We call these **brokers**.</span></span> <span data-ttu-id="4b9bf-119">В iOS и Android брокеры доступны в скачиваемых приложениях. Эти приложения пользователи устанавливают самостоятельно, либо их может передавать на устройство сотрудника компания, частично или полностью управляющая такими устройствами.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="4b9bf-120">Брокеры поддерживают управление безопасностью только для некоторых приложений или для всего устройства в зависимости от требований ИТ-администраторов.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="4b9bf-121">В Windows этот компонент предоставляется средством выбора учетной записи, встроенным в операционную систему (его техническое название — брокер веб-аутентификации).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="4b9bf-122">Сведения о том, как мы используем эти брокеры и как они будут отображаться для пользователей при входе на платформу Microsoft Identity, приводятся дальше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="4b9bf-123">Способы входа на мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="4b9bf-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="4b9bf-124">Доступ к учетным данным на устройствах с поддержкой платформы Microsoft Identity осуществляется в рамках двух основных подходов:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="4b9bf-125">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="4b9bf-126">вход с брокером.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="4b9bf-127">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-127">Non-broker assisted logins</span></span>
<span data-ttu-id="4b9bf-128">Вход без брокера — это встроенная возможность входа в приложение с использованием локального хранилища на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="4b9bf-129">Хотя доступ к этом хранилищу может осуществляться из других приложений, учетные данные строго привязаны к использующему их приложению или набору приложений.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="4b9bf-130">Скорее всего, вы уже встречали такой подход во многих мобильных приложениях, в которых имя пользователя и пароль вводятся непосредственно в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="4b9bf-131">Такой способ входа отличается следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="4b9bf-132">пользовательский интерфейс полностью реализован в приложении;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="4b9bf-133">учетные данные можно передавать в приложения, подписанные с использованием одного и того же сертификата, что создает возможность единого входа во все ваши приложения;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="4b9bf-134">управление процедурой входа в рамках приложения возможно как до, так и после входа.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="4b9bf-135">Такой способ входа имеет следующие недостатки:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="4b9bf-136">единый вход будет доступен пользователю не во всех приложениях, в которых используются удостоверения Microsoft Identity, а только для тех удостоверений Microsoft Identity, которые настроены в вашем приложении;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="4b9bf-137">нет возможности использовать для приложения расширенные бизнес-функции и компоненты, например условный доступ или набор продуктов InTune;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="4b9bf-138">приложение не поддерживает аутентификацию бизнес-пользователей на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="4b9bf-139">Ниже показано, как с помощью пакетов SDK для Microsoft Identity можно включить единый вход, используя общее хранилище приложений.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="4b9bf-140">Вход с брокером</span><span class="sxs-lookup"><span data-stu-id="4b9bf-140">Broker assisted logins</span></span>
<span data-ttu-id="4b9bf-141">Так называется вход, выполняемый в приложении брокера с использованием хранилища и системы безопасности брокера, который позволяет применить на устройстве один набор учетных данных для всех приложений, которые используют платформу Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="4b9bf-142">Это означает, что ваши приложения используют брокер для входа пользователей в систему.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="4b9bf-143">В iOS и Android брокеры доступны в виде скачиваемых приложений. Эти приложения устанавливаются пользователями самостоятельно либо принудительно передаются на устройство компанией, которая управляет устройствами.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="4b9bf-144">Пример этого типа приложений — приложение Microsoft Authenticator в iOS.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="4b9bf-145">В Windows этот компонент предоставляется средством выбора учетной записи, встроенным в операционную систему (его техническое название — брокер веб-проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="4b9bf-146">Этот способ входа зависит от платформы. При неправильном управлении он может мешать работе пользователей.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="4b9bf-147">Возможно, вы знакомы с этим способом входа, если у вас установлено приложение Facebook и вы используете Facebook Connect для входа в другие приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="4b9bf-148">Платформа Microsoft Identity использует этот же принцип.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="4b9bf-149">В iOS это реализовано в виде анимированного "перехода", в рамках которого ваше приложение переходит на задний план, а приложения Microsoft Authenticator — на передний, что позволяет пользователю выбрать учетную запись для входа.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="4b9bf-150">В Android и Windows для удобства пользователя средство выбора учетной записи отображается поверх приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="4b9bf-151">Способы вызова брокера</span><span class="sxs-lookup"><span data-stu-id="4b9bf-151">How the broker gets invoked</span></span>
<span data-ttu-id="4b9bf-152">При установке совместимого брокера на устройство, например приложение Microsoft Authenticator, пакеты SDK Microsoft Identity автоматически будут выполнять вызов брокера, когда пользователь укажет, что хочет войти с помощью любой учетной записи платформы Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="4b9bf-153">Это может быть личная учетная запись Майкрософт, рабочая или учебная учетная запись либо любая другая учетная запись, которую вы предоставили и разместили в Azure с использованием продуктов B2C и B2B.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="4b9bf-154">Как мы проверяем, что приложение является допустимым</span><span class="sxs-lookup"><span data-stu-id="4b9bf-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="4b9bf-155">Идентификация приложений, обращающихся к брокеру, имеет решающее значение для обеспечения безопасности при входе с брокером.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="4b9bf-156">Ни iOS, ни Android не предоставляют уникальные идентификаторы, действующие только для конкретного приложения. Это означает, что любое вредоносное ПО может имитировать идентификатор уполномоченного приложения и получать предназначенные для него маркеры.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="4b9bf-157">Чтобы убедиться, что во время выполнения мы всегда взаимодействуем с надежным приложением, мы просим разработчиков при регистрации приложений в корпорации Майкрософт предоставлять собственный универсальный код ресурса (URI) для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="4b9bf-158">**Ниже подробно описано, как разработчикам следует создавать этот универсальный код ресурса (URI) для перенаправления.**</span><span class="sxs-lookup"><span data-stu-id="4b9bf-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="4b9bf-159">Этот пользовательский универсальный код ресурса (URI) для перенаправления содержит идентификатор пакета, и его уникальность для приложения гарантируется магазином Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="4b9bf-160">Когда приложение вызывает брокер, он запрашивает у операционной системы iOS идентификатор пакета, с которым был вызван этот брокер.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="4b9bf-161">Затем брокер передает этот идентификатор пакета в корпорацию Майкрософт в вызове к системе удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="4b9bf-162">Если идентификатор пакета приложения не соответствует идентификатору пакета, который разработчик предоставил нам во время регистрации, то приложению будет отказано в выдаче запрашиваемых маркеров доступа к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="4b9bf-163">Такая проверка гарантирует, что только зарегистрированные разработчиком приложения получат маркеры.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="4b9bf-164">**Разработчик может выбрать, будет ли SDK Microsoft Identity вызывать брокер или использовать поток без помощи брокера.**</span><span class="sxs-lookup"><span data-stu-id="4b9bf-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="4b9bf-165">Если разработчик не желает использовать последовательность с брокером, он не сможет предоставить пользователям единый вход с помощью учетных данных, уже добавленных на устройство. Кроме того, приложение не сможет использовать такие бизнес-функции корпорации Майкрософт, как условный доступ, возможности управления InTune и аутентификация на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="4b9bf-166">Такой способ входа отличается следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="4b9bf-167">пользователь выполняет единый вход во всех приложениях независимо от поставщика;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="4b9bf-168">в приложении можно использовать расширенные бизнес-функции и компоненты, включая условный доступ и набор продуктов InTune;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="4b9bf-169">приложение может поддерживать аутентификацию бизнес-пользователей на основе сертификата;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="4b9bf-170">более безопасная процедура входа — удостоверение приложения и пользователь проверяются приложением брокера с использованием шифрования и дополнительных алгоритмов безопасности.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="4b9bf-171">Такой способ входа имеет следующие недостатки:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="4b9bf-172">в iOS пользователь выходит из приложения во время выбора учетных данных;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="4b9bf-173">невозможность управления процедурой входа пользователей в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="4b9bf-174">Ниже показано, как с помощью пакетов SDK для Microsoft Identity можно включить единый вход, используя приложение брокера.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="4b9bf-175">Теперь, вооружившись базовыми сведениями, вы сможете лучше понимать возможности единого входа и эффективнее реализовывать их в своем приложении с помощью платформы Microsoft Identity и пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="4b9bf-176">Включение единого входа в нескольких приложениях с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="4b9bf-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="4b9bf-177">Здесь пакет SDK iOS для ADAL используется в следующих целях:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="4b9bf-178">включение единого входа без помощи брокера для набора приложений;</span><span class="sxs-lookup"><span data-stu-id="4b9bf-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="4b9bf-179">включить поддержку единого входа с помощью брокера.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="4b9bf-180">Включение единого входа без брокера</span><span class="sxs-lookup"><span data-stu-id="4b9bf-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="4b9bf-181">Когда для приложений включен единый вход без брокера, большей частью связанных с этой функцией процессов управляют пакеты SDK для Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="4b9bf-182">Сюда входит поиск нужного пользователя в кэше, а также хранение списка вошедших пользователей для выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="4b9bf-183">Включить единый вход для своих приложений можно так:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="4b9bf-184">Убедитесь, что все приложения используют один идентификатор клиента или приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="4b9bf-185">Убедитесь, что все приложения имеют один и тот же самозаверяющий сертификат от Apple для общего доступа к цепочкам ключей.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="4b9bf-186">Запросите одинаковое назначение цепочки ключей для каждого из приложений.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="4b9bf-187">Сообщите SDK Microsoft Identity об общей цепочке ключей, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="4b9bf-188">Использование одного идентификатора клиента или приложения для всех приложений в наборе</span><span class="sxs-lookup"><span data-stu-id="4b9bf-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="4b9bf-189">Чтобы платформа Microsoft Identity получила разрешение на использование общих токенов в приложениях, каждому из приложений потребуется предоставить один идентификатор клиента или приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="4b9bf-190">Это уникальный идентификатор, предоставленный вам при регистрации первого приложения на портале.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="4b9bf-191">Возможно, вы еще не знаете, как службе Microsoft Identity различать разные приложения, ведь она использует только один идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="4b9bf-192">Все дело в **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="4b9bf-193">Каждое приложение может иметь несколько кодов URI перенаправления, зарегистрированных на портале подключения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="4b9bf-194">Каждое приложение в наборе получит уникальный код URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="4b9bf-195">Вот как это выглядит:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-195">An example of how this looks is below:</span></span>

<span data-ttu-id="4b9bf-196">URI перенаправления App1: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="4b9bf-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="4b9bf-197">URI перенаправления App2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="4b9bf-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="4b9bf-198">URI перенаправления App3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="4b9bf-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="4b9bf-199">....</span><span class="sxs-lookup"><span data-stu-id="4b9bf-199">....</span></span>

<span data-ttu-id="4b9bf-200">Эти элементы вложены в один и тот же идентификатор клиента или приложения. Найти их можно по коду URI перенаправления, возвращаемого нам в конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="4b9bf-201">*Обратите внимание, что формат URI перенаправления представлен ниже. Вы можете использовать любой URI перенаправления, если не хотите поддерживать брокера: в этом случае он будет выглядеть, как показано выше*</span><span class="sxs-lookup"><span data-stu-id="4b9bf-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="4b9bf-202">Создание общей цепочки ключей между приложениями</span><span class="sxs-lookup"><span data-stu-id="4b9bf-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="4b9bf-203">Включение общей цепочки ключей не описано в этом документе. См. документ Apple [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) (Добавление возможностей).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="4b9bf-204">Важно, что именно вы решаете, как следует назвать цепочку ключей, и добавляете эту возможность во всех приложениях.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="4b9bf-205">Если у вас правильно настроены назначения, в каталоге проекта появится файл `entitlements.plist`, содержимое которого аналогично следующему:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

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

<span data-ttu-id="4b9bf-206">Если вы включили назначение цепочки ключей в каждом из приложений и готовы использовать единый вход, используйте цепочку ключей в пакете SDK Microsoft Identity в `ADAuthenticationSettings` с помощью следующего параметра:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="4b9bf-207">При предоставлении цепочки ключей в приложениях любое приложение может удалить пользователей или даже все токены в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="4b9bf-208">Это особенно катастрофично, если фоновая работа некоторых приложений зависит от токенов.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="4b9bf-209">Общий доступ к цепочке ключей означает, что вы должны быть очень аккуратны при операциях удаления, выполняемых через SDK Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="4b9bf-210">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="4b9bf-210">That's it!</span></span> <span data-ttu-id="4b9bf-211">Теперь пакет SDK для Microsoft Identity передаст учетные данные во все приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="4b9bf-212">Кроме того, во все экземпляры приложений будет отправлен список пользователей.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="4b9bf-213">Включение единого входа с брокером</span><span class="sxs-lookup"><span data-stu-id="4b9bf-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="4b9bf-214">Возможность приложения использовать любой брокер, который установлен на устройстве, **по умолчанию отключена**.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="4b9bf-215">Чтобы пользоваться приложением с брокером, необходимо выполнить дополнительную настройку и добавить код в приложение.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="4b9bf-216">Шаги для выполнения:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-216">The steps to follow are:</span></span>

1. <span data-ttu-id="4b9bf-217">Включите режим брокера в вызове MS SDK кода приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="4b9bf-218">Установите новый URI перенаправления и предоставьте его приложению и для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="4b9bf-219">Регистрация схемы URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="4b9bf-220">Поддержка iOS9: добавление разрешения в файл info.plist.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="4b9bf-221">Шаг 1. Включение режима брокера в приложении</span><span class="sxs-lookup"><span data-stu-id="4b9bf-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="4b9bf-222">Возможность для приложения использовать брокера включена при создании "контекста" и первоначальной настройке объекта проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="4b9bf-223">Она выполняется путем настройки типа учетных данных в коде.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="4b9bf-224">Параметр `AD_CREDENTIALS_AUTO` разрешает пакету SDK Microsoft Identity вызывать брокер, а `AD_CREDENTIALS_EMBEDDED` запрещает пакету SDK Microsoft Identity вызывать брокер.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="4b9bf-225">Шаг 2. Регистрация схемы URL-адреса</span><span class="sxs-lookup"><span data-stu-id="4b9bf-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="4b9bf-226">Платформа Microsoft Identity использует URL-адреса для вызова брокера, а затем возвращает элемент управления в приложение.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="4b9bf-227">Чтобы завершить этот цикл, требуется схема URL-адреса, зарегистрированная для приложения, о котором платформа Microsoft Identity узнает.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="4b9bf-228">Она может быть дополнением к другим схемам безопасности, которые вы зарегистрировали в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="4b9bf-229">Рекомендуется сделать схему URL-адреса уникальной, чтобы свести к минимуму вероятность использования той же схемы URL-адреса другим приложением.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="4b9bf-230">Apple не обеспечивает уникальность схем URL-адреса, зарегистрированных в магазине приложений.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="4b9bf-231">Ниже представлен пример того, как это показано в конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="4b9bf-232">Также это можно сделать в XCode:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-232">You may also do this in XCode as well:</span></span>

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

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="4b9bf-233">Шаг 3. Установка нового URI перенаправления в схеме URL-адреса</span><span class="sxs-lookup"><span data-stu-id="4b9bf-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="4b9bf-234">Чтобы обеспечить обязательный возврат токенов учетных данных в нужное приложение, необходимо убедиться, что мы выполняем обратный вызов в приложение таким способом, который операционная система iOS может проверить.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="4b9bf-235">Операционная система iOS передает идентификатор набора вызывающего приложения в приложения брокера Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="4b9bf-236">Стороннее приложение не может подделать его.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="4b9bf-237">Следовательно, мы будем использовать его с кодом URI приложения брокера, обеспечивая тем самым возврат маркеров в нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="4b9bf-238">Вам нужно указать этот уникальный код URI перенаправления в приложении, а также выбрать его в качестве URI перенаправления на нашем портале разработчиков.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="4b9bf-239">Формат кода URI перенаправления должен быть таким:</span><span class="sxs-lookup"><span data-stu-id="4b9bf-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="4b9bf-240">Пример: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="4b9bf-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="4b9bf-241">Этот URI перенаправления должен быть указан при регистрации приложения на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4b9bf-242">Дополнительные сведения о регистрации приложения Azure AD см. в статье, посвященной [интеграции с Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="4b9bf-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="4b9bf-243">Шаг 3а. Добавление URI перенаправления в приложение и на портал разработчика для поддержки проверки подлинности на основе сертификатов</span><span class="sxs-lookup"><span data-stu-id="4b9bf-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="4b9bf-244">Чтобы обеспечить аутентификацию на основе сертификата, необходимо зарегистрировать второй файл msauth в приложении и на [портале Azure](https://portal.azure.com/) для обработки аутентификации сертификатов, если вы хотите добавить эту поддержку в приложение.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="4b9bf-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="4b9bf-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="4b9bf-246">Шаг 4. iOS9: добавление параметра конфигурации в приложение</span><span class="sxs-lookup"><span data-stu-id="4b9bf-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="4b9bf-247">ADAL использует –canOpenURL для проверки того, установлен ли брокер на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="4b9bf-248">В iOS 9 Apple заблокированы схемы, которые может запрашивать приложение.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="4b9bf-249">Вам потребуется вручную добавить msauth в раздел LSApplicationQueriesSchemes файла `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="4b9bf-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="4b9bf-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="4b9bf-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="4b9bf-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="4b9bf-252">Вы настроили единый вход!</span><span class="sxs-lookup"><span data-stu-id="4b9bf-252">You've configured SSO!</span></span>
<span data-ttu-id="4b9bf-253">Теперь пакет SDK для Microsoft Identity будет автоматически предоставлять учетные данные в приложения и вызывать брокера, если он есть на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4b9bf-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

