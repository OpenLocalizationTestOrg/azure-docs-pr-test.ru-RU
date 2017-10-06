---
title: "aaaWhat возможности совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Совместная работа Azure Active Directory B2B поддерживает связей между компаниями, включив деловых партнеров tooselectively доступ к корпоративным приложениям."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="6dd58-104">Что такое служба совместной работы Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="6dd58-105">Возможности (B2B) совместной работы Azure AD бизнес-включить любой организации, с помощью Azure AD toowork безопасно и надежно с пользователями из любую другую организацию, крупных или мелких.</span><span class="sxs-lookup"><span data-stu-id="6dd58-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD toowork safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="6dd58-106">наличия Azure AD и даже наличия ИТ-отдела.</span><span class="sxs-lookup"><span data-stu-id="6dd58-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="6dd58-107">Организации с помощью Azure AD могут предоставлять доступ партнеров tootheir toodocuments, ресурсам и приложениям, сохраняя полный контроль над корпоративных данных.</span><span class="sxs-lookup"><span data-stu-id="6dd58-107">Organizations using Azure AD can provide access toodocuments, resources, and applications tootheir partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="6dd58-108">Разработчики могут использовать приложения toowrite API-интерфейсы бизнес-hello Azure AD, объединяющие две организации в более безопасно.</span><span class="sxs-lookup"><span data-stu-id="6dd58-108">Developers can use hello Azure AD business-to-business APIs toowrite applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="6dd58-109">Кроме того это довольно просто для toonavigate конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="6dd58-109">Also, it's pretty easy for end users toonavigate.</span></span>

<span data-ttu-id="6dd58-110">97% наших клиентов просили, что очень важно toothem совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="6dd58-110">97% of our customers have told us Azure AD B2B collaboration is very important toothem.</span></span>

