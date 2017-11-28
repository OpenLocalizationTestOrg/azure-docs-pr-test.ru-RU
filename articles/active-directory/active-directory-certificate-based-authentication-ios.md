---
title: "Аутентификация на основе сертификата в Azure Active Directory на устройстве iOS | Документация Майкрософт"
description: "Узнайте о поддерживаемых сценариях и требованиях к настройке аутентификации на основе сертификата в решениях на устройствах iOS."
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
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="178ec-103">Аутентификация на основе сертификата в Azure Active Directory на устройстве iOS</span><span class="sxs-lookup"><span data-stu-id="178ec-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="178ec-104">Аутентификация на основе сертификата (CBA) позволяет Azure Active Directory выполнять аутентификацию с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетной записи Exchange Online к:</span><span class="sxs-lookup"><span data-stu-id="178ec-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="178ec-105">мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;</span><span class="sxs-lookup"><span data-stu-id="178ec-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="178ec-106">клиентам Exchange ActiveSync (EAS).</span><span class="sxs-lookup"><span data-stu-id="178ec-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="178ec-107">Настройка данной функции избавляет от необходимости ввода имени пользователя и пароля в определенных почтовых клиентах и приложениях Microsoft Office на мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="178ec-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="178ec-108">В этой статье приведены требования и поддерживаемые сценарии для настройки CBA на устройстве iOS (Android) для пользователей клиентов в тарифных планах Office 365 корпоративный, бизнес, для образования, для государственных организаций США, Китая и Германии.</span><span class="sxs-lookup"><span data-stu-id="178ec-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="178ec-109">В тарифных планах Office 365 US Government Defense и Federal доступна предварительная версия этой функции.</span><span class="sxs-lookup"><span data-stu-id="178ec-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="178ec-110">Поддержка мобильных приложений Office</span><span class="sxs-lookup"><span data-stu-id="178ec-110">Office mobile applications support</span></span>

| <span data-ttu-id="178ec-111">Приложения</span><span class="sxs-lookup"><span data-stu-id="178ec-111">Apps</span></span> | <span data-ttu-id="178ec-112">Поддержка</span><span class="sxs-lookup"><span data-stu-id="178ec-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="178ec-113">Приложение Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="178ec-113">Azure Information Protection app</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="178ec-115">Microsoft Teams</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="178ec-117">OneNote</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="178ec-119">OneDrive</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="178ec-121">Outlook</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-123">Мобильные приложения Power BI</span><span class="sxs-lookup"><span data-stu-id="178ec-123">Power BI mobile apps</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-125">Skype для бизнеса</span><span class="sxs-lookup"><span data-stu-id="178ec-125">Skype for Business</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-127">Word/Excel/PowerPoint</span><span class="sxs-lookup"><span data-stu-id="178ec-127">Word / Excel / PowerPoint</span></span> |![Проверка][1] |
| <span data-ttu-id="178ec-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="178ec-129">Yammer</span></span> |![Проверка][1] |


## <a name="requirements"></a><span data-ttu-id="178ec-131">Требования</span><span class="sxs-lookup"><span data-stu-id="178ec-131">Requirements</span></span> 

<span data-ttu-id="178ec-132">Устройство должно иметь операционную систему iOS 9 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="178ec-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="178ec-133">Необходимо настроить сервер федерации.</span><span class="sxs-lookup"><span data-stu-id="178ec-133">A federation server must be configured.</span></span>  

<span data-ttu-id="178ec-134">Для приложений Office на iOS требуется Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="178ec-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="178ec-135">Чтобы служба Azure Active Directory могла отзывать сертификат клиента, маркер AD FS должен иметь следующие утверждения:</span><span class="sxs-lookup"><span data-stu-id="178ec-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="178ec-136">(серийный номер сертификата клиента);</span><span class="sxs-lookup"><span data-stu-id="178ec-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="178ec-137">(строка для издателя сертификата клиента).</span><span class="sxs-lookup"><span data-stu-id="178ec-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="178ec-138">Azure Active Directory добавляет эти утверждения в маркер обновления, если они доступны в маркере AD FS (или любом другом токене SAML).</span><span class="sxs-lookup"><span data-stu-id="178ec-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="178ec-139">Когда требуется проверить маркер обновления, эта информация используется для проверки отзыва.</span><span class="sxs-lookup"><span data-stu-id="178ec-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="178ec-140">Рекомендуется обновить страницы ошибок AD FS следующими сведениями:</span><span class="sxs-lookup"><span data-stu-id="178ec-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="178ec-141">требованием установки Microsoft Authenticator для iOS;</span><span class="sxs-lookup"><span data-stu-id="178ec-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="178ec-142">инструкциями о получении сертификата пользователя.</span><span class="sxs-lookup"><span data-stu-id="178ec-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="178ec-143">Дополнительные сведения см. в разделе [Настройка страниц входа AD FS](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="178ec-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="178ec-144">Некоторые приложения Office (с поддержкой современной проверки подлинности) отправляют в Azure AD запрос с текстом *prompt=login*.</span><span class="sxs-lookup"><span data-stu-id="178ec-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="178ec-145">По умолчанию Azure AD преобразует этот текст в запросе к службам AD FS в текст *wauth=usernamepassworduri* (запрашивает у AD FS выполнение проверки подлинности с помощью имени пользователя и пароля) и *wfresh=0* (запрашивает у AD FS игнорировать состояние единого входа и выполнять проверку подлинности заново).</span><span class="sxs-lookup"><span data-stu-id="178ec-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="178ec-146">Чтобы включить проверку подлинности на основе сертификатов для этих приложений, необходимо изменить поведение Azure AD по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="178ec-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="178ec-147">Просто задайте для параметра *PromptLoginBehavior* в настройках федеративного домена значение *Отключено*.</span><span class="sxs-lookup"><span data-stu-id="178ec-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="178ec-148">Для выполнения этой задачи можно использовать командлет [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):</span><span class="sxs-lookup"><span data-stu-id="178ec-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="178ec-149">Поддержка клиентов Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="178ec-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="178ec-150">В iOS версии 9 и выше поддерживается собственный почтовый клиент iOS.</span><span class="sxs-lookup"><span data-stu-id="178ec-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="178ec-151">Чтобы определить, поддерживается ли эта функция во всех остальных приложениях Exchange ActiveSync, обратитесь к разработчику приложения.</span><span class="sxs-lookup"><span data-stu-id="178ec-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="178ec-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="178ec-152">Next steps</span></span>

<span data-ttu-id="178ec-153">Чтобы настроить аутентификацию на основе сертификата в своей среде, ознакомьтесь с инструкциями в статье [Get started with certificate-based authentication in Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) (Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="178ec-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
