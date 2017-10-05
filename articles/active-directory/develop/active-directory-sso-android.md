---
title: "Включение единого входа для нескольких приложений Android с помощью ADAL | Документация Майкрософт"
description: "Использование функций ADAL SDK для включения единого входа в приложениях. "
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
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="a9574-103">Как включить единый вход для нескольких приложений Android с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="a9574-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="a9574-104">Сегодня пользователи рассчитывают на возможность единого входа, позволяющую вводить учетные данные только один раз с последующим автоматическим входом в разные приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="a9574-105">Сложность ввода имени пользователя и пароля на маленьком экране, часто с дополнительной проверкой подлинности, например посредством звонка по телефону или кода в SMS, приводит к неудовлетворенности пользователя, если ему приходится это делать больше одного раза.</span><span class="sxs-lookup"><span data-stu-id="a9574-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="a9574-106">Кроме того, если вы используете платформу удостоверений, которую могут использовать другие приложения, например учетные записи Майкрософт или рабочую учетную запись Office 365, пользователи ожидают, что эти учетные данные будут доступны во всех приложениях любых поставщиков.</span><span class="sxs-lookup"><span data-stu-id="a9574-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="a9574-107">Платформа Microsoft Identity вместе с пакетом SDK для этой платформы делают всю сложную работу за вас, предоставляя пользователям возможность единого входа во все используемые вами приложения либо на всем устройстве (с помощью брокера и приложений Authenticator).</span><span class="sxs-lookup"><span data-stu-id="a9574-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="a9574-108">В этом пошаговом руководстве описывается, как настроить пакет SDK в приложении, чтобы ваши пользователи смогли воспользоваться этими преимуществами.</span><span class="sxs-lookup"><span data-stu-id="a9574-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="a9574-109">Руководство применимо при работе с такими службами:</span><span class="sxs-lookup"><span data-stu-id="a9574-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="a9574-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9574-110">Azure Active Directory</span></span>
* <span data-ttu-id="a9574-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="a9574-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="a9574-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a9574-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="a9574-113">Условный доступ к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9574-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="a9574-114">В представленном выше документе предполагается, что вы способны [подготовить приложения на устаревшем портале для Azure Active Directory](active-directory-how-to-integrate.md) и уже интегрировали приложение с [пакетом Android SDK для Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="a9574-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="a9574-115">Концепции единого входа на платформе Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="a9574-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="a9574-116">Брокеры Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="a9574-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="a9574-117">Корпорация Майкрософт предоставляет приложения для всех мобильных платформ, которые позволяют привязывать учетные данные к приложениям разных поставщиков и использовать специальные расширенные возможности, требующие единого безопасного расположения для проверки учетных данных.</span><span class="sxs-lookup"><span data-stu-id="a9574-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="a9574-118">Они называются **брокеры**.</span><span class="sxs-lookup"><span data-stu-id="a9574-118">We call these **brokers**.</span></span> <span data-ttu-id="a9574-119">В iOS и Android брокеры доступны в скачиваемых приложениях. Эти приложения пользователи устанавливают самостоятельно, либо их может передавать на устройство сотрудника компания, частично или полностью управляющая такими устройствами.</span><span class="sxs-lookup"><span data-stu-id="a9574-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="a9574-120">Брокеры поддерживают управление безопасностью только для некоторых приложений или для всего устройства в зависимости от требований ИТ-администраторов.</span><span class="sxs-lookup"><span data-stu-id="a9574-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="a9574-121">В Windows этот компонент предоставляется средством выбора учетной записи, встроенным в операционную систему (его техническое название — брокер веб-аутентификации).</span><span class="sxs-lookup"><span data-stu-id="a9574-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="a9574-122">Сведения о том, как мы используем эти брокеры и как они будут отображаться для пользователей при входе на платформу Microsoft Identity, приводятся дальше в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a9574-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="a9574-123">Способы входа на мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="a9574-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="a9574-124">Доступ к учетным данным на устройствах с поддержкой платформы Microsoft Identity осуществляется в рамках двух основных подходов:</span><span class="sxs-lookup"><span data-stu-id="a9574-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="a9574-125">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="a9574-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="a9574-126">вход с брокером.</span><span class="sxs-lookup"><span data-stu-id="a9574-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="a9574-127">вход без брокера;</span><span class="sxs-lookup"><span data-stu-id="a9574-127">Non-broker assisted logins</span></span>
<span data-ttu-id="a9574-128">Вход без брокера — это встроенная возможность входа в приложение с использованием локального хранилища на устройстве.</span><span class="sxs-lookup"><span data-stu-id="a9574-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="a9574-129">Хотя доступ к этом хранилищу может осуществляться из других приложений, учетные данные строго привязаны к использующему их приложению или набору приложений.</span><span class="sxs-lookup"><span data-stu-id="a9574-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="a9574-130">Скорее всего, вы уже встречали такой подход во многих мобильных приложениях, в которых имя пользователя и пароль вводятся непосредственно в приложении.</span><span class="sxs-lookup"><span data-stu-id="a9574-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="a9574-131">Такой способ входа отличается следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="a9574-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="a9574-132">пользовательский интерфейс полностью реализован в приложении;</span><span class="sxs-lookup"><span data-stu-id="a9574-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="a9574-133">учетные данные можно передавать в приложения, подписанные с использованием одного и того же сертификата, что создает возможность единого входа во все ваши приложения;</span><span class="sxs-lookup"><span data-stu-id="a9574-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="a9574-134">управление процедурой входа в рамках приложения возможно как до, так и после входа.</span><span class="sxs-lookup"><span data-stu-id="a9574-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="a9574-135">Такой способ входа имеет следующие недостатки:</span><span class="sxs-lookup"><span data-stu-id="a9574-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="a9574-136">единый вход будет доступен пользователю не во всех приложениях, в которых используются удостоверения Microsoft Identity, а только для тех удостоверений Microsoft Identity, которые настроены в вашем приложении;</span><span class="sxs-lookup"><span data-stu-id="a9574-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="a9574-137">нет возможности использовать для приложения расширенные бизнес-функции и компоненты, например условный доступ или набор продуктов InTune;</span><span class="sxs-lookup"><span data-stu-id="a9574-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="a9574-138">приложение не поддерживает аутентификацию бизнес-пользователей на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="a9574-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="a9574-139">Ниже показано, как с помощью пакетов SDK для Microsoft Identity можно включить единый вход, используя общее хранилище приложений.</span><span class="sxs-lookup"><span data-stu-id="a9574-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="a9574-140">Вход с брокером</span><span class="sxs-lookup"><span data-stu-id="a9574-140">Broker assisted logins</span></span>
<span data-ttu-id="a9574-141">Так называется вход, выполняемый в приложении брокера с использованием хранилища и системы безопасности брокера, который позволяет применить на устройстве один набор учетных данных для всех приложений, которые используют платформу Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a9574-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="a9574-142">Это означает, что ваши приложения используют брокер для входа пользователей в систему.</span><span class="sxs-lookup"><span data-stu-id="a9574-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="a9574-143">В iOS и Android брокеры доступны в виде скачиваемых приложений. Эти приложения устанавливаются пользователями самостоятельно либо принудительно передаются на устройство компанией, которая управляет устройствами.</span><span class="sxs-lookup"><span data-stu-id="a9574-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="a9574-144">Пример этого типа приложений — приложение Microsoft Authenticator в iOS.</span><span class="sxs-lookup"><span data-stu-id="a9574-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="a9574-145">В Windows этот компонент предоставляется средством выбора учетной записи, встроенным в операционную систему (его техническое название — брокер веб-проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="a9574-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="a9574-146">Этот способ входа зависит от платформы. При неправильном управлении он может мешать работе пользователей.</span><span class="sxs-lookup"><span data-stu-id="a9574-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="a9574-147">Возможно, вы знакомы с этим способом входа, если у вас установлено приложение Facebook и вы используете Facebook Connect для входа в другие приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="a9574-148">Платформа Microsoft Identity использует этот же принцип.</span><span class="sxs-lookup"><span data-stu-id="a9574-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="a9574-149">В iOS это реализовано в виде анимированного "перехода", в рамках которого ваше приложение переходит на задний план, а приложения Microsoft Authenticator — на передний, что позволяет пользователю выбрать учетную запись для входа.</span><span class="sxs-lookup"><span data-stu-id="a9574-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="a9574-150">В Android и Windows для удобства пользователя средство выбора учетной записи отображается поверх приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="a9574-151">Способы вызова брокера</span><span class="sxs-lookup"><span data-stu-id="a9574-151">How the broker gets invoked</span></span>
<span data-ttu-id="a9574-152">При установке совместимого брокера на устройство, например приложение Microsoft Authenticator, пакеты SDK Microsoft Identity автоматически будут выполнять вызов брокера, когда пользователь укажет, что хочет войти с помощью любой учетной записи платформы Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a9574-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="a9574-153">Это может быть личная учетная запись Майкрософт, рабочая или учебная учетная запись либо любая другая учетная запись, которую вы предоставили и разместили в Azure с использованием продуктов B2C и B2B.</span><span class="sxs-lookup"><span data-stu-id="a9574-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="a9574-154">Как мы проверяем, что приложение является допустимым</span><span class="sxs-lookup"><span data-stu-id="a9574-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="a9574-155">Идентификация приложений, обращающихся к брокеру, имеет решающее значение для обеспечения безопасности при входе с брокером.</span><span class="sxs-lookup"><span data-stu-id="a9574-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="a9574-156">Ни iOS, ни Android не предоставляют уникальные идентификаторы, действующие только для конкретного приложения. Это означает, что любое вредоносное ПО может имитировать идентификатор уполномоченного приложения и получать предназначенные для него маркеры.</span><span class="sxs-lookup"><span data-stu-id="a9574-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="a9574-157">Чтобы убедиться, что во время выполнения мы всегда взаимодействуем с надежным приложением, мы просим разработчиков при регистрации приложений в корпорации Майкрософт предоставлять собственный универсальный код ресурса (URI) для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="a9574-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="a9574-158">**Ниже подробно описано, как разработчику создать URI-адрес для перенаправления.**</span><span class="sxs-lookup"><span data-stu-id="a9574-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="a9574-159">Этот пользовательский URI для перенаправления содержит отпечаток сертификата приложения и служит уникальным идентификатором приложения в магазине Google Play.</span><span class="sxs-lookup"><span data-stu-id="a9574-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="a9574-160">Когда приложение вызывает брокер, тот запрашивает у операционной системы Android отпечаток сертификата, с которым был вызван этот брокер.</span><span class="sxs-lookup"><span data-stu-id="a9574-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="a9574-161">Затем брокер предоставляет этот отпечаток сертификата в корпорацию Майкрософт в рамках обращения к системе удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a9574-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="a9574-162">Если отпечаток сертификата, указанный приложением, не соответствует тому отпечатку сертификата, который разработчик предоставил нам во время регистрации, запрошенные приложением маркеры доступа к ресурсам не выдаются.</span><span class="sxs-lookup"><span data-stu-id="a9574-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="a9574-163">Такая проверка гарантирует, что только зарегистрированные разработчиком приложения получат маркеры.</span><span class="sxs-lookup"><span data-stu-id="a9574-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="a9574-164">**Разработчик может выбрать, будет ли SDK Microsoft Identity вызывать брокер или использовать поток без помощи брокера.**</span><span class="sxs-lookup"><span data-stu-id="a9574-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="a9574-165">Если разработчик не желает использовать последовательность с брокером, он не сможет предоставить пользователям единый вход с помощью учетных данных, уже добавленных на устройство. Кроме того, приложение не сможет использовать такие бизнес-функции корпорации Майкрософт, как условный доступ, возможности управления InTune и аутентификация на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="a9574-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="a9574-166">Такой способ входа отличается следующими преимуществами:</span><span class="sxs-lookup"><span data-stu-id="a9574-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="a9574-167">пользователь выполняет единый вход во всех приложениях независимо от поставщика;</span><span class="sxs-lookup"><span data-stu-id="a9574-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="a9574-168">в приложении можно использовать расширенные бизнес-функции и компоненты, включая условный доступ и набор продуктов InTune;</span><span class="sxs-lookup"><span data-stu-id="a9574-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="a9574-169">приложение может поддерживать аутентификацию бизнес-пользователей на основе сертификата;</span><span class="sxs-lookup"><span data-stu-id="a9574-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="a9574-170">более безопасная процедура входа — удостоверение приложения и пользователь проверяются приложением брокера с использованием шифрования и дополнительных алгоритмов безопасности.</span><span class="sxs-lookup"><span data-stu-id="a9574-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="a9574-171">Такой способ входа имеет следующие недостатки:</span><span class="sxs-lookup"><span data-stu-id="a9574-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="a9574-172">в iOS пользователь выходит из приложения во время выбора учетных данных;</span><span class="sxs-lookup"><span data-stu-id="a9574-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="a9574-173">невозможность управления процедурой входа пользователей в приложении.</span><span class="sxs-lookup"><span data-stu-id="a9574-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="a9574-174">Ниже показано, как с помощью пакетов SDK для Microsoft Identity можно включить единый вход, используя приложение брокера.</span><span class="sxs-lookup"><span data-stu-id="a9574-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="a9574-175">Теперь, вооружившись базовыми сведениями, вы сможете лучше понимать возможности единого входа и эффективнее реализовывать их в своем приложении с помощью платформы Microsoft Identity и пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="a9574-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="a9574-176">Включение единого входа в нескольких приложениях с помощью ADAL</span><span class="sxs-lookup"><span data-stu-id="a9574-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="a9574-177">Здесь мы с помощью пакета SDK ADAL для Android решим следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a9574-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="a9574-178">включение единого входа без помощи брокера для набора приложений;</span><span class="sxs-lookup"><span data-stu-id="a9574-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="a9574-179">включить поддержку единого входа с помощью брокера.</span><span class="sxs-lookup"><span data-stu-id="a9574-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="a9574-180">Включение единого входа без брокера</span><span class="sxs-lookup"><span data-stu-id="a9574-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="a9574-181">Когда для приложений включен единый вход без брокера, большей частью связанных с этой функцией процессов управляют пакеты SDK для Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="a9574-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="a9574-182">Сюда входит поиск нужного пользователя в кэше, а также хранение списка вошедших пользователей для выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="a9574-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="a9574-183">Включить единый вход для своих приложений можно так:</span><span class="sxs-lookup"><span data-stu-id="a9574-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="a9574-184">Убедитесь, что все приложения используют один идентификатор клиента или приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="a9574-185">Убедитесь, что все приложения имеют один набор SharedUserID.</span><span class="sxs-lookup"><span data-stu-id="a9574-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="a9574-186">Убедитесь, что все приложения используют один самозаверяющий сертификат из магазина Google Play для общего доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="a9574-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="a9574-187">Шаг 1. Использование одного идентификатора клиента или приложения для всех приложений в наборе</span><span class="sxs-lookup"><span data-stu-id="a9574-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="a9574-188">Чтобы платформа Microsoft Identity получила разрешение на использование в приложениях общих маркеров, всем этим приложениям нужно предоставить один и тот же идентификатор клиента или приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="a9574-189">Это уникальный идентификатор, предоставленный вам при регистрации первого приложения на портале.</span><span class="sxs-lookup"><span data-stu-id="a9574-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="a9574-190">Возможно, вы еще не знаете, как службе Microsoft Identity различать разные приложения, ведь она использует только один идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="a9574-191">Все дело в **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="a9574-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="a9574-192">Каждое приложение может иметь несколько кодов URI перенаправления, зарегистрированных на портале подключения.</span><span class="sxs-lookup"><span data-stu-id="a9574-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="a9574-193">Каждое приложение в наборе получит уникальный код URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="a9574-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="a9574-194">Вот как это выглядит:</span><span class="sxs-lookup"><span data-stu-id="a9574-194">An example of how this looks is below:</span></span>

