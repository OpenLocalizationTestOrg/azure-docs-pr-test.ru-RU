---
title: "Публикация собственных клиентских приложений — Azure AD | Документация Майкрософт"
description: "В этой статье описано, как включить собственные клиентские приложения для взаимодействия с соединителем прокси приложений Azure AD, чтобы обеспечить безопасный удаленный доступ к локальным приложениям."
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
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="aa625-103">Включение собственных клиентских приложений для взаимодействия с приложениями прокси</span><span class="sxs-lookup"><span data-stu-id="aa625-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="aa625-104">В дополнение к веб-приложениям, для публикации приложений собственного клиента можно использовать прокси приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa625-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="aa625-105">Приложения собственного клиента отличаются от веб-приложений, потому что они устанавливаются на устройство, а веб-приложения предоставляются через браузер.</span><span class="sxs-lookup"><span data-stu-id="aa625-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="aa625-106">Прокси приложения поддерживает приложения собственного клиента, принимая выданные маркеры Azure AD, отправляемые в стандартных заголовках HTTP "Authorize".</span><span class="sxs-lookup"><span data-stu-id="aa625-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Связь между конечными пользователями, Azure Active Directory и опубликованными приложениями](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="aa625-108">Используйте библиотеку аутентификации Azure AD, которая отвечает за аутентификацию и поддерживает многие клиентские среды, для публикации собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="aa625-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="aa625-109">Прокси приложения вписывается в [сценарий вызова веб-API собственным приложением](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="aa625-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="aa625-110">В этой статье рассматриваются четыре действия, которые нужно выполнить, чтобы опубликовать собственное приложение с помощью прокси приложения и библиотеки аутентификации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aa625-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="aa625-111">Шаг 1. Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="aa625-111">Step 1: Publish your application</span></span>
<span data-ttu-id="aa625-112">Опубликуйте приложение прокси, как любое другое приложение, и назначьте пользователей, имеющих доступ к вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="aa625-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="aa625-113">Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="aa625-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="aa625-114">Шаг 2. Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="aa625-114">Step 2: Configure your application</span></span>
<span data-ttu-id="aa625-115">Настройте собственное приложение, следуя инструкциям ниже.</span><span class="sxs-lookup"><span data-stu-id="aa625-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="aa625-116">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa625-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aa625-117">Выберите **Azure Active Directory** > **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="aa625-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="aa625-118">Выберите **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="aa625-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="aa625-119">Укажите имя приложения, выберите тип приложения **Машинный код** и укажите универсальный код ресурса (URI)универсальный код ресурса (URI) перенаправления для приложения.</span><span class="sxs-lookup"><span data-stu-id="aa625-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Создание регистрации приложения](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="aa625-121">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="aa625-121">Select **Create**.</span></span>

<span data-ttu-id="aa625-122">Дополнительные сведения о создании регистрации приложения см. в разделе [Интеграция приложений с Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="aa625-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="aa625-123">Шаг 3. Предоставление доступа для других приложений</span><span class="sxs-lookup"><span data-stu-id="aa625-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="aa625-124">Включите собственное приложение, которое должно быть доступно для других приложений в каталоге.</span><span class="sxs-lookup"><span data-stu-id="aa625-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="aa625-125">На странице **Регистрация приложений** выберите только что созданное собственное приложение.</span><span class="sxs-lookup"><span data-stu-id="aa625-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="aa625-126">Выберите **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="aa625-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="aa625-127">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="aa625-127">Select **Add**.</span></span>
4. <span data-ttu-id="aa625-128">Откройте первый шаг, **Выбор API**.</span><span class="sxs-lookup"><span data-stu-id="aa625-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="aa625-129">С помощью панели поиска найдите приложение прокси приложения, которое вы опубликовали в первом разделе.</span><span class="sxs-lookup"><span data-stu-id="aa625-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="aa625-130">Выберите это приложение и щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="aa625-130">Choose that app, then click **Select**.</span></span> 

   ![Поиск приложения прокси приложения](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="aa625-132">Откройте второй шаг, **Выбор разрешений**.</span><span class="sxs-lookup"><span data-stu-id="aa625-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="aa625-133">Установите соответствующий флажок, чтобы предоставить своему собственному приложению доступ к приложению прокси, а затем щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="aa625-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Предоставление доступа к приложению прокси приложения](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="aa625-135">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="aa625-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="aa625-136">Шаг 4. Изменение библиотеки проверки подлинности Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa625-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="aa625-137">Измените код собственного приложения с учетом проверки подлинности с помощью библиотеки Active Directory Authentication Library (ADAL). Для этого включите в код следующий текст:</span><span class="sxs-lookup"><span data-stu-id="aa625-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="aa625-138">Переменные в примере кода должны быть заменены следующим образом.</span><span class="sxs-lookup"><span data-stu-id="aa625-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="aa625-139">**Идентификатор клиента** находится на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="aa625-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="aa625-140">Выберите **Azure Active Directory** > **Свойства** и скопируйте идентификатор каталога.</span><span class="sxs-lookup"><span data-stu-id="aa625-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="aa625-141">**Внешний URL-адрес** — это интерфейсный URL-адрес, введенный в приложении прокси.</span><span class="sxs-lookup"><span data-stu-id="aa625-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="aa625-142">Чтобы найти это значение, перейдите в раздел **Прокси приложения** приложения прокси.</span><span class="sxs-lookup"><span data-stu-id="aa625-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="aa625-143">**Идентификатор приложения** собственного приложения находится на странице **Свойства** собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="aa625-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="aa625-144">Значение **Redirect URI of the native app** (URI перенаправления собственного клиента) находится на странице **URI перенаправления** собственного приложения.</span><span class="sxs-lookup"><span data-stu-id="aa625-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="aa625-145">См. также</span><span class="sxs-lookup"><span data-stu-id="aa625-145">See also</span></span>

<span data-ttu-id="aa625-146">Дополнительные сведения о блок-схеме собственного приложения см. в разделе [Из нативного приложения к веб-интерфейсу API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="aa625-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="aa625-147">Последние новости и обновления см. в [блоге, посвященном прокси приложения](http://blogs.technet.com/b/applicationproxyblog/).</span><span class="sxs-lookup"><span data-stu-id="aa625-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
