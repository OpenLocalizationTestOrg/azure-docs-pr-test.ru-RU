---
title: "aaaCustom домены в прокси приложения Azure AD | Документы Microsoft"
description: "Управление пользовательских доменов в прокси приложения Azure AD, поэтому hello URL-адреса для приложения hello hello одинаково независимо от того, где пользователям обращаться к ней."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="f10e0-103">Работа с пользовательскими доменами в прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10e0-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="f10e0-104">При публикации приложения с помощью прокси приложения Azure Active Directory создается внешний URL-адрес вашего toowhen toogo пользователей, которыми работает удаленно.</span><span class="sxs-lookup"><span data-stu-id="f10e0-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="f10e0-105">Этот URL-адрес Возвращает домен по умолчанию hello *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="f10e0-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="f10e0-106">Например если вы опубликовали приложение с именем расходы и вашего клиента называется Contoso, а затем hello внешний URL-адрес будет https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="f10e0-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="f10e0-107">Если требуется toouse собственное доменное имя, Настройка пользовательского домена для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f10e0-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="f10e0-108">Мы рекомендуем настраивать личные домены для ваших приложений, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="f10e0-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="f10e0-109">Ниже перечислены некоторые преимущества hello пользовательских доменов.</span><span class="sxs-lookup"><span data-stu-id="f10e0-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="f10e0-110">Пользователей можно заставить приложение toohello с hello же URL-адрес, находящихся внутри или за пределами вашей сети.</span><span class="sxs-lookup"><span data-stu-id="f10e0-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="f10e0-111">Если все ваши приложения имеют hello же внутренние и внешние URL-адреса, ссылки в одном приложении, указывающие tooanother продолжить toowork даже за пределами корпоративной сети hello.</span><span class="sxs-lookup"><span data-stu-id="f10e0-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="f10e0-112">Управлять вашей фирменная символика и hello URL-адреса, нужно создать.</span><span class="sxs-lookup"><span data-stu-id="f10e0-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="f10e0-113">Настройка личного домена</span><span class="sxs-lookup"><span data-stu-id="f10e0-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f10e0-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f10e0-114">Prerequisites</span></span>