<span data-ttu-id="a9574-195">URI перенаправления App1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="a9574-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="a9574-196">URI перенаправления App2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="a9574-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="a9574-197">URI перенаправления App3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="a9574-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="a9574-198">....</span><span class="sxs-lookup"><span data-stu-id="a9574-198">....</span></span>

<span data-ttu-id="a9574-199">Эти элементы вложены в один и тот же идентификатор клиента или приложения. Найти их можно по коду URI перенаправления, возвращаемого нам в конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="a9574-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="a9574-200">*Обратите внимание, что формат URI перенаправления представлен ниже. Вы можете использовать любой код URI перенаправления, если не хотите использовать брокер. В таком случае он будет выглядеть как показано выше.*</span><span class="sxs-lookup"><span data-stu-id="a9574-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="a9574-201">Шаг 2. Настройка общего хранилища в Android</span><span class="sxs-lookup"><span data-stu-id="a9574-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="a9574-202">Настройка идентификатора `SharedUserID` не описана в этом документе. См. соответствующие инструкции в документации по Google Android в разделе [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="a9574-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="a9574-203">Важно, что именно вы решаете, как следует назвать идентификатор sharedUserID, и используете его во всех ваших приложениях.</span><span class="sxs-lookup"><span data-stu-id="a9574-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="a9574-204">После того как вы добавите идентификатор `SharedUserID` во все свои приложения, вы сможете использовать единый вход.</span><span class="sxs-lookup"><span data-stu-id="a9574-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="a9574-205">Если вы предоставляете общий доступ к хранилищу всем своим приложениям, любое из них может удалить пользователей или, что еще хуже, все маркеры в приложении.</span><span class="sxs-lookup"><span data-stu-id="a9574-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="a9574-206">Это особенно катастрофично, если фоновая работа некоторых приложений зависит от токенов.</span><span class="sxs-lookup"><span data-stu-id="a9574-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="a9574-207">Общий доступ к хранилищу означает, что все операции удаления с помощью пакета SDK для Microsoft Identity теперь следует выполнять крайне осторожно.</span><span class="sxs-lookup"><span data-stu-id="a9574-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="a9574-208">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="a9574-208">That's it!</span></span> <span data-ttu-id="a9574-209">Теперь пакет SDK для Microsoft Identity передаст учетные данные во все приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="a9574-210">Кроме того, во все экземпляры приложений будет отправлен список пользователей.</span><span class="sxs-lookup"><span data-stu-id="a9574-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="a9574-211">Включение единого входа с брокером</span><span class="sxs-lookup"><span data-stu-id="a9574-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="a9574-212">Возможность приложения использовать любой брокер, который установлен на устройстве, **по умолчанию отключена**.</span><span class="sxs-lookup"><span data-stu-id="a9574-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="a9574-213">Чтобы пользоваться приложением с брокером, необходимо выполнить дополнительную настройку и добавить код в приложение.</span><span class="sxs-lookup"><span data-stu-id="a9574-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="a9574-214">Вот как это сделать:</span><span class="sxs-lookup"><span data-stu-id="a9574-214">The steps to follow are:</span></span>

