---
title: "aaaAzure на основе сертификатов проверки подлинности Active Directory на Android | Документы Microsoft"
description: "Дополнительные сведения о сценарии hello поддерживается и hello требования для настройки проверки подлинности на основе сертификата в решениях с устройства Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="5d8d5-103">Аутентификация на основе сертификата в Azure Active Directory на устройстве Android</span><span class="sxs-lookup"><span data-stu-id="5d8d5-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="5d8d5-104">Проверку подлинности на основе сертификатов (CBA) обеспечивает проверку подлинности Azure Active Directory с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетную Exchange online с toobe:</span><span class="sxs-lookup"><span data-stu-id="5d8d5-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="5d8d5-105">мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;</span><span class="sxs-lookup"><span data-stu-id="5d8d5-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="5d8d5-106">клиентам Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="5d8d5-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="5d8d5-107">Эта настройка устраняет необходимость hello tooenter имя пользователя и пароль к нему в определенных почты и приложения Microsoft Office на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="5d8d5-108">В этом разделе приведены с hello требований и сценариев hello поддерживается настройка CBA на устройстве iOS(Android) для пользователей клиентов в Office 365 Enterprise, Business, образование, правительства США, Китае, и Германии планов.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="5d8d5-109">В тарифных планах Office 365 US Government Defense и Federal доступна предварительная версия этой функции.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="5d8d5-110">Поддержка мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="5d8d5-110">Office mobile applications support</span></span>
| <span data-ttu-id="5d8d5-111">Приложения</span><span class="sxs-lookup"><span data-stu-id="5d8d5-111">Apps</span></span> | <span data-ttu-id="5d8d5-112">Поддержка</span><span class="sxs-lookup"><span data-stu-id="5d8d5-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="5d8d5-113">Приложение Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="5d8d5-113">Azure Information Protection app</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5d8d5-115">Microsoft Teams</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="5d8d5-117">OneNote</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="5d8d5-119">OneDrive</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="5d8d5-121">Outlook</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-123">Мобильные приложения Power BI</span><span class="sxs-lookup"><span data-stu-id="5d8d5-123">Power BI mobile apps</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-125">Skype для бизнеса</span><span class="sxs-lookup"><span data-stu-id="5d8d5-125">Skype for Business</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-127">Word/Excel/PowerPoint</span><span class="sxs-lookup"><span data-stu-id="5d8d5-127">Word / Excel / PowerPoint</span></span> |![Проверка][1] |
| <span data-ttu-id="5d8d5-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="5d8d5-129">Yammer</span></span> |![Проверка][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="5d8d5-131">Требования к реализации</span><span class="sxs-lookup"><span data-stu-id="5d8d5-131">Implementation requirements</span></span>

<span data-ttu-id="5d8d5-132">Hello версия ОС устройства должны быть Android 5.0 (без описания операций) и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="5d8d5-133">Необходимо настроить сервер федерации.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-133">A federation server must be configured.</span></span>  

<span data-ttu-id="5d8d5-134">Для Azure Active Directory toorevoke сертификат клиента маркер hello служб федерации Active Directory должен иметь hello следующих утверждений:</span><span class="sxs-lookup"><span data-stu-id="5d8d5-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="5d8d5-135">(hello серийный номер сертификата клиента hello)</span><span class="sxs-lookup"><span data-stu-id="5d8d5-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="5d8d5-136">(строка hello для hello издателя сертификата клиента hello)</span><span class="sxs-lookup"><span data-stu-id="5d8d5-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="5d8d5-137">Azure Active Directory добавляет маркер обновления toohello эти утверждения, если они доступны в маркере ADFS hello (или любой другой маркер SAML).</span><span class="sxs-lookup"><span data-stu-id="5d8d5-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="5d8d5-138">Когда токен обновления hello должен проверить toobe, информация, которая используется toocheck hello отзыва.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="5d8d5-139">Рекомендуется, следует обновить страницы ошибок hello ADFS с инструкциями о том, как tooget сертификат пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="5d8d5-140">Дополнительные сведения см. в разделе [настройка страниц hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d8d5-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="5d8d5-141">Некоторые приложения Office (с включена современная проверка подлинности) отправлять "*prompt = имя входа*" tooAzure AD в свой запрос.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="5d8d5-142">По умолчанию, Azure AD преобразует это в tooADFS hello запроса слишком "*wauth = usernamepassworduri*" (запрашивает auth U и P toodo ADFS) и "*wfresh = 0*" (запрашивает состояние единого входа tooignore служб федерации Active Directory и сделать дополнительной проверки подлинности) .</span><span class="sxs-lookup"><span data-stu-id="5d8d5-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="5d8d5-143">Если вы хотите tooenable на основе сертификатов проверки подлинности для этих приложений, необходимо toomodify hello по умолчанию Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="5d8d5-144">Просто набор hello "*PromptLoginBehavior*" в параметрах федеративного домена слишком "*отключено*".</span><span class="sxs-lookup"><span data-stu-id="5d8d5-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="5d8d5-145">Можно использовать hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform командлет этой задачи:</span><span class="sxs-lookup"><span data-stu-id="5d8d5-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="5d8d5-146">Поддержка клиентов Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="5d8d5-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="5d8d5-147">Поддерживаются некоторые приложения Exchange ActiveSync, работающие на Android 5.0 (Lollipop) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="5d8d5-148">toodetermine при приложение электронной почты поддерживают эту функцию, обратитесь к разработчику вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5d8d5-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d8d5-149">Next steps</span></span>

<span data-ttu-id="5d8d5-150">Если требуется проверка подлинности на основе tooconfigure в вашей среде, см. раздел [приступить к работе с проверкой подлинности на основе сертификатов в Android](active-directory-certificate-based-authentication-get-started.md) инструкции.</span><span class="sxs-lookup"><span data-stu-id="5d8d5-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