![круговая диаграмма](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="6dd58-112">По состоянию на начало апреля 2017 года приблизительно 3 миллиона пользователей уже применяли возможности совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="6dd58-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="6dd58-113">Более 23 % организаций со службой Azure AD и числом пользователей более 10 уже применяют эти возможности.</span><span class="sxs-lookup"><span data-stu-id="6dd58-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a><span data-ttu-id="6dd58-114">Основные преимущества Hello организации tooyour совместной работы Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-114">hello key benefits of Azure AD B2B collaboration tooyour organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="6dd58-115">Работа с любым пользователем из любой партнерской организации</span><span class="sxs-lookup"><span data-stu-id="6dd58-115">Work with any user from any partner</span></span>

* <span data-ttu-id="6dd58-116">Партнеры используют собственные учетные данные</span><span class="sxs-lookup"><span data-stu-id="6dd58-116">Partners use their own credentials</span></span>

* <span data-ttu-id="6dd58-117">Не требуется для партнеров toouse Azure AD</span><span class="sxs-lookup"><span data-stu-id="6dd58-117">No requirement for partners toouse Azure AD</span></span>

* <span data-ttu-id="6dd58-118">Не требуются внешние каталоги или сложная настройка</span><span class="sxs-lookup"><span data-stu-id="6dd58-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="6dd58-119">Простая и безопасная совместная работа</span><span class="sxs-lookup"><span data-stu-id="6dd58-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="6dd58-120">Предоставить доступ tooany корпоративному приложению или данных, при применении сложных, Azure AD энергопотреблением политики авторизации</span><span class="sxs-lookup"><span data-stu-id="6dd58-120">Provide access tooany corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="6dd58-121">Простое использование</span><span class="sxs-lookup"><span data-stu-id="6dd58-121">Easy for users</span></span>

* <span data-ttu-id="6dd58-122">Безопасность корпоративного уровня для приложений и данных</span><span class="sxs-lookup"><span data-stu-id="6dd58-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="6dd58-123">Отсутствие накладных расходов на управление</span><span class="sxs-lookup"><span data-stu-id="6dd58-123">No management overhead</span></span>

* <span data-ttu-id="6dd58-124">Не требуется управлять внешними учетными записями или паролями</span><span class="sxs-lookup"><span data-stu-id="6dd58-124">No external account or password management</span></span>

* <span data-ttu-id="6dd58-125">Не требуется синхронизировать учетные записи или управлять их жизненным циклом вручную</span><span class="sxs-lookup"><span data-stu-id="6dd58-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="6dd58-126">Отсутствие накладных расходов на внешнее администрирование</span><span class="sxs-lookup"><span data-stu-id="6dd58-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a><span data-ttu-id="6dd58-127">Можно легко добавить B2B совместной работы пользователей tooyour организации</span><span class="sxs-lookup"><span data-stu-id="6dd58-127">You can easily add B2B collaboration users tooyour organization</span></span>

<span data-ttu-id="6dd58-128">Администраторы могут добавить пользователей совместной работы (гостевая) B2B на hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dd58-128">Admins can add B2B collaboration (guest) users in hello [Azure portal](https://portal.azure.com).</span></span>

![добавление гостевых пользователей](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a><span data-ttu-id="6dd58-130">Включить собственные удостоверения вашей toobring участники совместной работы</span><span class="sxs-lookup"><span data-stu-id="6dd58-130">Enable your collaborators toobring their own identity</span></span>

<span data-ttu-id="6dd58-131">Партнеры B2B могут выполнять вход, используя удостоверения на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="6dd58-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="6dd58-132">Если пользователь hello не имеет учетной записи Майкрософт или учетную запись Azure AD, он будет создан для них без проблем во время hello для активации предложения.</span><span class="sxs-lookup"><span data-stu-id="6dd58-132">If hello user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at hello time for offer redemption.</span></span>

![выбор удостоверения для входа](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a><span data-ttu-id="6dd58-134">Владельцы делегат tooapplication и группы</span><span class="sxs-lookup"><span data-stu-id="6dd58-134">Delegate tooapplication and group owners</span></span> 
<span data-ttu-id="6dd58-135">Приложения и владельцев группы можно добавлять пользователей B2B непосредственно tooany приложения, который вас интересует, как приложение Microsoft, так и не.</span><span class="sxs-lookup"><span data-stu-id="6dd58-135">Application and group owners can add B2B users directly tooany application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="6dd58-136">Администраторы могут делегировать B2B пользователям разрешение tooadd toonon администраторов.</span><span class="sxs-lookup"><span data-stu-id="6dd58-136">Admins can delegate permission tooadd B2B users toonon-admins.</span></span> <span data-ttu-id="6dd58-137">Администраторы не могут использовать hello [панели доступа приложения Azure AD](https://myapps.microsoft.com) tooadd B2B tooapplications совместной работы пользователей или групп.</span><span class="sxs-lookup"><span data-stu-id="6dd58-137">Non-admins can use hello [Azure AD Application Access Panel](https://myapps.microsoft.com) tooadd B2B collaboration users tooapplications or groups.</span></span>

![панель доступа](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="6dd58-140">Защита корпоративного содержимого с помощью политик авторизации</span><span class="sxs-lookup"><span data-stu-id="6dd58-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="6dd58-141">Вы можете применить политики условного доступа, например многофакторную проверку подлинности на следующих уровнях:</span><span class="sxs-lookup"><span data-stu-id="6dd58-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="6dd58-142">На уровне клиента hello</span><span class="sxs-lookup"><span data-stu-id="6dd58-142">At hello tenant level</span></span>
- <span data-ttu-id="6dd58-143">На уровне приложения hello</span><span class="sxs-lookup"><span data-stu-id="6dd58-143">At hello application level</span></span>
- <span data-ttu-id="6dd58-144">Для определенных пользователей tooprotect корпоративным приложениям и данным</span><span class="sxs-lookup"><span data-stu-id="6dd58-144">For specific users tooprotect corporate apps and data</span></span>

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a><span data-ttu-id="6dd58-146">Используйте наши API-интерфейсы и образец кода tooeasily построения приложений tooonboard</span><span class="sxs-lookup"><span data-stu-id="6dd58-146">Use our APIs and sample code tooeasily build applications tooonboard</span></span>
<span data-ttu-id="6dd58-147">Переведите внешними партнерами на них в способов настроенные tooyour с потребностями организации.</span><span class="sxs-lookup"><span data-stu-id="6dd58-147">Bring your external partners on board in ways customized tooyour organization’s needs.</span></span>

<span data-ttu-id="6dd58-148">С помощью hello [приглашения совместной работы B2B API-интерфейсы](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), вы можете настроить своими впечатлениями адаптации, включая создание порталы самообслуживания, регистрации.</span><span class="sxs-lookup"><span data-stu-id="6dd58-148">Using hello [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="6dd58-149">В [GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) вы найдете образец кода для этого портала.</span><span class="sxs-lookup"><span data-stu-id="6dd58-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![портал регистрации](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="6dd58-151">С совместной работы Azure AD B2B можно получить все возможности Azure AD tooprotect hello связей партнера в результате которого пользователи найти легко и интуитивно понятно.</span><span class="sxs-lookup"><span data-stu-id="6dd58-151">With Azure AD B2B collaboration, you can get hello full power of Azure AD tooprotect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="6dd58-152">Поэтому действуйте, соединения hello тысяч организаций, которые уже используют Azure AD B2B для совместной работы в их внешних!</span><span class="sxs-lookup"><span data-stu-id="6dd58-152">So go ahead, join hello thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dd58-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6dd58-153">Next steps</span></span>

* <span data-ttu-id="6dd58-154">Возможности администратора находятся в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dd58-154">Administrator experiences are found in hello [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="6dd58-155">Опыт работника сведения доступны в hello [панели доступа](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6dd58-155">Information worker experiences are available in hello [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="6dd58-156">И как всегда, связь с группой разработчиков hello за любые отзывы, обсуждения и предложения по нашей [Технический сообщества Майкрософт](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="6dd58-156">And, as always, connect with hello product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="6dd58-157">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="6dd58-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6dd58-158">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="6dd58-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6dd58-159">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6dd58-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6dd58-160">элементы Hello hello электронное приглашение B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="6dd58-160">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6dd58-161">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6dd58-162">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6dd58-163">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="6dd58-164">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6dd58-165">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="6dd58-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="6dd58-166">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="6dd58-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="6dd58-167">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="6dd58-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="6dd58-168">[Auditing and reporting a B2B collaboration user](active-directory-b2b-auditing-and-reporting.md) (Аудит и создание отчетов для пользователей службы совместной работы B2B)</span><span class="sxs-lookup"><span data-stu-id="6dd58-168">[B2B collaboration user auditing and reporting](active-directory-b2b-auditing-and-reporting.md)</span></span>
* [<span data-ttu-id="6dd58-169">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6dd58-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