1. <span data-ttu-id="a9574-215">Включите режим брокера в вызове пакета SDK MS, осуществляемом в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="a9574-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="a9574-216">Укажите новый код URI перенаправления для самого приложения и его регистрации.</span><span class="sxs-lookup"><span data-stu-id="a9574-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="a9574-217">Настройте требуемые разрешения в манифесте Android.</span><span class="sxs-lookup"><span data-stu-id="a9574-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="a9574-218">Шаг 1. Включение режима брокера в приложении</span><span class="sxs-lookup"><span data-stu-id="a9574-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="a9574-219">Возможность использовать в приложении брокер включается во время создания параметров или при первоначальной настройке экземпляра проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a9574-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="a9574-220">Это можно сделать, настроив тип ApplicationSettings в коде.</span><span class="sxs-lookup"><span data-stu-id="a9574-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="a9574-221">Шаг 2. Настройка нового кода URI перенаправления в схеме URL-адреса</span><span class="sxs-lookup"><span data-stu-id="a9574-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="a9574-222">Вы можете обеспечить возврат маркеров учетных данных в нужное приложение. Для этого нужно убедиться, что способ выполнения обратного вызова к приложению доступен для проверки операционной системой Android.</span><span class="sxs-lookup"><span data-stu-id="a9574-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="a9574-223">Операционная система Android использует хэш сертификата в магазине Google Play.</span><span class="sxs-lookup"><span data-stu-id="a9574-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="a9574-224">Стороннее приложение не сможет подделать его.</span><span class="sxs-lookup"><span data-stu-id="a9574-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="a9574-225">Следовательно, мы будем использовать его с кодом URI приложения брокера, обеспечивая тем самым возврат маркеров в нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="a9574-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="a9574-226">Вам нужно указать этот уникальный код URI перенаправления в приложении, а также выбрать его в качестве URI перенаправления на нашем портале разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a9574-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="a9574-227">Формат кода URI перенаправления должен быть таким:</span><span class="sxs-lookup"><span data-stu-id="a9574-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="a9574-228">Например, *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="a9574-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="a9574-229">Этот URI перенаправления должен быть указан при регистрации приложения на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9574-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a9574-230">Дополнительные сведения о регистрации приложения Azure AD см. в статье, посвященной [интеграции с Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="a9574-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="a9574-231">Шаг 3. Настройка требуемых разрешений в приложении</span><span class="sxs-lookup"><span data-stu-id="a9574-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="a9574-232">В нашем приложении брокера в Android используется функция диспетчера учетных записей ОС Android для управления учетными данными в разных приложениях.</span><span class="sxs-lookup"><span data-stu-id="a9574-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="a9574-233">Чтобы использовать брокер в приложении Android, ваш манифест приложения должен содержать разрешения на использование учетных записей AccountManager.</span><span class="sxs-lookup"><span data-stu-id="a9574-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="a9574-234">Дополнительные сведения об этом см. в [документации Google по использованию диспетчера учетных записей](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="a9574-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="a9574-235">Речь идет о следующих разрешениях:</span><span class="sxs-lookup"><span data-stu-id="a9574-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="a9574-236">Вы настроили единый вход!</span><span class="sxs-lookup"><span data-stu-id="a9574-236">You've configured SSO!</span></span>
<span data-ttu-id="a9574-237">Теперь пакет SDK для Microsoft Identity будет автоматически предоставлять учетные данные в приложения и вызывать брокера, если он есть на устройстве.</span><span class="sxs-lookup"><span data-stu-id="a9574-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

