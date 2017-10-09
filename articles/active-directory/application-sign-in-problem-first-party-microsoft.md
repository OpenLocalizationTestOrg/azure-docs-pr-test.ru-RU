---
title: "вход в приложение Microsoft tooa aaaProblems | Документы Microsoft"
description: "Устранение общих проблем, возникающих при входе в toofirst сторонних приложений Майкрософт, с помощью Azure AD (например, Office 365)"
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="f75ec-103">Проблемы со входом в приложение Microsoft tooa</span><span class="sxs-lookup"><span data-stu-id="f75ec-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="f75ec-104">Приложения Майкрософт (такие как Office 365 Exchange, SharePoint, Yammer и т. д.) назначаются и управляются немного иначе, чем приложения SaaS от сторонних разработчиков и другие приложения, которые вы интегрируете с Azure AD для единого входа.</span><span class="sxs-lookup"><span data-stu-id="f75ec-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="f75ec-105">Существует три основных способа, пользователь сможет получить доступ tooa Корпорация Майкрософт опубликовала приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="f75ec-106">Для приложений в hello Office 365 или другие платные наборы пользователям разрешен доступ через **лицензии назначения** либо непосредственно tootheir учетной записи пользователя, или с помощью в группу с помощью наших возможность назначения лицензий на основе групп.</span><span class="sxs-lookup"><span data-stu-id="f75ec-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="f75ec-107">Для приложений, что Майкрософт или третьей стороной публикует свободно для тех, кто toouse, пользователи могут получать доступ через **согласие пользователя**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="f75ec-108">This0 означает, что они toohello приложения с помощью Azure AD или рабочей учетной записи входа и разрешить toohave доступа toosome ограниченный набор данных на свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f75ec-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="f75ec-109">Для приложений, что Майкрософт или сторонних производителей публикует свободно для тех, кто toouse, пользователи могут также иметь доступ через **согласия администратора**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="f75ec-110">Это означает, что администратор определяет, что приложение hello может использоваться всем пользователям в организации hello, поэтому они войти в приложение toohello с учетной записью глобального администратора и предоставить доступ tooeveryone в организации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="f75ec-111">tootroubleshoot свою проблему, начинаются с Привет [общие проблемные области с tooconsider доступ к приложению](#general-problem-areas-with-application-access-to-consider) и затем прочитать hello [Пошаговое руководство: tootroubleshoot действия приложения Microsoft access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget сведения о hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="f75ec-112">Общие проблемные области с tooconsider доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="f75ec-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="f75ec-113">Ниже приведен список hello общие проблемные области, которые вы можете перейти в, если у вас о том, где toostart, но мы рекомендуем прочитать hello tooget Пошаговое руководство, как быстро: [Пошаговое руководство: tootroubleshoot действия приложения Microsoft access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="f75ec-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="f75ec-114">Проблемы с учетной записью пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f75ec-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="f75ec-115">Проблемы с группами</span><span class="sxs-lookup"><span data-stu-id="f75ec-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="f75ec-116">Проблемы с политиками условного доступа</span><span class="sxs-lookup"><span data-stu-id="f75ec-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="f75ec-117">Проблемы с согласием для приложений</span><span class="sxs-lookup"><span data-stu-id="f75ec-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="f75ec-118">Tootroubleshoot действия приложения Microsoft access</span><span class="sxs-lookup"><span data-stu-id="f75ec-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="f75ec-119">Ниже некоторые распространенные проблемы люди выполняются в при пользователей не сможет войти в приложение Microsoft tooa.</span><span class="sxs-lookup"><span data-stu-id="f75ec-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="f75ec-120">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="f75ec-120">General issues toocheck first</span></span>

  * <span data-ttu-id="f75ec-121">Убедитесь, что пользователь hello, вход toohello **исправьте URL-адрес** не URL- адрес локального приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="f75ec-122">Убедитесь, что учетная запись пользователя hello **не заблокирована.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="f75ec-123">Убедитесь, что hello **учетная запись пользователя существует** в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f75ec-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="f75ec-124">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f75ec-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="f75ec-125">Убедитесь, что учетная запись пользователя hello **включен** для входа. [Проверка состояния учетной записи пользователя](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="f75ec-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="f75ec-126">Убедитесь, что пользователь hello **не просрочен или забудете пароль.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="f75ec-127">[Сброс пароля пользователя](#reset-a-users-password) или [Включение самостоятельного сброса пароля](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="f75ec-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="f75ec-128">Проверьте, не блокирует ли **Многофакторная идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f75ec-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="f75ec-129">[Проверка состояния службы Многофакторной идентификации](#check-a-users-multi-factor-authentication-status) или [Проверка контактной информации для проверки подлинности](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="f75ec-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="f75ec-130">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f75ec-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="f75ec-131">[Проверка конкретной политики условного доступа](#problems-with-conditional-access-policies), [Проверка политики условного доступа для конкретного приложения](#check-a-specific-applications-conditional-access-policy) или [Отключение конкретной политики условного доступа](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="f75ec-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="f75ec-132">Убедитесь, что пользователь **контактные сведения для проверки подлинности** работает toodate tooallow многофакторной проверки подлинности или условного доступа политики toobe принудительно.</span><span class="sxs-lookup"><span data-stu-id="f75ec-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="f75ec-133">[Проверка состояния службы Многофакторной идентификации](#check-a-users-multi-factor-authentication-status) или [Проверка контактной информации для проверки подлинности](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="f75ec-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="f75ec-134">Для **Microsoft** **приложений, которым требуется лицензия** (например, Office 365), Вот некоторые конкретные проблемы toocheck после исключить hello общие вопросы, описанные выше:</span><span class="sxs-lookup"><span data-stu-id="f75ec-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="f75ec-135">Обеспечить hello пользователя или имеет **назначена лицензия.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="f75ec-136">[Проверка назначенных пользователю лицензий](#check-a-users-assigned-licenses) или [Проверка назначенных группе лицензий](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="f75ec-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="f75ec-137">Если лицензия hello **назначенный tooa** **Статическая группа**, убедитесь, что hello **пользователь является членом** этой группы.</span><span class="sxs-lookup"><span data-stu-id="f75ec-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="f75ec-138">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="f75ec-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="f75ec-139">Если лицензия hello **назначенный tooa** **динамическую группу**, убедитесь, что hello **динамическая группа правил имеет правильное значение**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="f75ec-140">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="f75ec-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="f75ec-141">Если лицензия hello **назначенный tooa** **динамическую группу**, убедитесь, что hello в динамической группе есть **завершения обработки** членство и что hello **пользователь член** (это может занять некоторое время).</span><span class="sxs-lookup"><span data-stu-id="f75ec-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="f75ec-142">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="f75ec-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="f75ec-143">После назначения лицензии hello, убедитесь, что лицензия hello **не истек**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="f75ec-144">Убедитесь, что лицензия hello **для приложения hello** они обращаются.</span><span class="sxs-lookup"><span data-stu-id="f75ec-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="f75ec-145">Для **Microsoft** **приложений, которым не требуется лицензия**, Вот некоторые другие вещи toocheck:</span><span class="sxs-lookup"><span data-stu-id="f75ec-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="f75ec-146">Если приложение hello запрашивает **разрешения уровня пользователя** (например «доступ к почтовый ящик этого пользователя»), убедитесь, что этот пользователь hello вход в приложение toohello и выполнил **операции разрешения уровня пользователя**  приложения hello toolet доступ к ее данным.</span><span class="sxs-lookup"><span data-stu-id="f75ec-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="f75ec-147">Если приложение hello запрашивает **разрешения уровня администратора** (например «доступ к почтовым ящикам пользователей все»), убедитесь, что выполнены глобального администратора **операции разрешения уровня администратора имени все пользователей** в организации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="f75ec-148">Проблемы с учетной записью пользователя hello</span><span class="sxs-lookup"><span data-stu-id="f75ec-148">Problems with hello user’s account</span></span>

<span data-ttu-id="f75ec-149">Доступ к приложению может быть заблокирована из-за проблемы tooa с пользователем, который назначается toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="f75ec-150">Ниже приведены некоторые способы устранения неполадок, связанных с параметрами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="f75ec-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="f75ec-151">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f75ec-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="f75ec-152">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="f75ec-153">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="f75ec-154">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="f75ec-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="f75ec-155">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="f75ec-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="f75ec-156">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f75ec-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="f75ec-157">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="f75ec-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="f75ec-158">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="f75ec-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="f75ec-159">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="f75ec-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="f75ec-160">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f75ec-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="f75ec-161">toocheck, если учетная запись пользователя отсутствует, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-162">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-163">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-164">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-165">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-166">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-166">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-167">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-168">Проверьте свойства hello hello пользователя объекта toobe убедиться, что они выглядят как предполагается, что и данные не отсутствует.</span><span class="sxs-lookup"><span data-stu-id="f75ec-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="f75ec-169">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-169">Check a user’s account status</span></span>

<span data-ttu-id="f75ec-170">toocheck пользователя состояние учетной записи, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-171">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-172">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-173">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-174">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-175">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-175">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-176">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-177">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-177">click **Profile**.</span></span>

8.  <span data-ttu-id="f75ec-178">В разделе **параметры** убедитесь, что **входа блока** задано слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="f75ec-179">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-179">Reset a user’s password</span></span>

<span data-ttu-id="f75ec-180">tooreset пароль пользователя, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-181">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-182">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-183">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-184">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-185">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-185">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-186">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-187">Нажмите кнопку hello **сброс пароля** кнопку hello верхней части колонки hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="f75ec-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="f75ec-188">Нажмите кнопку hello **сброс пароля** кнопку на hello **сброс пароля** колонки, отображается.</span><span class="sxs-lookup"><span data-stu-id="f75ec-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="f75ec-189">Копировать hello **временный пароль** или **ввести новый пароль** для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="f75ec-190">Связь этого нового пользователя toohello пароль, они необходимые toochange этот пароль во время следующего входа в tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f75ec-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="f75ec-191">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="f75ec-191">Enable self-service password reset</span></span>

<span data-ttu-id="f75ec-192">tooenable пароль самостоятельного сброса, выполните следующие действия развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="f75ec-193">Включение пользователей tooreset свои пароли с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f75ec-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="f75ec-194">Включить tooreset пользователей или изменить свои пароли в локальной среде Active Directory</span><span class="sxs-lookup"><span data-stu-id="f75ec-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="f75ec-195">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="f75ec-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="f75ec-196">toocheck пользователь многофакторной проверки подлинности состояние, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-197">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-198">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-199">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-200">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-201">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-201">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-202">Нажмите кнопку hello **многофакторной проверки подлинности** кнопку hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="f75ec-203">Здравствуйте, один раз **портала администрирования многофакторной проверки подлинности** загрузок, убедитесь в hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="f75ec-204">Найти hello пользователя в список пользователей hello, поиск, фильтрацию или сортировку.</span><span class="sxs-lookup"><span data-stu-id="f75ec-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="f75ec-205">Выберите hello пользователя из списка пользователей hello и **включить**, **отключить**, или **принудительное применение** многофакторной проверки подлинности в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="f75ec-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="f75ec-206">**Примечание**: Если пользователь входит в **принудительно** состоянии, можно установить их слишком**отключено** временно toolet их обратно в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="f75ec-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="f75ec-207">После их обратно в, можно изменить свое состояние слишком**включено** снова toorequire их toore-register свои контактные данные во время следующего входа.</span><span class="sxs-lookup"><span data-stu-id="f75ec-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="f75ec-208">Кроме того, можно выполнить действия hello в hello [проверьте контактные данные для проверки подлинности пользователя](#check-a-users-authentication-contact-info) tooverify или задать для них эти данные.</span><span class="sxs-lookup"><span data-stu-id="f75ec-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="f75ec-209">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f75ec-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="f75ec-210">toocheck проверку подлинности пользователя с контактные данные, для многофакторной проверки подлинности, условный доступ, защиту учетных данных и сброса пароля, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-211">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-212">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-213">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-214">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-215">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-215">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-216">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-217">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-217">click **Profile**.</span></span>

8.  <span data-ttu-id="f75ec-218">Прокрутите список вниз слишком**контактные сведения для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="f75ec-219">**Просмотрите** hello данных, зарегистрированных для пользователя hello и обновление при необходимости.</span><span class="sxs-lookup"><span data-stu-id="f75ec-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="f75ec-220">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="f75ec-220">Check a user’s group memberships</span></span>

<span data-ttu-id="f75ec-221">toocheck пользователя членство в группе, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-222">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-223">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-224">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-225">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-226">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-226">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-227">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-228">Нажмите кнопку **группы** toosee, который группирует hello пользователь является членом.</span><span class="sxs-lookup"><span data-stu-id="f75ec-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="f75ec-229">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="f75ec-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="f75ec-230">toocheck пользователя назначить лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-231">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-232">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-233">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-234">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-235">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-235">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-236">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-237">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="f75ec-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="f75ec-238">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="f75ec-238">Assign a user a license</span></span> 

<span data-ttu-id="f75ec-239">tooassign пользователь tooa лицензии, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-240">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-241">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-242">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-243">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-244">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-244">click **All users**.</span></span>

6.  <span data-ttu-id="f75ec-245">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-246">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="f75ec-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="f75ec-247">Нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="f75ec-248">Выберите **один или несколько продуктов** из списка допустимых продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="f75ec-249">**Необязательный** щелкните hello **параметры назначения** toogranularly элемента назначить продукты.</span><span class="sxs-lookup"><span data-stu-id="f75ec-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="f75ec-250">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="f75ec-251">Нажмите кнопку hello **назначить** кнопку tooassign toothis эти лицензии пользователя.</span><span class="sxs-lookup"><span data-stu-id="f75ec-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="f75ec-252">Проблемы с группами</span><span class="sxs-lookup"><span data-stu-id="f75ec-252">Problems with groups</span></span>

<span data-ttu-id="f75ec-253">Доступ к приложению может быть заблокирована из-за tooa проблему с группой, которая назначается toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="f75ec-254">Ниже приведены некоторые способы для устранения неполадок, связанных с группами и членством в них.</span><span class="sxs-lookup"><span data-stu-id="f75ec-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="f75ec-255">Проверка членства в группе</span><span class="sxs-lookup"><span data-stu-id="f75ec-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="f75ec-256">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="f75ec-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="f75ec-257">Проверка назначенных группе лицензий</span><span class="sxs-lookup"><span data-stu-id="f75ec-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="f75ec-258">Повторная обработка лицензий группы</span><span class="sxs-lookup"><span data-stu-id="f75ec-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="f75ec-259">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="f75ec-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="f75ec-260">Проверка членства в группе</span><span class="sxs-lookup"><span data-stu-id="f75ec-260">Check a group’s membership</span></span>

<span data-ttu-id="f75ec-261">toocheck членство в группе, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-262">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-263">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-264">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-265">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-266">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-266">click **All groups**.</span></span>

6.  <span data-ttu-id="f75ec-267">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-268">Нажмите кнопку **элементы** toothis группу назначить tooreview hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="f75ec-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="f75ec-269">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="f75ec-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="f75ec-270">toocheck условия членства динамическую группу, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-271">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-272">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-273">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-274">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-275">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-275">click **All groups**.</span></span>

6.  <span data-ttu-id="f75ec-276">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-277">Щелкните **Правила динамического членства**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="f75ec-278">Просмотрите hello **простой** или **Дополнительно** правила, определенные для этой группы и убедитесь, этот пользователь hello требуется toobe членом этой группы соответствовал этим критериям.</span><span class="sxs-lookup"><span data-stu-id="f75ec-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="f75ec-279">Проверка назначенных группе лицензий</span><span class="sxs-lookup"><span data-stu-id="f75ec-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="f75ec-280">toocheck группы назначенные лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-281">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-282">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-283">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-284">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-285">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-285">click **All groups**.</span></span>

6.  <span data-ttu-id="f75ec-286">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-287">Нажмите кнопку **лицензий** toosee, какую группу hello лицензии в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="f75ec-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="f75ec-288">Повторная обработка лицензий группы</span><span class="sxs-lookup"><span data-stu-id="f75ec-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="f75ec-289">tooreprocess группы назначенные лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="f75ec-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-290">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-291">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-292">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-293">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-294">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-294">click **All groups**.</span></span>

6.  <span data-ttu-id="f75ec-295">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-296">Нажмите кнопку **лицензий** toosee, какую группу hello лицензии в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="f75ec-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="f75ec-297">Нажмите кнопку hello **повторно обработать** tooensure кнопки, hello членов группы toothis лицензии обновлены.</span><span class="sxs-lookup"><span data-stu-id="f75ec-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="f75ec-298">Это может занять много времени, в зависимости от hello размера и сложности hello группы.</span><span class="sxs-lookup"><span data-stu-id="f75ec-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f75ec-299">toodo это быстрее, рассмотрите возможность временно назначение лицензии пользователя toohello напрямую.</span><span class="sxs-lookup"><span data-stu-id="f75ec-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="f75ec-300">[Назначение лицензии пользователю](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="f75ec-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="f75ec-301">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="f75ec-301">Assign a group a license</span></span>

<span data-ttu-id="f75ec-302">tooassign tooa в лицензионную группу, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="f75ec-303">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-304">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-305">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-306">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-307">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-307">click **All groups**.</span></span>

6.  <span data-ttu-id="f75ec-308">**Поиск** для hello группы, которые вас интересуют и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="f75ec-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="f75ec-309">Нажмите кнопку **лицензий** toosee, какую группу hello лицензии в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="f75ec-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="f75ec-310">Нажмите кнопку hello **назначить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="f75ec-311">Выберите **один или несколько продуктов** из списка допустимых продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="f75ec-312">**Необязательный** щелкните hello **параметры назначения** toogranularly элемента назначить продукты.</span><span class="sxs-lookup"><span data-stu-id="f75ec-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="f75ec-313">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="f75ec-314">Нажмите кнопку hello **назначить** кнопку tooassign группы toothis эти лицензии.</span><span class="sxs-lookup"><span data-stu-id="f75ec-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="f75ec-315">Это может занять много времени, в зависимости от hello размера и сложности hello группы.</span><span class="sxs-lookup"><span data-stu-id="f75ec-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f75ec-316">toodo это быстрее, рассмотрите возможность временно назначение лицензии пользователя toohello напрямую.</span><span class="sxs-lookup"><span data-stu-id="f75ec-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="f75ec-317">[Назначение лицензии пользователю](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="f75ec-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="f75ec-318">Проблемы с политиками условного доступа</span><span class="sxs-lookup"><span data-stu-id="f75ec-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="f75ec-319">Проверка конкретной политики условного доступа</span><span class="sxs-lookup"><span data-stu-id="f75ec-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="f75ec-320">toocheck или проверить политику одного условного доступа:</span><span class="sxs-lookup"><span data-stu-id="f75ec-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="f75ec-321">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-322">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-323">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-324">Нажмите кнопку **корпоративных приложений** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-325">Нажмите кнопку hello **условного доступа** элемент навигации.</span><span class="sxs-lookup"><span data-stu-id="f75ec-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="f75ec-326">Выберите политику hello, вас интересует изучение.</span><span class="sxs-lookup"><span data-stu-id="f75ec-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="f75ec-327">Убедитесь, что нет никаких условий, назначений или других параметров, которые могут блокировать доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f75ec-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="f75ec-328">Вы можете отключить tootemporarily tooensure этой политики, она не влияет на toodo входа очередном hello, этот набор **включить политику** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки .</span><span class="sxs-lookup"><span data-stu-id="f75ec-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="f75ec-329">Проверка политики условного доступа для конкретного приложения</span><span class="sxs-lookup"><span data-stu-id="f75ec-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="f75ec-330">toocheck или проверить политику одно приложение в настоящий момент условного доступа:</span><span class="sxs-lookup"><span data-stu-id="f75ec-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="f75ec-331">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-332">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-333">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-334">Нажмите кнопку **корпоративных приложений** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-335">Щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-335">click **All applications**.</span></span>

6.  <span data-ttu-id="f75ec-336">Поиск приложение hello интересуют или hello пользователь пытается toosign в приложении tooby отображения идентификатор имя или приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="f75ec-337">Если вы не видите нужного приложения hello, щелкните hello **фильтра** кнопку и расширить область hello hello списка слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="f75ec-338">Toosee больше столбцов, нажмите кнопку hello **столбцы** кнопку tooadd Дополнительные сведения для приложений.</span><span class="sxs-lookup"><span data-stu-id="f75ec-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="f75ec-339">Нажмите кнопку hello **условного доступа** элемент навигации.</span><span class="sxs-lookup"><span data-stu-id="f75ec-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="f75ec-340">Выберите политику hello, вас интересует изучение.</span><span class="sxs-lookup"><span data-stu-id="f75ec-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="f75ec-341">Убедитесь, что нет никаких условий, назначений или других параметров, которые могут блокировать доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f75ec-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="f75ec-342">Вы можете отключить tootemporarily tooensure этой политики, она не влияет на toodo входа очередном hello, этот набор **включить политику** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки .</span><span class="sxs-lookup"><span data-stu-id="f75ec-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="f75ec-343">Отключение конкретной политики условного доступа</span><span class="sxs-lookup"><span data-stu-id="f75ec-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="f75ec-344">toocheck или проверить политику одного условного доступа:</span><span class="sxs-lookup"><span data-stu-id="f75ec-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="f75ec-345">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="f75ec-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f75ec-346">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f75ec-347">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="f75ec-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f75ec-348">Нажмите кнопку **корпоративных приложений** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="f75ec-349">Нажмите кнопку hello **условного доступа** элемент навигации.</span><span class="sxs-lookup"><span data-stu-id="f75ec-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="f75ec-350">Выберите политику hello, вас интересует изучение.</span><span class="sxs-lookup"><span data-stu-id="f75ec-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="f75ec-351">Отключить hello политики, установка hello **включить политику** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f75ec-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="f75ec-352">Проблемы с согласием для приложений</span><span class="sxs-lookup"><span data-stu-id="f75ec-352">Problems with application consent</span></span>

<span data-ttu-id="f75ec-353">Доступ к приложениям может быть заблокирована, так как не выполнена операция разрешения hello соответствующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="f75ec-354">Ниже приведены некоторые способы для устранения неполадок, связанных с согласием для приложений.</span><span class="sxs-lookup"><span data-stu-id="f75ec-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="f75ec-355">Операция разрешения на уровня пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="f75ec-356">Операция разрешения на уровне администратора для любого приложения</span><span class="sxs-lookup"><span data-stu-id="f75ec-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="f75ec-357">Операция разрешения на уровне администратора для приложения с одним клиентом</span><span class="sxs-lookup"><span data-stu-id="f75ec-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="f75ec-358">Операция разрешения на уровне администратора для мультитенантного приложения</span><span class="sxs-lookup"><span data-stu-id="f75ec-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="f75ec-359">Операция разрешения на уровня пользователя</span><span class="sxs-lookup"><span data-stu-id="f75ec-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="f75ec-360">Для любого подключения откройте идентификатор приложения с поддержкой разрешений, переход на экране входа toohello приложения выполняет пользовательское приложение toohello уровня разрешения для пользователя, выполнившего вход hello.</span><span class="sxs-lookup"><span data-stu-id="f75ec-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="f75ec-361">При желании toodo это программными средствами в разделе [запрашивает согласие пользователя на отдельных](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="f75ec-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="f75ec-362">Операция разрешения на уровне администратора для любого приложения</span><span class="sxs-lookup"><span data-stu-id="f75ec-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="f75ec-363">Для **только приложения, разработанные с помощью модели приложения hello V1**, можно принудительно это toooccur уровня согласия администратора путем добавления «**? prompt = admin\_согласия**» toohello конец URL-адреса входа приложения.</span><span class="sxs-lookup"><span data-stu-id="f75ec-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="f75ec-364">Для **любое приложение, разработанное с использованием модели приложения hello V2**, можно принудительно выполнить этот toooccur согласие на уровне администратора в соответствии с инструкциями hello под hello **запрашивать разрешения hello из каталога Администратор** раздел [с использованием конечной точки согласия администратора hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f75ec-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="f75ec-365">Операция разрешения на уровне администратора для приложения с одним клиентом</span><span class="sxs-lookup"><span data-stu-id="f75ec-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="f75ec-366">Для **приложения одного клиента** , запрашивать разрешения (например, тех, которые вы разрабатываете или владеть в вашей организации), можно выполнить **разрешения уровня администратора** операции от имени все Пользователи, вход в качестве глобального администратора и выбрав hello **предоставить разрешения** кнопку вверху hello hello **Application Registry -&gt; все приложения -&gt; выбрать приложение - &gt; Требуемые разрешения** колонку.</span><span class="sxs-lookup"><span data-stu-id="f75ec-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="f75ec-367">Для **любое приложение, разработанное с использованием hello V1 или V2 модели приложения**, можно принудительно выполнить этот toooccur согласие на уровне администратора в соответствии с инструкциями hello под hello **запрашивать разрешения hello из Администратор Directory** раздел [с использованием конечной точки согласия администратора hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f75ec-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="f75ec-368">Операция разрешения на уровне администратора для мультитенантного приложения</span><span class="sxs-lookup"><span data-stu-id="f75ec-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="f75ec-369">Для **мультитенантных приложений**, запрашивающих разрешения (например, приложения, которое разрабатывают сторонние производители или корпорация Майкрософт), можно выполнить операцию **согласия на уровне администратора**.</span><span class="sxs-lookup"><span data-stu-id="f75ec-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="f75ec-370">Войдите как глобальный администратор и щелкнув hello **предоставить разрешения** кнопку под hello **корпоративных приложений -&gt; все приложения -&gt; выбрать приложение -&gt; Разрешения** колонке (доступных ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="f75ec-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="f75ec-371">Также можно применять этот toooccur согласие на уровне администратора в соответствии с инструкциями hello под hello **запрашивать hello разрешения от администратора каталога** раздел [с использованием конечной точки согласия администратора hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f75ec-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f75ec-372">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f75ec-372">Next steps</span></span>
[<span data-ttu-id="f75ec-373">С помощью конечной точки согласия администратора hello</span><span class="sxs-lookup"><span data-stu-id="f75ec-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

