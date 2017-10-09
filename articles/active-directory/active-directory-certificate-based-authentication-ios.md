---
title: "aaaAzure на основе сертификатов проверки подлинности Active Directory на iOS | Документы Microsoft"
description: "Дополнительные сведения о сценариях поддерживается hello и hello требования к настройке проверки подлинности на основе сертификата в решениях с устройствами iOS"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="f7755-103">Аутентификация на основе сертификата в Azure Active Directory на устройстве iOS</span><span class="sxs-lookup"><span data-stu-id="f7755-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="f7755-104">Проверку подлинности на основе сертификатов (CBA) обеспечивает проверку подлинности Azure Active Directory с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетную Exchange online с toobe:</span><span class="sxs-lookup"><span data-stu-id="f7755-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="f7755-105">мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;</span><span class="sxs-lookup"><span data-stu-id="f7755-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="f7755-106">клиентам Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="f7755-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="f7755-107">Эта настройка устраняет необходимость hello tooenter имя пользователя и пароль к нему в определенных почты и приложения Microsoft Office на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="f7755-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="f7755-108">В этом разделе приведены с hello требований и сценариев hello поддерживается настройка CBA на устройстве iOS(Android) для пользователей клиентов в Office 365 Enterprise, Business, образование, правительства США, Китае, и Германии планов.</span><span class="sxs-lookup"><span data-stu-id="f7755-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="f7755-109">В тарифных планах Office 365 US Government Defense и Federal доступна предварительная версия этой функции.</span><span class="sxs-lookup"><span data-stu-id="f7755-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="f7755-110">Поддержка мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="f7755-110">Office mobile applications support</span></span>

| <span data-ttu-id="f7755-111">Приложения</span><span class="sxs-lookup"><span data-stu-id="f7755-111">Apps</span></span> | <span data-ttu-id="f7755-112">Поддержка</span><span class="sxs-lookup"><span data-stu-id="f7755-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="f7755-113">Приложение Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="f7755-113">Azure Information Protection app</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f7755-115">Microsoft Teams</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="f7755-117">OneNote</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f7755-119">OneDrive</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="f7755-121">Outlook</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-123">Мобильные приложения Power BI</span><span class="sxs-lookup"><span data-stu-id="f7755-123">Power BI mobile apps</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-125">Skype для бизнеса</span><span class="sxs-lookup"><span data-stu-id="f7755-125">Skype for Business</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-127">Word/Excel/PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f7755-127">Word / Excel / PowerPoint</span></span> |![Проверка][1] |
| <span data-ttu-id="f7755-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="f7755-129">Yammer</span></span> |![Проверка][1] |


## <a name="requirements"></a><span data-ttu-id="f7755-131">Требования</span><span class="sxs-lookup"><span data-stu-id="f7755-131">Requirements</span></span> 

<span data-ttu-id="f7755-132">Hello ОС устройства должен иметь версию iOS 9 и более поздних версий</span><span class="sxs-lookup"><span data-stu-id="f7755-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="f7755-133">Необходимо настроить сервер федерации.</span><span class="sxs-lookup"><span data-stu-id="f7755-133">A federation server must be configured.</span></span>  

<span data-ttu-id="f7755-134">Для приложений Office на iOS требуется Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="f7755-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="f7755-135">Для Azure Active Directory toorevoke сертификат клиента маркер hello служб федерации Active Directory должен иметь hello следующих утверждений:</span><span class="sxs-lookup"><span data-stu-id="f7755-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="f7755-136">(hello серийный номер сертификата клиента hello)</span><span class="sxs-lookup"><span data-stu-id="f7755-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="f7755-137">(строка hello для hello издателя сертификата клиента hello)</span><span class="sxs-lookup"><span data-stu-id="f7755-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="f7755-138">Azure Active Directory добавляет маркер обновления toohello эти утверждения, если они доступны в маркере ADFS hello (или любой другой маркер SAML).</span><span class="sxs-lookup"><span data-stu-id="f7755-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="f7755-139">Когда токен обновления hello должен проверить toobe, информация, которая используется toocheck hello отзыва.</span><span class="sxs-lookup"><span data-stu-id="f7755-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="f7755-140">Рекомендуется следует обновить страницы ошибок ADFS hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f7755-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="f7755-141">Hello требование для установки средства проверки подлинности Microsoft hello на iOS</span><span class="sxs-lookup"><span data-stu-id="f7755-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="f7755-142">Инструкции о том, как tooget сертификат пользователя.</span><span class="sxs-lookup"><span data-stu-id="f7755-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="f7755-143">Дополнительные сведения см. в разделе [настройка страниц hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7755-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="f7755-144">Некоторые приложения Office (с включена современная проверка подлинности) отправлять "*prompt = имя входа*" tooAzure AD в свой запрос.</span><span class="sxs-lookup"><span data-stu-id="f7755-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="f7755-145">По умолчанию, Azure AD преобразует это в tooADFS hello запроса слишком "*wauth = usernamepassworduri*" (запрашивает auth U и P toodo ADFS) и "*wfresh = 0*" (запрашивает состояние единого входа tooignore служб федерации Active Directory и сделать дополнительной проверки подлинности) .</span><span class="sxs-lookup"><span data-stu-id="f7755-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="f7755-146">Если вы хотите tooenable на основе сертификатов проверки подлинности для этих приложений, необходимо toomodify hello по умолчанию Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7755-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="f7755-147">Просто набор hello "*PromptLoginBehavior*" в параметрах федеративного домена слишком "*отключено*".</span><span class="sxs-lookup"><span data-stu-id="f7755-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="f7755-148">Можно использовать hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform командлет этой задачи:</span><span class="sxs-lookup"><span data-stu-id="f7755-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="f7755-149">Поддержка клиентов Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="f7755-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="f7755-150">IOS 9 или более поздней версии поддерживается почтовый клиент hello машинным кодом iOS.</span><span class="sxs-lookup"><span data-stu-id="f7755-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="f7755-151">Все остальные приложения Exchange ActiveSync toodetermine Если эта возможность поддерживается, обратитесь в службу разработчика приложения.</span><span class="sxs-lookup"><span data-stu-id="f7755-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="f7755-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7755-152">Next steps</span></span>

<span data-ttu-id="f7755-153">Если требуется проверка подлинности на основе tooconfigure в вашей среде, см. раздел [приступить к работе с проверкой подлинности на основе сертификатов в Android](active-directory-certificate-based-authentication-get-started.md) инструкции.</span><span class="sxs-lookup"><span data-stu-id="f7755-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
