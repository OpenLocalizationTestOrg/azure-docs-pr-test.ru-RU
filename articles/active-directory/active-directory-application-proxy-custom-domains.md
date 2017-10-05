---
title: "Личные домены в прокси приложения Azure AD | Документация Майкрософт"
description: "Вы можете управлять личными доменами в прокси приложения Azure AD, чтобы использовать один и тот же URL-адрес для приложения вне зависимости от того, откуда к нему обращаются пользователи."
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="403ed-103">Работа с пользовательскими доменами в прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="403ed-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="403ed-104">При публикации приложения через прокси приложения Azure Active Directory можно создать внешний URL-адрес для перехода ваших пользователей при удаленной работе.</span><span class="sxs-lookup"><span data-stu-id="403ed-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="403ed-105">Имя этого URL-адреса содержит домен по умолчанию *ваш_клиент-msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="403ed-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="403ed-106">Например, если вы опубликовали приложение Expenses и используете клиент Contoso, то внешним URL-адресом будет https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="403ed-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="403ed-107">Если вы хотите использовать собственное доменное имя, настройте личный домен для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="403ed-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="403ed-108">Мы рекомендуем настраивать личные домены для ваших приложений, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="403ed-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="403ed-109">Ниже перечислены некоторые преимущества личных доменов.</span><span class="sxs-lookup"><span data-stu-id="403ed-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="403ed-110">Пользователи могут получить доступ к приложению, используя тот же URL-адрес, как при работе в сети, так и за ее пределами.</span><span class="sxs-lookup"><span data-stu-id="403ed-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="403ed-111">Если все ваши приложения имеют одинаковые внутренние и внешние URL-адреса, то ссылки в одном приложении, которые указывают на другое приложение, продолжат работать даже за пределами корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="403ed-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="403ed-112">Вы можете управлять фирменной символикой и создавать необходимые URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="403ed-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="403ed-113">Настройка личного домена</span><span class="sxs-lookup"><span data-stu-id="403ed-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="403ed-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="403ed-114">Prerequisites</span></span>

<span data-ttu-id="403ed-115">Прежде чем настроить личный домен, убедитесь, что у вас есть следующие необходимые компоненты:</span><span class="sxs-lookup"><span data-stu-id="403ed-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="403ed-116">[Проверенный домен, добавленный в Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="403ed-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="403ed-117">Пользовательский сертификат для домена в формате PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="403ed-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="403ed-118">Локальное приложение, [опубликованное через прокси приложение](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="403ed-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="403ed-119">Настройка личного домена</span><span class="sxs-lookup"><span data-stu-id="403ed-119">Configure your custom domain</span></span>

