---
title: "Проблемы при входе в приложение Майкрософт | Документы Майкрософт"
description: "Устранение распространенных проблем, возникающих при входе в приложения Майкрософт с помощью Azure AD (например, Office 365)"
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="d18ec-103">Проблемы при входе в приложение Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d18ec-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="d18ec-104">Приложения Майкрософт (такие как Office 365 Exchange, SharePoint, Yammer и т. д.) назначаются и управляются немного иначе, чем приложения SaaS от сторонних разработчиков и другие приложения, которые вы интегрируете с Azure AD для единого входа.</span><span class="sxs-lookup"><span data-stu-id="d18ec-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="d18ec-105">Есть три основных способа, с помощью которых пользователь может получить доступ к приложению, опубликованному корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d18ec-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="d18ec-106">Для приложений в Office 365 или других платных наборах доступ пользователям предоставляется посредством **назначения лицензии** — непосредственно для учетной записи или в группе с помощью нашей возможности по групповому назначению лицензий.</span><span class="sxs-lookup"><span data-stu-id="d18ec-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="d18ec-107">Для приложений, которые Майкрософт или сторонний разработчик публикуют для свободного использования, пользователи могут получать доступ через **согласие пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="d18ec-108">Это означает, что они входят в приложение с помощью рабочей или учебной учетной записи Azure AD и предоставляют ему доступ к ограниченному набору данных в ней.</span><span class="sxs-lookup"><span data-stu-id="d18ec-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="d18ec-109">Для приложений, которые Майкрософт или сторонний разработчик публикуют для свободного использования, пользователи также могут получать доступ через **согласие администратора**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="d18ec-110">В этом случае администратор решает, что приложение разрешено использовать всем сотрудникам организации, после чего входит в приложение с помощью учетной записи глобального администратора и предоставляет доступ всем пользователям в организации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="d18ec-111">Чтобы устранить проблему, начните с раздела [Общие проблемные области при доступе к приложениям, которые необходимо учитывать](#general-problem-areas-with-application-access-to-consider), а затем получите более подробные сведения в статье [Пошаговое руководство: инструкции по устранению неполадок при доступе к приложениям Майкрософт](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="d18ec-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="d18ec-112">Общие проблемные области при доступе к приложениям, которые необходимо учитывать</span><span class="sxs-lookup"><span data-stu-id="d18ec-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="d18ec-113">Ниже приведен список общих проблемных областей, которые можно изучить более подробно, если вы поняли, где именно нужно искать. Однако для быстрого начала работы мы рекомендуем прочитать [Пошаговое руководство: инструкции по устранению неполадок при доступе к приложениям Майкрософт](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="d18ec-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="d18ec-114">Проблемы с учетной записью пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="d18ec-115">Проблемы с группами</span><span class="sxs-lookup"><span data-stu-id="d18ec-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="d18ec-116">Проблемы с политиками условного доступа</span><span class="sxs-lookup"><span data-stu-id="d18ec-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="d18ec-117">Проблемы с согласием для приложений</span><span class="sxs-lookup"><span data-stu-id="d18ec-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="d18ec-118">Инструкции по устранению неполадок при доступе к приложениям Майкрософт</span><span class="sxs-lookup"><span data-stu-id="d18ec-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="d18ec-119">Ниже приведены некоторые распространенные проблемы, с которыми сталкиваются специалисты, когда пользователям не удается войти в приложение Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d18ec-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="d18ec-120">Общие проблемы, которые следует проверить в первую очередь</span><span class="sxs-lookup"><span data-stu-id="d18ec-120">General issues to check first</span></span>

  * <span data-ttu-id="d18ec-121">Убедитесь, что пользователь выполняет вход с **правильным URL-адресом**, а не локальным URL-адресом приложения.</span><span class="sxs-lookup"><span data-stu-id="d18ec-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="d18ec-122">Убедитесь, что учетная запись пользователя **не заблокирована**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="d18ec-123">Убедитесь, что **учетная запись пользователя существует** в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d18ec-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="d18ec-124">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d18ec-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="d18ec-125">Проверьте, **включена** ли учетная запись пользователя для входа.</span><span class="sxs-lookup"><span data-stu-id="d18ec-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="d18ec-126">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="d18ec-127">Удостоверьтесь в том, что **пароль действителен и пользователь не забыл его**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="d18ec-128">[Сброс пароля пользователя](#reset-a-users-password) или [Включение самостоятельного сброса пароля](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="d18ec-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="d18ec-129">Проверьте, не блокирует ли **Многофакторная идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="d18ec-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="d18ec-130">[Проверка состояния службы Многофакторной идентификации](#check-a-users-multi-factor-authentication-status) или [Проверка контактной информации для проверки подлинности](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="d18ec-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="d18ec-131">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="d18ec-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="d18ec-132">[Проверка конкретной политики условного доступа](#problems-with-conditional-access-policies), [Проверка политики условного доступа для конкретного приложения](#check-a-specific-applications-conditional-access-policy) или [Отключение конкретной политики условного доступа](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="d18ec-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="d18ec-133">Убедитесь, что **контактная информация для проверки подлинности** актуальна, чтобы разрешить применение политик Многофакторной идентификации или условного доступа.</span><span class="sxs-lookup"><span data-stu-id="d18ec-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="d18ec-134">[Проверка состояния службы Многофакторной идентификации](#check-a-users-multi-factor-authentication-status) или [Проверка контактной информации для проверки подлинности](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="d18ec-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="d18ec-135">Для приложений **Майкрософт**, **которым требуется лицензия** (например, Office 365) ниже приведены характерные проблемы, которым нужно уделить внимание после обработки описанных выше общих проблем:</span><span class="sxs-lookup"><span data-stu-id="d18ec-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="d18ec-136">Убедитесь, что пользователю **назначена лицензия**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="d18ec-137">[Проверка назначенных пользователю лицензий](#check-a-users-assigned-licenses) или [Проверка назначенных группе лицензий](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="d18ec-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="d18ec-138">Если лицензия **назначена** **статической группе**, убедитесь, что **пользователь является членом** этой группы.</span><span class="sxs-lookup"><span data-stu-id="d18ec-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="d18ec-139">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="d18ec-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="d18ec-140">Если лицензия **назначена** **динамической группе**, убедитесь, что **правило динамической группы задано правильно**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="d18ec-141">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="d18ec-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="d18ec-142">Если лицензия **назначена** **динамической группе**, убедитесь, что эта группа **завершила обработку** членства и **пользователь является членом** (это может занять некоторое время).</span><span class="sxs-lookup"><span data-stu-id="d18ec-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="d18ec-143">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="d18ec-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="d18ec-144">Подтвердив назначение лицензии, убедитесь, что ее срок действия **не истек**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="d18ec-145">Убедитесь, что лицензия предназначена именно для **приложения**, к которому обращаются пользователи.</span><span class="sxs-lookup"><span data-stu-id="d18ec-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="d18ec-146">Для приложений **Майкрософт**, **которым лицензия не нужна**, можно проверить следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="d18ec-147">Если приложение запрашивает **разрешения уровня пользователя** (например, "доступ к почтовому ящику этого пользователя"), убедитесь, что пользователь вошел в приложение и выполнил **операцию согласия на уровне пользователя**, чтобы предоставить приложению доступ к своим данным.</span><span class="sxs-lookup"><span data-stu-id="d18ec-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="d18ec-148">Если приложение запрашивает **разрешения уровня администратора** (например, "доступ к почтовым ящикам всех пользователей"), убедитесь, что глобальный администратор выполнил **операцию согласия на уровне администратора от лица всех пользователей** в организации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="d18ec-149">Проблемы с учетной записью пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-149">Problems with the user’s account</span></span>

<span data-ttu-id="d18ec-150">Доступ к приложению может быть заблокирован из-за проблемы с пользователем, назначенным для приложения.</span><span class="sxs-lookup"><span data-stu-id="d18ec-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="d18ec-151">Ниже приведены некоторые способы устранения неполадок, связанных с параметрами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="d18ec-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="d18ec-152">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d18ec-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="d18ec-153">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="d18ec-154">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="d18ec-155">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="d18ec-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="d18ec-156">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="d18ec-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="d18ec-157">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="d18ec-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="d18ec-158">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="d18ec-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="d18ec-159">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="d18ec-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="d18ec-160">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="d18ec-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="d18ec-161">Проверка существования учетной записи пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d18ec-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="d18ec-162">Чтобы проверить, существует ли учетная запись пользователя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-163">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-164">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-165">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-166">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-167">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-167">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-168">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-169">Проверьте свойства объекта пользователя, чтобы убедиться, что они выглядят должным образом и что данные не отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="d18ec-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="d18ec-170">Проверка состояния учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-170">Check a user’s account status</span></span>

<span data-ttu-id="d18ec-171">Чтобы проверить состояние учетной записи пользователя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-172">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-173">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-174">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-175">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-176">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-176">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-177">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-178">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-178">click **Profile**.</span></span>

8.  <span data-ttu-id="d18ec-179">Убедитесь, что в разделе **Параметры** для параметра **Заблокировать вход** задано значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="d18ec-180">Сброс пароля пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-180">Reset a user’s password</span></span>

<span data-ttu-id="d18ec-181">Чтобы сбросить пароль пользователя, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-182">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-183">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-184">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-185">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-186">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-186">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-187">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-188">Нажмите кнопку **Сброс пароля** в верхней части колонки пользователя.</span><span class="sxs-lookup"><span data-stu-id="d18ec-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="d18ec-189">В открывшейся колонке **Смена пароля** нажмите кнопку **Сброс пароля**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="d18ec-190">Скопируйте **временный пароль** или **введите новый пароль** для пользователя.</span><span class="sxs-lookup"><span data-stu-id="d18ec-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="d18ec-191">Сообщите этот новый пароль пользователю, так как ему потребуется изменить пароль при следующем входе в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d18ec-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="d18ec-192">Включение самостоятельного сброса пароля</span><span class="sxs-lookup"><span data-stu-id="d18ec-192">Enable self-service password reset</span></span>

<span data-ttu-id="d18ec-193">Чтобы включить самостоятельный сброс пароля, следуйте указанным ниже разделам по развертыванию.</span><span class="sxs-lookup"><span data-stu-id="d18ec-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="d18ec-194">Разрешение пользователям сбрасывать пароли Azure AD</span><span class="sxs-lookup"><span data-stu-id="d18ec-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="d18ec-195">Разрешение пользователям сбрасывать или изменять пароли AD</span><span class="sxs-lookup"><span data-stu-id="d18ec-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="d18ec-196">Проверка состояния службы Многофакторной Идентификации</span><span class="sxs-lookup"><span data-stu-id="d18ec-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="d18ec-197">Чтобы проверить состояние службы Многофакторной Идентификации, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-198">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-199">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-200">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-201">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-202">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-202">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-203">Нажмите кнопку **Многофакторная Идентификация** в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="d18ec-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="d18ec-204">После загрузки **портала администрирования Многофакторной Идентификации** перейдите на вкладку **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="d18ec-205">Найдите пользователя в списке пользователей, выполнив поиск, фильтрацию или сортировку.</span><span class="sxs-lookup"><span data-stu-id="d18ec-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="d18ec-206">Выберите его из списка пользователей и по своему усмотрению **включите**, **отключите** или **примените** Многофакторною идентификацию.</span><span class="sxs-lookup"><span data-stu-id="d18ec-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="d18ec-207">**Примечание**. Если пользователь находится в состоянии **Принудительно**, можно временно задать состояние **Отключено**, чтобы разрешить ему вернуться в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d18ec-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="d18ec-208">После этого можно снова изменить состояние на **Включено**, чтобы при следующем входе пользователь повторно зарегистрировал контактные данные.</span><span class="sxs-lookup"><span data-stu-id="d18ec-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="d18ec-209">Кроме того, можно выполнить действия, описанные в разделе [Проверка контактной информации для проверки подлинности](#check-a-users-authentication-contact-info), чтобы проверить или задать эти данные для пользователя.</span><span class="sxs-lookup"><span data-stu-id="d18ec-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="d18ec-210">Проверка контактной информации для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="d18ec-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="d18ec-211">Чтобы проверить контактную информацию для проверки подлинности, используемую для Многофакторной Идентификации, условного доступа, защиты идентификации и сброса пароля, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-212">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-213">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-214">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-215">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-216">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-216">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-217">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-218">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-218">click **Profile**.</span></span>

8.  <span data-ttu-id="d18ec-219">Прокрутите вниз до раздела **Контактная информация для проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="d18ec-220">**Просмотрите** данные, зарегистрированные для пользователя, и обновите их при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d18ec-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="d18ec-221">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="d18ec-221">Check a user’s group memberships</span></span>

<span data-ttu-id="d18ec-222">Чтобы проверить членство пользователя в группах, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-223">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-224">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-225">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-226">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-227">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-227">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-228">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-229">Щелкните **Группы**, чтобы узнать, в какие группы входит пользователь.</span><span class="sxs-lookup"><span data-stu-id="d18ec-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="d18ec-230">Проверка назначенных пользователю лицензий</span><span class="sxs-lookup"><span data-stu-id="d18ec-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="d18ec-231">Чтобы проверить назначенные пользователю лицензии, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d18ec-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-232">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-233">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-234">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-235">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-236">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-236">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-237">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-238">Чтобы просмотреть лицензии, которые в настоящее время назначены пользователю, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="d18ec-239">Назначение лицензии пользователю</span><span class="sxs-lookup"><span data-stu-id="d18ec-239">Assign a user a license</span></span> 

<span data-ttu-id="d18ec-240">Чтобы назначить лицензию пользователю, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d18ec-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-241">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-242">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-243">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-244">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-245">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-245">click **All users**.</span></span>

6.  <span data-ttu-id="d18ec-246">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-247">Чтобы просмотреть лицензии, которые в настоящее время назначены пользователю, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="d18ec-248">Нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="d18ec-249">Выберите **один или несколько продуктов** в списке доступных продуктов.</span><span class="sxs-lookup"><span data-stu-id="d18ec-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="d18ec-250">**Необязательно:** чтобы назначить отдельные продукты, щелкните элемент **Параметры назначения**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="d18ec-251">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="d18ec-252">Чтобы назначить выбранные лицензии пользователю, нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="d18ec-253">Проблемы с группами</span><span class="sxs-lookup"><span data-stu-id="d18ec-253">Problems with groups</span></span>

<span data-ttu-id="d18ec-254">Доступ к приложению может быть заблокирован из-за проблемы с группой, назначенной для приложения.</span><span class="sxs-lookup"><span data-stu-id="d18ec-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="d18ec-255">Ниже приведены некоторые способы для устранения неполадок, связанных с группами и членством в них.</span><span class="sxs-lookup"><span data-stu-id="d18ec-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="d18ec-256">Проверка членства в группе</span><span class="sxs-lookup"><span data-stu-id="d18ec-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="d18ec-257">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="d18ec-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="d18ec-258">Проверка назначенных группе лицензий</span><span class="sxs-lookup"><span data-stu-id="d18ec-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="d18ec-259">Повторная обработка лицензий группы</span><span class="sxs-lookup"><span data-stu-id="d18ec-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="d18ec-260">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="d18ec-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="d18ec-261">Проверка членства в группе</span><span class="sxs-lookup"><span data-stu-id="d18ec-261">Check a group’s membership</span></span>

<span data-ttu-id="d18ec-262">Чтобы проверить членство в группе, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d18ec-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-263">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-264">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-265">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-266">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-267">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-267">click **All groups**.</span></span>

6.  <span data-ttu-id="d18ec-268">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-269">Щелкните **Члены**, чтобы просмотреть список пользователей, назначенных этой группе.</span><span class="sxs-lookup"><span data-stu-id="d18ec-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="d18ec-270">Проверка критериев членства для динамической группы</span><span class="sxs-lookup"><span data-stu-id="d18ec-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="d18ec-271">Чтобы проверить критерии членства в динамической группе, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-272">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-273">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-274">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-275">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-276">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-276">click **All groups**.</span></span>

6.  <span data-ttu-id="d18ec-277">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-278">Щелкните **Правила динамического членства**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="d18ec-279">Просмотрите **простое** или **расширенное** правило, определенное для этой группы, и убедитесь, что пользователь, который должен стать ее членом, соответствует данным критериям.</span><span class="sxs-lookup"><span data-stu-id="d18ec-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="d18ec-280">Проверка назначенных группе лицензий</span><span class="sxs-lookup"><span data-stu-id="d18ec-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="d18ec-281">Чтобы проверить назначенные группе лицензии, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-282">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-283">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-284">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-285">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-286">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-286">click **All groups**.</span></span>

6.  <span data-ttu-id="d18ec-287">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-288">Чтобы просмотреть лицензии, которые в настоящее время назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="d18ec-289">Повторная обработка лицензий группы</span><span class="sxs-lookup"><span data-stu-id="d18ec-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="d18ec-290">Чтобы повторно обработать назначенные группе лицензии, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d18ec-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-291">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-292">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-293">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-294">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-295">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-295">click **All groups**.</span></span>

6.  <span data-ttu-id="d18ec-296">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-297">Чтобы просмотреть лицензии, которые в настоящее время назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="d18ec-298">Нажмите кнопку **Повторно обработать**, чтобы обеспечить актуальность лицензий, назначенных членам этой группы.</span><span class="sxs-lookup"><span data-stu-id="d18ec-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="d18ec-299">Это действие может занять много времени в зависимости от размера и сложности группы.</span><span class="sxs-lookup"><span data-stu-id="d18ec-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d18ec-300">Чтобы ускорить процесс, можно временно назначить лицензию пользователю напрямую.</span><span class="sxs-lookup"><span data-stu-id="d18ec-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="d18ec-301">[Назначение лицензии пользователю](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="d18ec-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="d18ec-302">Назначение лицензии группе</span><span class="sxs-lookup"><span data-stu-id="d18ec-302">Assign a group a license</span></span>

<span data-ttu-id="d18ec-303">Чтобы назначить лицензию группе, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d18ec-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="d18ec-304">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-305">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-306">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-307">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-308">Щелкните **Все группы**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-308">click **All groups**.</span></span>

6.  <span data-ttu-id="d18ec-309">**Найдите** нужную группу и выберите ее, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="d18ec-310">Чтобы просмотреть лицензии, которые в настоящее время назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="d18ec-311">Нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="d18ec-312">Выберите **один или несколько продуктов** в списке доступных продуктов.</span><span class="sxs-lookup"><span data-stu-id="d18ec-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="d18ec-313">**Необязательно:** чтобы назначить отдельные продукты, щелкните элемент **Параметры назначения**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="d18ec-314">По завершении нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="d18ec-315">Чтобы назначить выбранные лицензии группе, нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="d18ec-316">Это действие может занять много времени в зависимости от размера и сложности группы.</span><span class="sxs-lookup"><span data-stu-id="d18ec-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d18ec-317">Чтобы ускорить процесс, можно временно назначить лицензию пользователю напрямую.</span><span class="sxs-lookup"><span data-stu-id="d18ec-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="d18ec-318">[Назначение лицензии пользователю](#problems-with-application-consent)</span><span class="sxs-lookup"><span data-stu-id="d18ec-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="d18ec-319">Проблемы с политиками условного доступа</span><span class="sxs-lookup"><span data-stu-id="d18ec-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="d18ec-320">Проверка конкретной политики условного доступа</span><span class="sxs-lookup"><span data-stu-id="d18ec-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="d18ec-321">Проверка отдельной политики условного доступа:</span><span class="sxs-lookup"><span data-stu-id="d18ec-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="d18ec-322">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-323">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-324">Введите **Azure Active Directory** в поле фильтра поиска и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-325">Щелкните пункт **Корпоративные приложения** в меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-326">Щелкните элемент навигации **Условный доступ**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="d18ec-327">Щелкните политику, которую хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="d18ec-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="d18ec-328">Убедитесь, что нет никаких условий, назначений или других параметров, которые могут блокировать доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="d18ec-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="d18ec-329">Вы можете временно отключить эту политику, чтобы убедиться, что она не влияет на операции входа.</span><span class="sxs-lookup"><span data-stu-id="d18ec-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="d18ec-330">Для этого установите переключатель **Включить политику** в положение **Нет** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="d18ec-331">Проверка политики условного доступа для конкретного приложения</span><span class="sxs-lookup"><span data-stu-id="d18ec-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="d18ec-332">Проверка отдельной настроенной политики условного доступа для приложения:</span><span class="sxs-lookup"><span data-stu-id="d18ec-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="d18ec-333">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-334">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-335">Введите **Azure Active Directory** в поле фильтра поиска и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-336">Щелкните пункт **Корпоративные приложения** в меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-337">Щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-337">click **All applications**.</span></span>

6.  <span data-ttu-id="d18ec-338">Найдите приложение, которое вас заинтересовало или куда пытался войти пользователь, по отображаемому имени или идентификатору.</span><span class="sxs-lookup"><span data-stu-id="d18ec-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="d18ec-339">Если вы не находите приложение, нажмите кнопку **Фильтр** и разверните область до значения **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="d18ec-340">Если вы хотите отобразить больше столбцов, нажмите кнопку **Столбцы**, чтобы добавить дополнительные сведения для приложений.</span><span class="sxs-lookup"><span data-stu-id="d18ec-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="d18ec-341">Щелкните элемент навигации **Условный доступ**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="d18ec-342">Щелкните политику, которую хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="d18ec-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="d18ec-343">Убедитесь, что нет никаких условий, назначений или других параметров, которые могут блокировать доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="d18ec-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="d18ec-344">Вы можете временно отключить эту политику, чтобы убедиться, что она не влияет на операции входа.</span><span class="sxs-lookup"><span data-stu-id="d18ec-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="d18ec-345">Для этого установите переключатель **Включить политику** в положение **Нет** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="d18ec-346">Отключение конкретной политики условного доступа</span><span class="sxs-lookup"><span data-stu-id="d18ec-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="d18ec-347">Проверка отдельной политики условного доступа:</span><span class="sxs-lookup"><span data-stu-id="d18ec-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="d18ec-348">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d18ec-349">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d18ec-350">Введите **Azure Active Directory** в поле фильтра поиска и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d18ec-351">Щелкните пункт **Корпоративные приложения** в меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d18ec-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="d18ec-352">Щелкните элемент навигации **Условный доступ**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="d18ec-353">Щелкните политику, которую хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="d18ec-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="d18ec-354">Отключите политику, установив переключатель **Включить политику** в положение **Нет**, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="d18ec-355">Проблемы с согласием для приложений</span><span class="sxs-lookup"><span data-stu-id="d18ec-355">Problems with application consent</span></span>

<span data-ttu-id="d18ec-356">Доступ к приложению может быть заблокирован из-за того, что не выполнена должная операция предоставления согласия.</span><span class="sxs-lookup"><span data-stu-id="d18ec-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="d18ec-357">Ниже приведены некоторые способы для устранения неполадок, связанных с согласием для приложений.</span><span class="sxs-lookup"><span data-stu-id="d18ec-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="d18ec-358">Операция разрешения на уровня пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="d18ec-359">Операция разрешения на уровне администратора для любого приложения</span><span class="sxs-lookup"><span data-stu-id="d18ec-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="d18ec-360">Операция разрешения на уровне администратора для приложения с одним клиентом</span><span class="sxs-lookup"><span data-stu-id="d18ec-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="d18ec-361">Операция разрешения на уровне администратора для мультитенантного приложения</span><span class="sxs-lookup"><span data-stu-id="d18ec-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="d18ec-362">Операция разрешения на уровня пользователя</span><span class="sxs-lookup"><span data-stu-id="d18ec-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="d18ec-363">Для любого приложения с включенным Open ID Connect, которое запрашивает разрешение, переход на экран входа обеспечивает согласие на предоставление приложению прав для пользователя, выполнившего вход.</span><span class="sxs-lookup"><span data-stu-id="d18ec-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="d18ec-364">Если вы хотите сделать это программными средствами, см. статью [Запрос на получение согласия одного пользователя](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="d18ec-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="d18ec-365">Операция разрешения на уровне администратора для любого приложения</span><span class="sxs-lookup"><span data-stu-id="d18ec-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="d18ec-366">**Только для приложений, разработанных с помощью модели приложения версии 1**, вы можете принудительно реализовать согласие на уровне администратора, добавив "**?prompt=admin\_consent**" в конец URL-адреса входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="d18ec-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="d18ec-367">Для **любых приложений, разработанных с помощью модели приложения версии 2**, вы можете принудительно реализовать согласие на уровне администратора, выполнив инструкции из раздела **Запрос разрешений у администратора каталога** статьи [Использование конечной точки предоставления согласия администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="d18ec-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="d18ec-368">Операция разрешения на уровне администратора для приложения с одним клиентом</span><span class="sxs-lookup"><span data-stu-id="d18ec-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="d18ec-369">Для **приложений с одним клиентом**, запрашивающих разрешения (как те, которые вы разрабатываете или используете в своей организации), можно выполнить операцию **согласия на уровне администратора** от имени всех пользователей. Для этого выполните вход в качестве глобального администратора и нажмите кнопку **Предоставить разрешения** в верхней части колонки **Реестр приложений -&gt; Все приложения -&gt; Выберите приложение -&gt; Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="d18ec-370">Для **любых приложений, разработанных с помощью модели приложения версии 1 или 2**, вы можете принудительно реализовать согласие на уровне администратора, выполнив инструкции из раздела **Запрос разрешений у администратора каталога** статьи [Использование конечной точки предоставления согласия администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="d18ec-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="d18ec-371">Операция разрешения на уровне администратора для мультитенантного приложения</span><span class="sxs-lookup"><span data-stu-id="d18ec-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="d18ec-372">Для **мультитенантных приложений**, запрашивающих разрешения (например, приложения, которое разрабатывают сторонние производители или корпорация Майкрософт), можно выполнить операцию **согласия на уровне администратора**.</span><span class="sxs-lookup"><span data-stu-id="d18ec-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="d18ec-373">Войдите в качестве глобального администратора и нажмите кнопку **Предоставить разрешения** в колонке **Корпоративные приложения -&gt; Все приложения -&gt; Выберите приложение -&gt; Разрешения** (будет доступна в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="d18ec-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="d18ec-374">Вы также можете принудительно реализовать согласие на уровне администратора, выполнив инструкции из раздела **Запрос разрешений у администратора каталога** статьи [Использование конечной точки предоставления согласия администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="d18ec-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d18ec-375">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d18ec-375">Next steps</span></span>
[<span data-ttu-id="d18ec-376">Использование конечной точки предоставления согласия администратора</span><span class="sxs-lookup"><span data-stu-id="d18ec-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

