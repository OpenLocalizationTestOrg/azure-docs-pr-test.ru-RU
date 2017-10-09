---
title: "приложения native client aaaPublish - Azure AD | Документы Microsoft"
description: "Рассматриваются как tooenable toocommunicate приложения собственного клиента с tooyour безопасный удаленный доступ соединитель прокси приложения Azure AD tooprovide локальных приложений."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="90bf0-103">Как tooenable toointeract приложения собственного клиента с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="90bf0-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="90bf0-104">В приложениях tooweb сложения прокси приложения Azure Active Directory также может быть используется toopublish приложения native client.</span><span class="sxs-lookup"><span data-stu-id="90bf0-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="90bf0-105">Приложения собственного клиента отличаются от веб-приложений, потому что они устанавливаются на устройство, а веб-приложения предоставляются через браузер.</span><span class="sxs-lookup"><span data-stu-id="90bf0-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="90bf0-106">Прокси приложения поддерживает приложения собственного клиента, принимая выданные маркеры Azure AD, отправляемые в стандартных заголовках HTTP "Authorize".</span><span class="sxs-lookup"><span data-stu-id="90bf0-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Связь между конечными пользователями, Azure Active Directory и опубликованными приложениями](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="90bf0-108">Используйте hello библиотеки аутентификации Azure AD, который отвечает за проверку подлинности и поддерживает многие клиентские среды, toopublish собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="90bf0-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="90bf0-109">Прокси приложения попадают hello [сценарий tooWeb API собственного приложения](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="90bf0-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="90bf0-110">В этой статье рассматриваются четыре шага hello toopublish собственное приложение с помощью прокси приложения и hello библиотеки аутентификации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90bf0-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="90bf0-111">Шаг 1. Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="90bf0-111">Step 1: Publish your application</span></span>
<span data-ttu-id="90bf0-112">Опубликовать приложение прокси-сервера, как и любое другое приложение и назначьте tooaccess пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="90bf0-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="90bf0-113">Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="90bf0-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="90bf0-114">Шаг 2. Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="90bf0-114">Step 2: Configure your application</span></span>
<span data-ttu-id="90bf0-115">Настройте собственное приложение, следуя инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="90bf0-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="90bf0-116">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90bf0-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="90bf0-117">Перейдите в слишком**Azure Active Directory** > **регистрации приложения**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="90bf0-118">Выберите **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="90bf0-119">Укажите имя для приложения, установите **собственного** как тип приложения hello и укажите hello URI перенаправления для приложения.</span><span class="sxs-lookup"><span data-stu-id="90bf0-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Создание регистрации приложения](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="90bf0-121">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-121">Select **Create**.</span></span>

<span data-ttu-id="90bf0-122">Дополнительные сведения о создании регистрации приложения см. в разделе [Интеграция приложений с Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="90bf0-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="90bf0-123">Шаг 3: Предоставление доступа tooother приложений</span><span class="sxs-lookup"><span data-stu-id="90bf0-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="90bf0-124">Включение приложений tooother toobe предоставляется собственное приложение hello в каталоге:</span><span class="sxs-lookup"><span data-stu-id="90bf0-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="90bf0-125">В по-прежнему **регистрации приложения**, выберите hello новый собственным приложением, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="90bf0-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="90bf0-126">Выберите **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="90bf0-127">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-127">Select **Add**.</span></span>
4. <span data-ttu-id="90bf0-128">Сначала откройте hello **выберите API**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="90bf0-129">Используйте hello поиска панели toofind прокси приложения приложение hello, которые опубликованы в первом разделе hello.</span><span class="sxs-lookup"><span data-stu-id="90bf0-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="90bf0-130">Выберите это приложение и щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-130">Choose that app, then click **Select**.</span></span> 

   ![Найдите приложение hello прокси-сервера](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="90bf0-132">Привет открыть второй этап, **разрешений Select**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="90bf0-133">Используйте флажок toogrant hello прокси приложения tooyour доступа собственное приложение, затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Предоставление доступа tooproxy приложения](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="90bf0-135">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="90bf0-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="90bf0-136">Шаг 4: Изменение hello библиотеку аутентификации Active Directory</span><span class="sxs-lookup"><span data-stu-id="90bf0-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="90bf0-137">Изменение кода собственное приложение hello в контекста проверки подлинности hello hello библиотеку проверки подлинности Active Directory (ADAL) tooinclude hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="90bf0-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="90bf0-138">переменные Hello в примере кода hello следует заменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="90bf0-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="90bf0-139">**Идентификатор клиента** можно найти в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="90bf0-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="90bf0-140">Перейдите в слишком**Azure Active Directory** > **свойства** и копирования hello идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="90bf0-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="90bf0-141">**Внешний URL-адрес** является hello переднего плана введенного URL-адреса в hello прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="90bf0-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="90bf0-142">toofind это значение, перейдите toohello **прокси приложения** раздел приложение hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="90bf0-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="90bf0-143">**Идентификатор приложения** hello собственное приложение можно найти на hello **свойства** страница hello собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="90bf0-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="90bf0-144">**URI перенаправления собственного приложения hello** можно найти на hello **URI перенаправления** страница hello собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="90bf0-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="90bf0-145">См. также</span><span class="sxs-lookup"><span data-stu-id="90bf0-145">See also</span></span>

<span data-ttu-id="90bf0-146">Дополнительные сведения о потоке собственное приложение hello см. в разделе [tooweb собственное приложение API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="90bf0-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="90bf0-147">Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="90bf0-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