<span data-ttu-id="403ed-120">При наличии этих трех компонентов выполните указанные ниже действия для настройки личного домена.</span><span class="sxs-lookup"><span data-stu-id="403ed-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="403ed-121">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="403ed-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="403ed-122">Перейдите в **Azure Active Directory** > **Корпоративные приложения** > **Все приложения** и выберите приложение, которым необходимо управлять.</span><span class="sxs-lookup"><span data-stu-id="403ed-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="403ed-123">Выберите **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="403ed-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="403ed-124">Воспользуйтесь раскрывающимся списком в поле внешнего URL-адреса, чтобы выбрать личный домен.</span><span class="sxs-lookup"><span data-stu-id="403ed-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="403ed-125">Если ваш домен не отображается в списке, значит он еще не проверен.</span><span class="sxs-lookup"><span data-stu-id="403ed-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="403ed-126">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="403ed-126">Select **Save**</span></span>
5. <span data-ttu-id="403ed-127">Поле **Сертификат**, которое раньше было недоступным, станет доступным.</span><span class="sxs-lookup"><span data-stu-id="403ed-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="403ed-128">Выберите это поле.</span><span class="sxs-lookup"><span data-stu-id="403ed-128">Select this field.</span></span> 

   ![Щелкните, чтобы передать сертификат.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="403ed-130">Если вы уже передали сертификат для этого домена, то поле "Сертификат" отображает сведения об этом сертификате.</span><span class="sxs-lookup"><span data-stu-id="403ed-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="403ed-131">Передайте сертификат PFX и введите пароль к нему.</span><span class="sxs-lookup"><span data-stu-id="403ed-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="403ed-132">Выберите **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="403ed-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="403ed-133">Добавьте [запись DNS](../dns/dns-operations-recordsets-portal.md), которая перенаправляет новый внешний URL-адрес к домену msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="403ed-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="403ed-134">Для одного личного домена необходимо передать только один сертификат.</span><span class="sxs-lookup"><span data-stu-id="403ed-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="403ed-135">Когда сертификат будет передан, вы сможете выбрать личный домен при публикации нового приложения. Вам не нужно выполнять дополнительную настройку, за исключением записи DNS.</span><span class="sxs-lookup"><span data-stu-id="403ed-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="403ed-136">Управление сертификатами</span><span class="sxs-lookup"><span data-stu-id="403ed-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="403ed-137">Формат сертификата</span><span class="sxs-lookup"><span data-stu-id="403ed-137">Certificate format</span></span>
<span data-ttu-id="403ed-138">На методы подписки сертификатов нет никаких ограничений.</span><span class="sxs-lookup"><span data-stu-id="403ed-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="403ed-139">Поддерживается шифрование на основе эллиптических кривых (ECC), альтернативное имя субъекта (SAN) и другие стандартные типы сертификатов.</span><span class="sxs-lookup"><span data-stu-id="403ed-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="403ed-140">Можно использовать групповой сертификат, если он соответствует требуемому внешнему URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="403ed-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="403ed-141">Можно также использовать самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="403ed-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="403ed-142">При использовании частного центра сертификации CDP (точка распространения точки отзыва сертификата) для сертификата должна быть общедоступной.</span><span class="sxs-lookup"><span data-stu-id="403ed-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="403ed-143">Изменение домена</span><span class="sxs-lookup"><span data-stu-id="403ed-143">Changing the domain</span></span>
<span data-ttu-id="403ed-144">Все проверенные домены отображаются в раскрывающемся списке внешних URL-адресов для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="403ed-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="403ed-145">Чтобы изменить домен, просто обновите поле приложения.</span><span class="sxs-lookup"><span data-stu-id="403ed-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="403ed-146">Если в списке нет нужного домена, [добавьте его в качестве проверенного домена](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="403ed-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="403ed-147">Если вы выбрали домен без связанного сертификата, выполните шаги 5–7, чтобы добавить сертификат.</span><span class="sxs-lookup"><span data-stu-id="403ed-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="403ed-148">Затем убедитесь, что обновили запись DNS для перенаправления из нового внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="403ed-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="403ed-149">Управление сертификатами</span><span class="sxs-lookup"><span data-stu-id="403ed-149">Certificate management</span></span>
<span data-ttu-id="403ed-150">Вы можете использовать тот же сертификат для нескольких приложений, если они не находятся на одном и том же внешнем узле.</span><span class="sxs-lookup"><span data-stu-id="403ed-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="403ed-151">По истечении срока действия сертификата вы получите предупреждение о том, что необходимо передать другой сертификат с помощью портала.</span><span class="sxs-lookup"><span data-stu-id="403ed-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="403ed-152">Если сертификат отозван, пользователи могут увидеть предупреждение системы безопасности при получении доступа к приложению.</span><span class="sxs-lookup"><span data-stu-id="403ed-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="403ed-153">Проверки отзыва сертификатов не выполняются.</span><span class="sxs-lookup"><span data-stu-id="403ed-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="403ed-154">Чтобы обновить сертификат для нужного приложения, перейдите к приложению, выполните шаги 5–7 для настройки личных доменов в опубликованных приложениях и загрузите новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="403ed-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="403ed-155">Если старый сертификат не используется другими приложениями, он будет автоматически удален.</span><span class="sxs-lookup"><span data-stu-id="403ed-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="403ed-156">Сейчас все задачи управления сертификатами выполняются с помощью страниц отдельных приложений, поэтому необходимо управлять сертификатами в контексте соответствующих приложений.</span><span class="sxs-lookup"><span data-stu-id="403ed-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="403ed-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="403ed-157">Next steps</span></span>
* <span data-ttu-id="403ed-158">[Включите единый вход](active-directory-application-proxy-sso-using-kcd.md) в опубликованные приложения с помощью аутентификации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="403ed-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="403ed-159">[Включите условный доступ](active-directory-application-proxy-conditional-access.md) к опубликованным приложениям.</span><span class="sxs-lookup"><span data-stu-id="403ed-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="403ed-160">Добавление имени личного домена в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="403ed-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


