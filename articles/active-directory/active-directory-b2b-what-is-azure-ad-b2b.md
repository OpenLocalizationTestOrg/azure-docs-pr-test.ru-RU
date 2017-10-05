---
title: "Что такое служба совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Служба совместной работы Azure Active Directory B2B поддерживает взаимодействие между компаниями, позволяя предоставлять бизнес-партнерам выборочный доступ к вашим корпоративным приложениям."
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
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="78108-104">Что такое служба совместной работы Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="78108-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="78108-105">Возможности совместной работы Azure AD B2B позволяют любой организации, использующей Azure AD, безопасно работать с пользователями из любой другой организации независимо от ее размера,</span><span class="sxs-lookup"><span data-stu-id="78108-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="78108-106">наличия Azure AD и даже наличия ИТ-отдела.</span><span class="sxs-lookup"><span data-stu-id="78108-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="78108-107">Организации, использующие Azure AD, могут предоставлять доступ к документам, ресурсам и приложениям своим партнерам, сохраняя полный контроль над корпоративными данными.</span><span class="sxs-lookup"><span data-stu-id="78108-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="78108-108">Разработчики могут использовать предоставляемые интерфейсы API Azure AD типа "бизнес — бизнес" для написания приложений, которые защищенным способом соединяют две организации.</span><span class="sxs-lookup"><span data-stu-id="78108-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="78108-109">Кроме того, предусмотрена быстрая и удобная навигация.</span><span class="sxs-lookup"><span data-stu-id="78108-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="78108-110">97 % клиентов сообщили, что служба совместной работы Azure AD B2B очень важна для них.</span><span class="sxs-lookup"><span data-stu-id="78108-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![круговая диаграмма](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="78108-112">По состоянию на начало апреля 2017 года приблизительно 3 миллиона пользователей уже применяли возможности совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="78108-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="78108-113">Более 23 % организаций со службой Azure AD и числом пользователей более 10 уже применяют эти возможности.</span><span class="sxs-lookup"><span data-stu-id="78108-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="78108-114">Основные преимущества службы совместной работы Azure AD B2B для организации</span><span class="sxs-lookup"><span data-stu-id="78108-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="78108-115">Работа с любым пользователем из любой партнерской организации</span><span class="sxs-lookup"><span data-stu-id="78108-115">Work with any user from any partner</span></span>

* <span data-ttu-id="78108-116">Партнеры используют собственные учетные данные</span><span class="sxs-lookup"><span data-stu-id="78108-116">Partners use their own credentials</span></span>

* <span data-ttu-id="78108-117">От партнеров не требуется использовать Azure AD</span><span class="sxs-lookup"><span data-stu-id="78108-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="78108-118">Не требуются внешние каталоги или сложная настройка</span><span class="sxs-lookup"><span data-stu-id="78108-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="78108-119">Простая и безопасная совместная работа</span><span class="sxs-lookup"><span data-stu-id="78108-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="78108-120">Предоставление доступа к любым корпоративным приложениям и данным с применением эффективных политик авторизации на основе Azure AD</span><span class="sxs-lookup"><span data-stu-id="78108-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="78108-121">Простое использование</span><span class="sxs-lookup"><span data-stu-id="78108-121">Easy for users</span></span>

* <span data-ttu-id="78108-122">Безопасность корпоративного уровня для приложений и данных</span><span class="sxs-lookup"><span data-stu-id="78108-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="78108-123">Отсутствие накладных расходов на управление</span><span class="sxs-lookup"><span data-stu-id="78108-123">No management overhead</span></span>

* <span data-ttu-id="78108-124">Не требуется управлять внешними учетными записями или паролями</span><span class="sxs-lookup"><span data-stu-id="78108-124">No external account or password management</span></span>