<span data-ttu-id="f10e0-115">Прежде чем настраивать пользовательский домен, убедитесь, что hello следующие требования, которые подготовлены:</span><span class="sxs-lookup"><span data-stu-id="f10e0-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="f10e0-116">Объект [проверенный домен добавлен tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f10e0-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="f10e0-117">Пользовательский сертификат для домена hello в форме hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="f10e0-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="f10e0-118">Локальное приложение, [опубликованное через прокси приложение](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f10e0-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="f10e0-119">Настройка личного домена</span><span class="sxs-lookup"><span data-stu-id="f10e0-119">Configure your custom domain</span></span>

<span data-ttu-id="f10e0-120">При наличии эти три требования готова, выполните эти шаги tooset копирование вашего домена.</span><span class="sxs-lookup"><span data-stu-id="f10e0-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="f10e0-121">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f10e0-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f10e0-122">Перейдите в слишком**Azure Active Directory** > **корпоративных приложений** > **всех приложений** и выберите приложение hello требуется toomanage.</span><span class="sxs-lookup"><span data-stu-id="f10e0-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="f10e0-123">Выберите **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="f10e0-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="f10e0-124">В поле hello внешний URL-адрес с помощью hello раскрывающегося списка tooselect вашего домена.</span><span class="sxs-lookup"><span data-stu-id="f10e0-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="f10e0-125">Если вы не видите домен в списке hello, затем он еще не была проверена еще.</span><span class="sxs-lookup"><span data-stu-id="f10e0-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="f10e0-126">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f10e0-126">Select **Save**</span></span>
5. <span data-ttu-id="f10e0-127">Hello **сертификат** становится доступным поле, которое было отключено.</span><span class="sxs-lookup"><span data-stu-id="f10e0-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="f10e0-128">Выберите это поле.</span><span class="sxs-lookup"><span data-stu-id="f10e0-128">Select this field.</span></span> 

   ![Нажмите кнопку tooupload сертификата](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="f10e0-130">Если вы уже отправили сертификат для этого домена, в поле сертификата hello отображает сведения о сертификате hello.</span><span class="sxs-lookup"><span data-stu-id="f10e0-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="f10e0-131">Отправка сертификата PFX hello и введите пароль hello hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="f10e0-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="f10e0-132">Выберите **Сохранить** toosave изменения.</span><span class="sxs-lookup"><span data-stu-id="f10e0-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="f10e0-133">Добавить [запись DNS](../dns/dns-operations-recordsets-portal.md) что перенаправления hello нового внешнего домена msappproxy.net toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f10e0-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="f10e0-134">Требуется только один сертификат tooupload каждого пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="f10e0-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="f10e0-135">После отправки сертификата можно hello пользовательского домена, при публикации нового приложения и имеет toodo дополнительная настройка за исключением hello DNS-запись.</span><span class="sxs-lookup"><span data-stu-id="f10e0-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="f10e0-136">Управление сертификатами</span><span class="sxs-lookup"><span data-stu-id="f10e0-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="f10e0-137">Формат сертификата</span><span class="sxs-lookup"><span data-stu-id="f10e0-137">Certificate format</span></span>
<span data-ttu-id="f10e0-138">Нет никаких ограничений на hello сертификат подписи методов.</span><span class="sxs-lookup"><span data-stu-id="f10e0-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="f10e0-139">Поддерживается шифрование на основе эллиптических кривых (ECC), альтернативное имя субъекта (SAN) и другие стандартные типы сертификатов.</span><span class="sxs-lookup"><span data-stu-id="f10e0-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="f10e0-140">До тех пор, пока hello подстановочный знак соответствует требуемой hello внешний URL-адрес можно использовать сертификат с подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="f10e0-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="f10e0-141">Можно также использовать самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="f10e0-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="f10e0-142">Если вы используете закрытым центром сертификации, hello CDP (точка распространения точки отзыва сертификатов) для сертификата hello должны быть открытыми.</span><span class="sxs-lookup"><span data-stu-id="f10e0-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="f10e0-143">Изменение домена hello</span><span class="sxs-lookup"><span data-stu-id="f10e0-143">Changing hello domain</span></span>
<span data-ttu-id="f10e0-144">Все проверенных доменов отображаются в hello внешний URL-адрес раскрывающийся список для приложения.</span><span class="sxs-lookup"><span data-stu-id="f10e0-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="f10e0-145">домен toochange hello, обновите это поле для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f10e0-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="f10e0-146">Если hello домена, отсутствует в списке hello [добавьте его как проверенный домен](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f10e0-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="f10e0-147">Если выбрать домен, который еще не имеет соответствующий сертификат, выполните шаги 5 – 7 tooadd hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="f10e0-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="f10e0-148">Затем убедитесь, что обновление hello tooredirect записи DNS из hello новый внешний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f10e0-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="f10e0-149">Управление сертификатами</span><span class="sxs-lookup"><span data-stu-id="f10e0-149">Certificate management</span></span>
<span data-ttu-id="f10e0-150">Можно использовать приветствия же сертификатов для нескольких приложений, если приложения hello имеют внешнем узле.</span><span class="sxs-lookup"><span data-stu-id="f10e0-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="f10e0-151">Вы получите предупреждение по истечении срока действия сертификата о том, tooupload другой сертификат через портал hello.</span><span class="sxs-lookup"><span data-stu-id="f10e0-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="f10e0-152">Если hello сертификат отозван, пользователям может появиться следующее предупреждение безопасности, при доступе к приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f10e0-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="f10e0-153">Проверки отзыва сертификатов не выполняются.</span><span class="sxs-lookup"><span data-stu-id="f10e0-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="f10e0-154">tooupdate hello сертификат для данного приложения, перейдите toohello приложение и выполните шаги 5 – 7 для настройки пользовательских доменов на tooupload опубликованные приложения новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="f10e0-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="f10e0-155">Если Здравствуй, старый сертификат не используется другими приложениями, она будет автоматически удалена.</span><span class="sxs-lookup"><span data-stu-id="f10e0-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="f10e0-156">В настоящее время все управление сертификатами является приложения на отдельных страницах, поэтому вам необходимо toomanage сертификаты в контексте hello hello соответствующих приложений.</span><span class="sxs-lookup"><span data-stu-id="f10e0-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f10e0-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f10e0-157">Next steps</span></span>
* <span data-ttu-id="f10e0-158">[Включить единый вход](active-directory-application-proxy-sso-using-kcd.md) tooyour опубликованных приложений с помощью проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f10e0-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="f10e0-159">[Включить условный доступ](active-directory-application-proxy-conditional-access.md) tooyour опубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="f10e0-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="f10e0-160">Добавить к tooAzure имя пользовательского домена AD</span><span class="sxs-lookup"><span data-stu-id="f10e0-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


