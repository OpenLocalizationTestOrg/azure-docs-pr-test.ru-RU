---
title: "aaaIntegrate Azure AD в приложение iOS | Документы Microsoft"
description: "Как toobuild приложения iOS, которое интегрируется с Azure AD для входа в систему и вызовы Azure AD защищены API-интерфейсов с помощью OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="b5bcf-103">Интеграция Azure AD в приложение для iOS</span><span class="sxs-lookup"><span data-stu-id="b5bcf-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="b5bcf-104">Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/iOS) , поможет вам приступить к работе с Azure Active Directory через несколько минут!</span><span class="sxs-lookup"><span data-stu-id="b5bcf-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="b5bcf-105">портал разработчиков Hello поможет выполнить hello регистрации приложения и интеграции Azure AD в коде.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="b5bcf-106">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="b5bcf-107">Azure Active Directory (Azure AD) предоставляет hello библиотеку аутентификации Active Directory или ADAL, для операций ввода-вывода клиентов, требующих tooaccess защищенным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="b5bcf-108">ADAL упрощает процесс hello, что ваше приложение использует токены доступа tooobtain.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="b5bcf-109">toodemonstrate примеры, в этой статье мы создаем список дел C цель приложения:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="b5bcf-110">Получает маркеры для вызова API Azure AD Graph hello с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="b5bcf-111">Осуществляет поиск пользователей в каталоге по псевдониму.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="b5bcf-112">toobuild hello полное рабочее приложение, необходимо:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="b5bcf-113">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="b5bcf-114">Установить и настроить ADAL.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="b5bcf-115">Используйте ADAL tooget токены из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="b5bcf-116">tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="b5bcf-117">Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="b5bcf-118">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="b5bcf-119">Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/iOS) , поможет вам приступить к работе с Azure AD через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="b5bcf-120">портал разработчиков Hello поможет выполнить hello регистрации приложения и интеграции Azure AD в коде.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="b5bcf-121">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="b5bcf-122">1. Выбор URI перенаправления для iOS</span><span class="sxs-lookup"><span data-stu-id="b5bcf-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="b5bcf-123">toosecurely запуск приложения в определенных сценариях единого входа, необходимо создать *URI перенаправления* в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="b5bcf-124">Перенаправление URI является используется tooensure, hello правильного приложения возвращаемого toohello токены, задаваемые для них.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="b5bcf-125">Hello операций ввода-вывода для перенаправления URI выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="b5bcf-126">Схема **aap-scheme** регистрируется в проекте XCode и</span><span class="sxs-lookup"><span data-stu-id="b5bcf-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="b5bcf-127">используется для вызова из других приложений.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-127">It is how other applications can call you.</span></span> <span data-ttu-id="b5bcf-128">Данные сведения можно найти в файле Info.plist (URL Types -> URL Identifier).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="b5bcf-129">Если вы еще не создали или не настроили хотя бы одну схему, следует сделать это.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="b5bcf-130">**Идентификатор пакета** -это hello пакет идентификатор, найденный в разделе «удостоверение» un параметров проекта в XCode.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="b5bcf-131">Пример для рассматриваемого проекта QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="b5bcf-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="b5bcf-132">2. Регистрация приложения hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="b5bcf-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="b5bcf-133">tooset копирование маркеры tooget приложения необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="b5bcf-134">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b5bcf-135">На верхней панели hello выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-135">On hello top bar, click your account.</span></span> <span data-ttu-id="b5bcf-136">В разделе hello **каталога** выберите hello клиента Active Directory, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="b5bcf-137">Нажмите кнопку **более служб** в hello панели навигации крайний слева, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b5bcf-138">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b5bcf-139">Выполните hello предлагает toocreate новый **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="b5bcf-140">Hello **имя** из hello приложения описывает tooend пользователей приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="b5bcf-141">Hello **Uri перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="b5bcf-142">Введите значение, которое является tooyour конкретного приложения и основан на данных URI перенаправления предыдущего hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="b5bcf-143">После завершения регистрации hello Azure AD присваивает приложения уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="b5bcf-144">Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="b5bcf-145">Из hello **параметры** выберите **требуемые разрешения** , а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="b5bcf-146">Выберите **Microsoft Graph** как hello API, а затем добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b5bcf-147">Это настраивает вашего приложения tooquery hello API Azure AD Graph для пользователей.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="b5bcf-148">3. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="b5bcf-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="b5bcf-149">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="b5bcf-150">Для ADAL toocommunicate с Azure AD необходимо tooprovide его с некоторые сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="b5bcf-151">Сначала добавьте ADAL toohello DirectorySearcher проекта с помощью CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="b5bcf-152">Добавьте следующие toothis podfile hello:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="b5bcf-153">Теперь можно Загрузите hello podfile с помощью CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="b5bcf-154">На этом шаге создается новая рабочая область XCode.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="b5bcf-155">В проекте hello краткое руководство, откройте файл plist hello `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="b5bcf-156">Замените hello значений элементов hello hello hello раздел tooreflect значения, введенные в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="b5bcf-157">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="b5bcf-158">Hello `tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="b5bcf-159">Hello `clientId` hello идентификатор клиента приложения, скопированный из портала hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="b5bcf-160">Hello `redirectUri` hello перенаправления URL-адрес, зарегистрированный в портале hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="b5bcf-161">4.    Используйте ADAL tooget токены из Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5bcf-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="b5bcf-162">Hello базовый принцип ADAL является что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает completionBlock `+(void) getToken : `, и ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="b5bcf-163">В hello `QuickStart` откройте проект `GraphAPICaller.m` и найдите hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` комментарий верхней hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="b5bcf-164">Здесь передать координаты ADAL hello через CompletionBlock toocommunicate с Azure AD и о том, как toocache маркеры.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="b5bcf-165">Теперь нам требуется toouse этот токен toosearch пользователями в hello graph.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="b5bcf-166">Найти hello `// TODO: implement SearchUsersList` комментарий.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="b5bcf-167">Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="b5bcf-168">tooquery hello Azure AD Graph API, необходимые tooinclude access_token в hello `Authorization` заголовок запроса hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="b5bcf-169">Вот где может пригодиться ADAL.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. <span data-ttu-id="b5bcf-170">Когда приложение запрашивает маркер путем вызова `getToken(...)`, ADAL пытается tooreturn маркер без запроса учетных данных пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="b5bcf-171">Если ADAL определит, что данный пользователь hello должен toosign в tooget маркер, он будет отображать диалоговое окно для входа в систему, собирать hello учетные данные пользователя и затем возвращает токен после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="b5bcf-172">Если ADAL не может tooreturn маркер по любой причине, он выдает `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="b5bcf-173">Hello `AuthenticationResult` объект содержит `tokenCacheStoreItem` объект, который может быть используется toocollect hello сведения, может потребоваться приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="b5bcf-174">В hello краткое руководство `tokenCacheStoreItem` — toodetermine используется, если проверка подлинности уже выполняется.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="b5bcf-175">5. Постройте и запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="b5bcf-175">5. Build and run hello application</span></span>
<span data-ttu-id="b5bcf-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b5bcf-176">Congratulations!</span></span> <span data-ttu-id="b5bcf-177">Теперь у вас есть рабочее приложение iOS, которое может проверять подлинность пользователей, безопасно вызывать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="b5bcf-178">Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="b5bcf-179">Запустите приложение QuickStart и выполните вход как один из пользователей.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="b5bcf-180">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="b5bcf-181">Закройте приложение hello и запустите его снова.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="b5bcf-182">Обратите внимание, что сеанс пользователя hello остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="b5bcf-183">ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="b5bcf-184">Он отвечает за всю работу dirty hello, таких как Управление кэшем поддержку протокола OAuth, представивший hello пользователя toosign пользовательского интерфейса в и обновление маркеры с истекшим сроком действия.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="b5bcf-185">Действительно требуется tooknow всего в одном вызове API `getToken`.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="b5bcf-186">Справочник по образец hello завершена (без настройки) предоставляется на [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b5bcf-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b5bcf-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5bcf-187">Next steps</span></span>
<span data-ttu-id="b5bcf-188">Теперь можно переходить на tooadditional сценариев.</span><span class="sxs-lookup"><span data-stu-id="b5bcf-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="b5bcf-189">Вы можете tootry:</span><span class="sxs-lookup"><span data-stu-id="b5bcf-189">You may want tootry:</span></span>

* [<span data-ttu-id="b5bcf-190">Безопасность веб-API с Azure AD для Node.JS</span><span class="sxs-lookup"><span data-stu-id="b5bcf-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="b5bcf-191">Дополнительные сведения [как tooenable SSO нескольких приложений на iOS с помощью ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="b5bcf-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