* <span data-ttu-id="78108-125">Не требуется синхронизировать учетные записи или управлять их жизненным циклом вручную</span><span class="sxs-lookup"><span data-stu-id="78108-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="78108-126">Отсутствие накладных расходов на внешнее администрирование</span><span class="sxs-lookup"><span data-stu-id="78108-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="78108-127">Простота добавления пользователей решения для совместной работы B2B в организации</span><span class="sxs-lookup"><span data-stu-id="78108-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="78108-128">Администраторы могут добавлять пользователей (гостей) решения для совместной работы B2B на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78108-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![добавление гостевых пользователей](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="78108-130">Возможность использования партнерами собственных удостоверений</span><span class="sxs-lookup"><span data-stu-id="78108-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="78108-131">Партнеры B2B могут выполнять вход, используя удостоверения на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="78108-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="78108-132">Если у пользователя нет учетной записи Майкрософт или Azure AD, она быстро создается при активации предложения.</span><span class="sxs-lookup"><span data-stu-id="78108-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![выбор удостоверения для входа](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="78108-134">Делегирование прав владельцами приложений и групп</span><span class="sxs-lookup"><span data-stu-id="78108-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="78108-135">Владельцы приложений и групп могут напрямую добавлять пользователей B2B в любое приложение, будь то приложение Майкрософт или другого поставщика.</span><span class="sxs-lookup"><span data-stu-id="78108-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="78108-136">Администраторы могут делегировать разрешение на добавление пользователей B2B пользователям, не являющимся администраторами.</span><span class="sxs-lookup"><span data-stu-id="78108-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="78108-137">Эти пользователи могут с помощью [панели доступа к приложениям Azure AD](https://myapps.microsoft.com) добавлять пользователей B2B в приложения и группы.</span><span class="sxs-lookup"><span data-stu-id="78108-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![панель доступа](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="78108-140">Защита корпоративного содержимого с помощью политик авторизации</span><span class="sxs-lookup"><span data-stu-id="78108-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="78108-141">Вы можете применить политики условного доступа, например многофакторную проверку подлинности на следующих уровнях:</span><span class="sxs-lookup"><span data-stu-id="78108-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="78108-142">на уровне клиента;</span><span class="sxs-lookup"><span data-stu-id="78108-142">At the tenant level</span></span>
- <span data-ttu-id="78108-143">на уровне приложения;</span><span class="sxs-lookup"><span data-stu-id="78108-143">At the application level</span></span>
- <span data-ttu-id="78108-144">или для конкретных пользователей, чтобы защитить корпоративные приложения и данные.</span><span class="sxs-lookup"><span data-stu-id="78108-144">For specific users to protect corporate apps and data</span></span>

![добавление участника](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="78108-146">Быстрое создание приложений для регистрации с помощью интерфейсов API и образцов кода</span><span class="sxs-lookup"><span data-stu-id="78108-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="78108-147">Вы можете регистрировать внешних партнеров так, как требуется вашей организации.</span><span class="sxs-lookup"><span data-stu-id="78108-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="78108-148">С помощью [API-интерфейсов приглашения службы совместной работы B2B](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation) вы можете настроить собственные процедуры регистрации, в том числе создать портал для самостоятельной регистрации.</span><span class="sxs-lookup"><span data-stu-id="78108-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="78108-149">В [GitHub](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web) вы найдете образец кода для этого портала.</span><span class="sxs-lookup"><span data-stu-id="78108-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![портал регистрации](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="78108-151">С помощью службы совместной работы Azure AD B2B вы можете максимально эффективно использовать возможности Azure AD для защиты своих отношений с партнерами, обеспечив при этом удобство работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="78108-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="78108-152">Присоединяйтесь к тысячам организаций, которые уже применяют Azure AD B2B для взаимодействия с внешними партнерами.</span><span class="sxs-lookup"><span data-stu-id="78108-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="78108-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78108-153">Next steps</span></span>

* <span data-ttu-id="78108-154">Возможности для администраторов предоставляются на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78108-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="78108-155">Возможности для информационных работников доступны на [панели доступа](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="78108-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="78108-156">Как всегда, вы можете связаться с группой разработчиков через [техническое сообщество Майкрософт](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b), чтобы предоставить отзыв, обсудить проблему или внести предложение.</span><span class="sxs-lookup"><span data-stu-id="78108-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="78108-157">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="78108-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="78108-158">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="78108-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="78108-159">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78108-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="78108-160">Элементы сообщения с приглашением в службу совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="78108-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="78108-161">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="78108-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="78108-162">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="78108-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="78108-163">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="78108-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="78108-164">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="78108-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="78108-165">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="78108-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="78108-166">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="78108-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="78108-167">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="78108-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="78108-168">[Auditing and reporting a B2B collaboration user](active-directory-b2b-auditing-and-reporting.md) (Аудит и создание отчетов для пользователей службы совместной работы B2B)</span><span class="sxs-lookup"><span data-stu-id="78108-168">[B2B collaboration user auditing and reporting](active-directory-b2b-auditing-and-reporting.md)</span></span>
* [<span data-ttu-id="78108-169">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78108-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
