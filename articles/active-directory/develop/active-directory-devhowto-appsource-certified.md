---
title: "aaaHow tooget AppSource, сертифицированные для Azure Active Directory | Документы Microsoft"
description: "Сведения о том, как tooget приложения AppSource Сертифицировано для Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="81fd6-103">Как tooget AppSource Сертифицировано для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81fd6-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="81fd6-104">[Microsoft AppSource](https://appsource.microsoft.com/) является местом назначения для бизнеса toodiscover пользователей, попробуйте и управление бизнес-приложений SaaS (автономный SaaS и надстройки tooexisting Microsoft SaaS продуктов).</span><span class="sxs-lookup"><span data-stu-id="81fd6-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="81fd6-105">toolist автономное приложение SaaS на AppSource приложения необходимо принять единого входа из рабочих учетных записей из любой компании или организации с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81fd6-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="81fd6-106">Hello входа в процесс должен использовать hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) или [OAuth 2.0](./active-directory-protocols-oauth-code.md) протоколы.</span><span class="sxs-lookup"><span data-stu-id="81fd6-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="81fd6-107">Для сертификации AppSource интеграции SAML не принимается.</span><span class="sxs-lookup"><span data-stu-id="81fd6-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="81fd6-108">Руководства и примеры кода</span><span class="sxs-lookup"><span data-stu-id="81fd6-108">Guides and code samples</span></span>
<span data-ttu-id="81fd6-109">При необходимости toolearn о toointegrate приложения с Azure Active Directory с помощью Open ID подключении, выполните наши руководства и примеры в hello кода [руководство разработчика Azure Active Directory](./active-directory-developers-guide.md#get-started "начало работы с Azure AD для разработчиков").</span><span class="sxs-lookup"><span data-stu-id="81fd6-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="81fd6-110">Мультитенантные приложения</span><span class="sxs-lookup"><span data-stu-id="81fd6-110">Multi-tenant applications</span></span>

<span data-ttu-id="81fd6-111">Приложение, принимающее вход пользователя из любой компании или организации с Azure Active Directory, не требуя отдельного экземпляра, конфигурации и развертывания, называется *многопользовательским приложением*.</span><span class="sxs-lookup"><span data-stu-id="81fd6-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="81fd6-112">AppSource Корпорация Майкрософт рекомендует, чтобы приложения реализован tooenable Многопользовательские приложения hello *щелчком* освободить пробная версия.</span><span class="sxs-lookup"><span data-stu-id="81fd6-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="81fd6-113">В порядке tooenable многопользовательский режим приложения:</span><span class="sxs-lookup"><span data-stu-id="81fd6-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="81fd6-114">Задать `Multi-Tenanted` свойство слишком`Yes` на сведения о регистрации приложения в hello [портала Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (по умолчанию, приложения, созданные в hello портала Azure настроены как *одногоклиента*)</span><span class="sxs-lookup"><span data-stu-id="81fd6-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="81fd6-115">Обновите ваш код toosend запросов toohello "`common`" конечной точки (обновить конечную точку hello из *https://login.microsoftonline.com/ {yourtenant}* слишком*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="81fd6-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="81fd6-116">Для некоторых платформ, например, ASP.NET, необходимо также tooupdate ваш код tooaccept нескольких издателей</span><span class="sxs-lookup"><span data-stu-id="81fd6-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="81fd6-117">Дополнительные сведения о мультитенантности см. в разделе: [как toosign любого пользователя Azure Active Directory (AD) с помощью hello шаблон многопользовательского приложения](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81fd6-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="81fd6-118">Приложения с одним клиентом</span><span class="sxs-lookup"><span data-stu-id="81fd6-118">Single-tenant applications</span></span>
<span data-ttu-id="81fd6-119">Приложения, которые принимают вход пользователей только из определенного экземпляра Azure Active Directory, называются *приложениями с одним клиентом*.</span><span class="sxs-lookup"><span data-stu-id="81fd6-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="81fd6-120">Внешние пользователи (включая рабочую или учебную учетные записи из других организаций или личной учетной записи) могут войти в приложение одного клиента tooa после добавления каждого пользователя в качестве *учетная запись гостя* экземпляр toohello Azure Active Directory приложение Hello зарегистрировано.</span><span class="sxs-lookup"><span data-stu-id="81fd6-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="81fd6-121">Можно добавлять пользователей в качестве tooan гостевых учетных записей Azure Active Directory через hello [ *совместной работы Azure AD B2B* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - и может быть выполнена [программном](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="81fd6-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="81fd6-122">При добавлении пользователя в качестве tooan гостевой учетной записи Azure Active Directory приглашение по электронной почте отправляется toohello пользователь, имеющий tooaccept hello приглашения, щелкнув ссылку hello по электронной почте приглашение hello.</span><span class="sxs-lookup"><span data-stu-id="81fd6-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="81fd6-123">Приглашения, отправляемых tooan дополнительных пользователей в организации приглашения, которая также является членом hello партнерской организации являются не требуется tooaccept toosign приглашения в.</span><span class="sxs-lookup"><span data-stu-id="81fd6-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="81fd6-124">Приложения одного клиента могут включить hello *контакт мне* столкнуться, но tooenable hello одним щелчком / свободного пробная версия рекомендует AppSource следует включить Многопользовательские приложения на работу приложения.</span><span class="sxs-lookup"><span data-stu-id="81fd6-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="81fd6-125">Пробные версии возможностей AppSource</span><span class="sxs-lookup"><span data-stu-id="81fd6-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="81fd6-126">Бесплатная пробная версия возможности (для заказчика)</span><span class="sxs-lookup"><span data-stu-id="81fd6-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="81fd6-127">Hello *заказчика пробной версии* оказывается hello рекомендует AppSource предоставляют приложении tooyour доступ одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="81fd6-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="81fd6-128">Ниже показано, как выглядит эта возможность.</span><span class="sxs-lookup"><span data-stu-id="81fd6-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="81fd6-129">Пользователь находит ваше приложение на веб-сайте AppSource.</span><span class="sxs-lookup"><span data-stu-id="81fd6-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="81fd6-130">Затем выбирает "Бесплатная пробная версия".</span><span class="sxs-lookup"><span data-stu-id="81fd6-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="81fd6-131">AppSource перенаправляет пользователя tooa URL-адрес веб-узла</span><span class="sxs-lookup"><span data-stu-id="81fd6-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="81fd6-132">Веб-сайт запускается hello <i>единый вход</i> процесса автоматически (при загрузке страницы)</span><span class="sxs-lookup"><span data-stu-id="81fd6-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="81fd6-133">Пользователь — страница перенаправления tooMicrosoft входа</span><span class="sxs-lookup"><span data-stu-id="81fd6-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="81fd6-134">Пользователь предоставляет учетные данные toosign в</span><span class="sxs-lookup"><span data-stu-id="81fd6-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="81fd6-135">Пользователь дает согласие для приложения.</span><span class="sxs-lookup"><span data-stu-id="81fd6-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="81fd6-136">Вход завершается, и пользователь является перенаправленный задней tooyour веб-сайта</span><span class="sxs-lookup"><span data-stu-id="81fd6-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="81fd6-137">Пользователь запускает hello бесплатной пробной версии</span><span class="sxs-lookup"><span data-stu-id="81fd6-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="81fd6-138">Функция "Связаться со мной" (партнерская пробная версия)</span><span class="sxs-lookup"><span data-stu-id="81fd6-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="81fd6-139">Hello *партнеров пробная версия* может использоваться, если вручную или долгосрочные операции требуется toohappen tooprovision hello пользователя / company: например, приложению tooprovision виртуальные машины, экземпляры базы данных или операций, которые занимают много времени toocomplete.</span><span class="sxs-lookup"><span data-stu-id="81fd6-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="81fd6-140">В этом случае после пользователь выбирает hello *«Пробный запрос»* кнопку и заполнении формы, AppSource отправляет hello контактные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="81fd6-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="81fd6-141">При получении этих сведений, а затем подготовить среду hello и отправить пользователю toohello hello инструкции о том, как tooaccess hello пробная версия:</span><span class="sxs-lookup"><span data-stu-id="81fd6-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="81fd6-142">Пользователь находит ваше приложение на веб-сайте AppSource.</span><span class="sxs-lookup"><span data-stu-id="81fd6-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="81fd6-143">Выбирает параметр "Связаться со мной".</span><span class="sxs-lookup"><span data-stu-id="81fd6-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="81fd6-144">Заполняет форму контактными данными.</span><span class="sxs-lookup"><span data-stu-id="81fd6-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="81fd6-145">Вы получаете сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="81fd6-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="81fd6-146">Настраиваете среду.</span><span class="sxs-lookup"><span data-stu-id="81fd6-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="81fd6-147">Связываетесь с пользователем по поводу информации о пробной версии.</span><span class="sxs-lookup"><span data-stu-id="81fd6-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="81fd6-148">Вы получаете сведения пользователя и настраиваете пробный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="81fd6-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="81fd6-149">Отправить tooaccess гиперссылки hello toohello пользователя вашего приложения</span><span class="sxs-lookup"><span data-stu-id="81fd6-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="81fd6-150">Пользователь получает доступ к приложения и процесса завершения hello-единого входа</span><span class="sxs-lookup"><span data-stu-id="81fd6-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="81fd6-151">Пользователь дает согласие для приложения.</span><span class="sxs-lookup"><span data-stu-id="81fd6-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="81fd6-152">Вход завершается, и пользователь является перенаправленный задней tooyour веб-сайта</span><span class="sxs-lookup"><span data-stu-id="81fd6-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="81fd6-153">Пользователь запускает hello бесплатной пробной версии</span><span class="sxs-lookup"><span data-stu-id="81fd6-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="81fd6-154">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="81fd6-154">More information</span></span>
<span data-ttu-id="81fd6-155">Дополнительные сведения о пробная версия AppSource hello см. в разделе [в этом видеоролике](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="81fd6-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="81fd6-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81fd6-156">Next Steps</span></span>

- <span data-ttu-id="81fd6-157">Дополнительные сведения о разработке приложений, поддерживающих вход с помощью Azure Active Directory, см. в статье [Сценарии аутентификации в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="81fd6-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="81fd6-158">Сведения о том, как toolist go см. приложение SaaS в AppSource, [информация о партнере AppSource](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="81fd6-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="81fd6-159">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="81fd6-159">Get Support</span></span>
<span data-ttu-id="81fd6-160">Интеграция Azure Active Directory, мы используем [переполнения стека](http://stackoverflow.com/questions/tagged/azure-active-directory) с поддержкой tooprovide сообщества hello.</span><span class="sxs-lookup"><span data-stu-id="81fd6-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="81fd6-161">Настоятельно рекомендуется сначала задать свои вопросы о переполнении стека в и обзор существующих toosee проблемы, если кто-то запрошенных ваш вопрос, прежде чем.</span><span class="sxs-lookup"><span data-stu-id="81fd6-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="81fd6-162">Пометьте вопросы и комментарии тегом `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="81fd6-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="81fd6-163">Используйте следующие комментарии раздел tooprovide отзыв hello и помогают уточнить и отформатировать содержимое веб-узла.</span><span class="sxs-lookup"><span data-stu-id="81fd6-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->