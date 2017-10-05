---
title: "Интеграция Azure AD в приложение для iOS | Документы Майкрософт"
description: "Практическое руководство по созданию приложения для iOS, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищенные Azure AD, по протоколу OAuth."
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="1c791-103">Интеграция Azure AD в приложение для iOS</span><span class="sxs-lookup"><span data-stu-id="1c791-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="1c791-104">Воспользуйтесь предварительной версией нашего нового [портала разработчиков](https://identity.microsoft.com/Docs/iOS), который поможет вам приступить к работе с Azure Active Directory через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1c791-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="1c791-105">Портал разработчиков поможет зарегистрировать приложение и интегрировать Azure AD в код.</span><span class="sxs-lookup"><span data-stu-id="1c791-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="1c791-106">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="1c791-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="1c791-107">Клиентские приложения для iOS, которым необходим доступ к защищенным ресурсам, могут использовать библиотеку проверки подлинности Azure AD (ADAL), предоставляемую Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c791-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="1c791-108">ADAL упрощает процесс, который приложение использует для получения маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="1c791-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="1c791-109">Чтобы показать, насколько это просто, в этом руководстве описывается создание приложения "Список дел" на Objective, которое:</span><span class="sxs-lookup"><span data-stu-id="1c791-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="1c791-110">получает маркеры доступа для вызова интерфейса API Graph Azure AD с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="1c791-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="1c791-111">Осуществляет поиск пользователей в каталоге по псевдониму.</span><span class="sxs-lookup"><span data-stu-id="1c791-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="1c791-112">Для создания полного и действующего приложения вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="1c791-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="1c791-113">Зарегистрировать приложение в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c791-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="1c791-114">Установить и настроить ADAL.</span><span class="sxs-lookup"><span data-stu-id="1c791-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="1c791-115">использовать ADAL для получения маркеров из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c791-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="1c791-116">Чтобы начать работу, [скачайте схему приложения](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) или [скачайте готовый пример](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1c791-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="1c791-117">Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="1c791-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="1c791-118">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1c791-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="1c791-119">Воспользуйтесь предварительной версией нашего нового [портала разработчиков](https://identity.microsoft.com/Docs/iOS), который поможет вам приступить к работе с Azure AD через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1c791-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="1c791-120">Портал разработчиков поможет зарегистрировать приложение и интегрировать Azure AD в код.</span><span class="sxs-lookup"><span data-stu-id="1c791-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="1c791-121">Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.</span><span class="sxs-lookup"><span data-stu-id="1c791-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="1c791-122">1. Выбор URI перенаправления для iOS</span><span class="sxs-lookup"><span data-stu-id="1c791-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="1c791-123">Для безопасного запуска приложений в некоторых сценариях использования единого входа требуется создать *URI перенаправления* в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="1c791-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="1c791-124">URI перенаправления используется, чтобы гарантировать, что маркеры получает именно то приложение, которое их запрашивало.</span><span class="sxs-lookup"><span data-stu-id="1c791-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="1c791-125">Формат URI перенаправления в iOS:</span><span class="sxs-lookup"><span data-stu-id="1c791-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="1c791-126">Схема **aap-scheme** регистрируется в проекте XCode и</span><span class="sxs-lookup"><span data-stu-id="1c791-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="1c791-127">используется для вызова из других приложений.</span><span class="sxs-lookup"><span data-stu-id="1c791-127">It is how other applications can call you.</span></span> <span data-ttu-id="1c791-128">Данные сведения можно найти в файле Info.plist (URL Types -> URL Identifier).</span><span class="sxs-lookup"><span data-stu-id="1c791-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="1c791-129">Если вы еще не создали или не настроили хотя бы одну схему, следует сделать это.</span><span class="sxs-lookup"><span data-stu-id="1c791-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="1c791-130">**bundle-id** — это идентификатор пакета, который можно найти в разделе "identity" параметров проекта XCode.</span><span class="sxs-lookup"><span data-stu-id="1c791-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="1c791-131">Пример для рассматриваемого проекта QuickStart: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="1c791-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="1c791-132">2) Регистрация приложения DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="1c791-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="1c791-133">Чтобы настроить приложение для получения маркеров, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу API Graph для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c791-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="1c791-134">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c791-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c791-135">На верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="1c791-135">On the top bar, click your account.</span></span> <span data-ttu-id="1c791-136">В списке **Каталог** выберите клиент Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="1c791-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="1c791-137">В области навигации слева щелкните **Дополнительные службы**, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c791-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1c791-138">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c791-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1c791-139">Следуйте инструкциям на экране, чтобы создать **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="1c791-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="1c791-140">**Имя** приложения служит его описанием для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="1c791-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="1c791-141">**URI перенаправления** представляет собой сочетание схемы и строки, используемое Azure AD для возвращения ответов маркеров.</span><span class="sxs-lookup"><span data-stu-id="1c791-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="1c791-142">Введите значение, которое зависит от приложения и основано на предыдущей информации об URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="1c791-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="1c791-143">После завершения регистрации Azure AD присваивает приложению уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1c791-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="1c791-144">Это значение вам понадобится в следующих разделах, поэтому скопируйте его с вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="1c791-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="1c791-145">На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c791-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="1c791-146">Выберите **Microsoft Graph** в качестве интерфейса API и добавьте разрешение **Чтение данных каталога** в списке **Делегированные разрешения**.</span><span class="sxs-lookup"><span data-stu-id="1c791-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="1c791-147">Это позволит приложению запрашивать интерфейс Graph API для пользователей.</span><span class="sxs-lookup"><span data-stu-id="1c791-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="1c791-148">3. Установка и настройка ADAL</span><span class="sxs-lookup"><span data-stu-id="1c791-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="1c791-149">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="1c791-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="1c791-150">Чтобы ADAL могла обмениваться информацией с Azure AD, необходимо предоставить некоторую информацию о регистрации вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1c791-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="1c791-151">Для начала добавьте ADAL в проект DirectorySearcher, используя Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="1c791-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="1c791-152">Добавьте в файл Podfile следующий код:</span><span class="sxs-lookup"><span data-stu-id="1c791-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="1c791-153">Теперь загрузите профиль с помощью CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="1c791-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="1c791-154">На этом шаге создается новая рабочая область XCode.</span><span class="sxs-lookup"><span data-stu-id="1c791-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="1c791-155">В проекте QuickStart откройте файл `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="1c791-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="1c791-156">Замените значения элементов в соответствующем разделе на значения, указанные на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1c791-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="1c791-157">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="1c791-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="1c791-158">`tenant` — это имя вашего клиента Azure AD, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1c791-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="1c791-159">Для `clientId` укажите скопированный на портале идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="1c791-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="1c791-160">`redirectUri` — это URL-адрес перенаправления, зарегистрированный на портале.</span><span class="sxs-lookup"><span data-stu-id="1c791-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="1c791-161">4.    Использование ADAL для получения маркеров из Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c791-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="1c791-162">Основной принцип ADAL состоит в том, что каждый раз, когда вашему приложению необходим маркер доступа, оно будет просто вызывать сompletionBlock `+(void) getToken : `, а библиотека ADAL сделает все остальное.</span><span class="sxs-lookup"><span data-stu-id="1c791-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="1c791-163">В проекте `QuickStart` откройте `GraphAPICaller.m` и найдите комментарий "`// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.`" вверху.</span><span class="sxs-lookup"><span data-stu-id="1c791-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="1c791-164">Здесь вы указываете координаты, которые требуются библиотеке ADAL для взаимодействия с Azure AD, и сообщаете способ кэширования маркеров.</span><span class="sxs-lookup"><span data-stu-id="1c791-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="1c791-165">Мы будем использовать этот маркер для поиска пользователей в графе.</span><span class="sxs-lookup"><span data-stu-id="1c791-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="1c791-166">Найдите комментарий `// TODO: implement SearchUsersList`.</span><span class="sxs-lookup"><span data-stu-id="1c791-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="1c791-167">Этот метод выполняет запрос GET в интерфейс Graph API службы Azure AD для запроса списка пользователей, чьи UPN начинаются с данного слова поиска.</span><span class="sxs-lookup"><span data-stu-id="1c791-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="1c791-168">Для отправки запросов в Graph API необходимо включить access_token в заголовок `Authorization` запроса.</span><span class="sxs-lookup"><span data-stu-id="1c791-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="1c791-169">Вот где может пригодиться ADAL.</span><span class="sxs-lookup"><span data-stu-id="1c791-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="1c791-170">Когда приложение запрашивает маркер путем вызова `getToken(...)`, библиотека ADAL пытается вернуть маркер без запроса учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c791-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="1c791-171">Если ADAL решит, что пользователь должен войти в систему для получения маркера, то служба отобразит диалоговое окно входа, соберет учетные данные пользователя и вернет маркер после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1c791-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="1c791-172">Если библиотеке ADAL не удастся по какой-либо причине вернуть маркер, она вызовет исключение `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="1c791-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="1c791-173">Объект `AuthenticationResult` содержит объект `tokenCacheStoreItem`, который может использоваться для сбора сведений, необходимых приложению.</span><span class="sxs-lookup"><span data-stu-id="1c791-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="1c791-174">В проекте QuickStart объект `tokenCacheStoreItem` используется, чтобы определить, была ли выполнена проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="1c791-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="1c791-175">5. Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="1c791-175">5. Build and run the application</span></span>
<span data-ttu-id="1c791-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="1c791-176">Congratulations!</span></span> <span data-ttu-id="1c791-177">Теперь у нас есть рабочее приложение для iOS, которое может проверять подлинность пользователей, безопасно вызывать методы веб-API по протоколу OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="1c791-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="1c791-178">Если же вы этого еще не сделали, пришло время добавить в клиент нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="1c791-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="1c791-179">Запустите приложение QuickStart и выполните вход как один из пользователей.</span><span class="sxs-lookup"><span data-stu-id="1c791-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="1c791-180">Осуществите поиск других пользователей по их имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c791-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="1c791-181">Закройте приложение и запустите его снова.</span><span class="sxs-lookup"><span data-stu-id="1c791-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="1c791-182">Обратите внимание на то, что пользовательский сеанс остался без изменений.</span><span class="sxs-lookup"><span data-stu-id="1c791-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="1c791-183">Библиотека ADAL упрощает включение в приложение всех этих типичных функций работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="1c791-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="1c791-184">Она отвечает за всю "грязную работу": управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа и обновление истекших маркеров.</span><span class="sxs-lookup"><span data-stu-id="1c791-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="1c791-185">Все, что вам действительно нужно знать, — это вызов интерфейса API `getToken`.</span><span class="sxs-lookup"><span data-stu-id="1c791-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="1c791-186">Для справки следует отметить, что готовый пример (без ваших значений конфигурации) находится на [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1c791-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1c791-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c791-187">Next steps</span></span>
<span data-ttu-id="1c791-188">Теперь можно приступить к изучению других сценариев.</span><span class="sxs-lookup"><span data-stu-id="1c791-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="1c791-189">Можно попробовать:</span><span class="sxs-lookup"><span data-stu-id="1c791-189">You may want to try:</span></span>

* [<span data-ttu-id="1c791-190">Безопасность веб-API с Azure AD для Node.JS</span><span class="sxs-lookup"><span data-stu-id="1c791-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="1c791-191">См. раздел [Включение единого входа в нескольких приложениях iOS с помощью ADAL](active-directory-sso-ios.md).</span><span class="sxs-lookup"><span data-stu-id="1c791-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

