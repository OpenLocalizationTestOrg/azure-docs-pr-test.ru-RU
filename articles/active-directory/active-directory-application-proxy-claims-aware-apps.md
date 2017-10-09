---
title: "приложения, использующие aaaClaims - прокси приложения Azure AD | Документы Microsoft"
description: "Как toopublish локального приложения ASP.NET, принимающие утверждений служб федерации Active Directory для безопасного удаленного доступа пользователей."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="0c80f-103">Работа с приложениями, поддерживающими утверждения, в прокси приложения</span><span class="sxs-lookup"><span data-stu-id="0c80f-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="0c80f-104">[Приложения с поддержкой утверждений](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) выполнить перенаправление toohello службы маркеров безопасности (STS).</span><span class="sxs-lookup"><span data-stu-id="0c80f-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="0c80f-105">Hello STS запрашивает учетные данные пользователя hello в обмен на токен и затем перенаправляет toohello приложение hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="0c80f-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="0c80f-106">Существует несколько способов tooenable прокси приложения toowork с такие перенаправления.</span><span class="sxs-lookup"><span data-stu-id="0c80f-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="0c80f-107">Используйте этот tooconfigure статьи развертывания для приложений, поддерживающих утверждения.</span><span class="sxs-lookup"><span data-stu-id="0c80f-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0c80f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0c80f-108">Prerequisites</span></span>
<span data-ttu-id="0c80f-109">Убедитесь, что hello STS, hello приложение, поддерживающее утверждения перенаправляет toois доступны за пределами локальной сети.</span><span class="sxs-lookup"><span data-stu-id="0c80f-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="0c80f-110">Можно сделать hello STS доступных путем предоставления доступа к через прокси-сервер или, позволяя за пределами соединения.</span><span class="sxs-lookup"><span data-stu-id="0c80f-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="0c80f-111">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="0c80f-111">Publish your application</span></span>

1. <span data-ttu-id="0c80f-112">Опубликуйте приложение в соответствии с toohello инструкциям, описанным в [публикации приложений с помощью прокси приложения](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0c80f-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="0c80f-113">Перейдите toohello приложение-страница hello портала и выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0c80f-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="0c80f-114">Если для параметра **Метод предварительной проверки подлинности** выбрано значение **Azure Active Directory**, выберите для параметра **Метод внутренней проверки подлинности** значение **Единый вход Azure AD отключен**.</span><span class="sxs-lookup"><span data-stu-id="0c80f-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="0c80f-115">Если вы выбрали **Passthrough** как вашей **метод предварительной проверки подлинности**, не требуется toochange всего.</span><span class="sxs-lookup"><span data-stu-id="0c80f-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="0c80f-116">Настройка AD FS</span><span class="sxs-lookup"><span data-stu-id="0c80f-116">Configure ADFS</span></span>

<span data-ttu-id="0c80f-117">AD FS можно настроить для приложений, поддерживающих утверждения, одним из двух способов.</span><span class="sxs-lookup"><span data-stu-id="0c80f-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="0c80f-118">Привет, сначала при помощи пользовательских доменов.</span><span class="sxs-lookup"><span data-stu-id="0c80f-118">hello first is by using custom domains.</span></span> <span data-ttu-id="0c80f-119">Во-вторых, Hello — с WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="0c80f-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="0c80f-120">Вариант 1. Личные домены</span><span class="sxs-lookup"><span data-stu-id="0c80f-120">Option 1: Custom domains</span></span>

<span data-ttu-id="0c80f-121">Если все hello внутренние URL-адреса для приложения: полный доменные имена (FQDN), то можно настроить [пользовательских доменов](active-directory-application-proxy-custom-domains.md) для ваших приложений.</span><span class="sxs-lookup"><span data-stu-id="0c80f-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="0c80f-122">Используйте hello пользовательских доменов toocreate внешние URL-адреса, являются hello так же, как hello внутренние URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="0c80f-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="0c80f-123">Если внешний URL-адресов совпадают, внутренний URL-адресов, перенаправлений STS hello работать ли пользователи являются локального или удаленного.</span><span class="sxs-lookup"><span data-stu-id="0c80f-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="0c80f-124">Вариант 2. WS-Federation</span><span class="sxs-lookup"><span data-stu-id="0c80f-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="0c80f-125">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="0c80f-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="0c80f-126">Go слишком**доверия с проверяющей стороной**, щелкните правой кнопкой мыши приложение hello публикации с помощью прокси приложения и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="0c80f-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Щелчок правой кнопкой мыши имени приложения в разделе "Отношения доверия проверяющей стороны" (снимок экрана)](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="0c80f-128">На hello **конечные точки** в разделе **тип конечной точки**выберите **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="0c80f-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="0c80f-129">В разделе **доверенные URL-адрес**, введите URL-адрес hello, введенного в hello прокси приложения в разделе **внешний URL-адрес** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c80f-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Добавление конечной точки: задайте значение в поле «Доверенный URL-адрес» (снимок экрана)](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="0c80f-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c80f-131">Next steps</span></span>
* <span data-ttu-id="0c80f-132">[Включение единого входа](application-proxy-sso-overview.md) для приложений, не поддерживающих утверждения.</span><span class="sxs-lookup"><span data-stu-id="0c80f-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="0c80f-133">Включить toointeract собственного клиентского приложения с прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="0c80f-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


