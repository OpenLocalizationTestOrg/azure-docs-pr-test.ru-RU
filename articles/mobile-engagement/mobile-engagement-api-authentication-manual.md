---
title: "aaaAuthenticate с Mobile Engagement API-интерфейс REST - Ручная настройка"
description: "Описывает, как настроить проверку подлинности для API-интерфейс REST Mobile Engagement в toomanually"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="12f9f-103">Проверка подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия — настройка вручную</span><span class="sxs-lookup"><span data-stu-id="12f9f-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="12f9f-104">Это приложение документации слишком[аутентификация с помощью API-интерфейсов REST Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="12f9f-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="12f9f-105">Убедитесь, что вы прочитали первый контекст tooget hello.</span><span class="sxs-lookup"><span data-stu-id="12f9f-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="12f9f-106">Описывает способ toodo hello однократно для настройки проверки подлинности для hello с помощью API-интерфейсов REST Mobile Engagement hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="12f9f-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="12f9f-107">Приведенные ниже инструкции Hello основаны на этой [руководство по Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) и настраивать для требования проверки подлинности для API-интерфейсов Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="12f9f-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="12f9f-108">Поэтому tooit см. Если требуется, чтобы toounderstand hello описанные ниже шаги подробно.</span><span class="sxs-lookup"><span data-stu-id="12f9f-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="12f9f-109">Tooyour входа учетной записи Azure через hello [классический портал](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="12f9f-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="12f9f-110">Выберите **Active Directory** hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="12f9f-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![выбор Active Directory][1]
3. <span data-ttu-id="12f9f-112">Выберите hello **по умолчанию Active Directory** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="12f9f-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![выбор каталога][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="12f9f-114">Такой подход работает только в том случае, если вы работаете в Active Directory учетной записи по умолчанию hello и не будет работать, если вы выполняете это в Active Directory, созданной в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="12f9f-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="12f9f-115">Щелкните tooview hello приложений в каталоге, **приложений**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![просмотр приложений][3]
5. <span data-ttu-id="12f9f-117">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-117">Click on **ADD**.</span></span> 
   
     ![добавление приложения][4]
6. <span data-ttu-id="12f9f-119">Нажмите кнопку **Добавить приложение, которое разрабатывает моя организация**</span><span class="sxs-lookup"><span data-stu-id="12f9f-119">Click on **Add an application my organization is developing**</span></span>
   
     ![новое приложение][5]
7. <span data-ttu-id="12f9f-121">Введите имя приложения hello и выберите hello типа приложения как **веб-приложение и/или WEB API** и нажмите кнопку Далее hello.</span><span class="sxs-lookup"><span data-stu-id="12f9f-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![указание имени приложения][6]
8. <span data-ttu-id="12f9f-123">В полях **URL-адрес входа** и **URI кода приложения** можно указать любые фиктивные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="12f9f-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="12f9f-124">Они не используются в нашем сценарии и URL-адреса hello сами не проверяются.</span><span class="sxs-lookup"><span data-stu-id="12f9f-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![свойства приложения][7]
9. <span data-ttu-id="12f9f-126">В конце этого hello имеется приложение AAD с именем hello, указанным ранее hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="12f9f-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="12f9f-127">Это имя **AD\_APP\_NAME**. Запомните его.</span><span class="sxs-lookup"><span data-stu-id="12f9f-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![имя приложения][8]
10. <span data-ttu-id="12f9f-129">Щелкните имя приложения hello, нажмите кнопку на **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![настройка приложения][9]
11. <span data-ttu-id="12f9f-131">Запишите идентификатор КЛИЕНТА, который будет использоваться в качестве hello **КЛИЕНТА\_идентификатор** API вызывает.</span><span class="sxs-lookup"><span data-stu-id="12f9f-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![настройка приложения][10]
12. <span data-ttu-id="12f9f-133">Прокрутите вниз toohello **ключей** и добавьте раздел длительностью предпочтительно 2 года (срок действия) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![настройка приложения][11]
13. <span data-ttu-id="12f9f-135">Немедленно скопируйте hello значение, которое отображается для ключа hello, как он доступен только теперь и не сохраняются, поэтому не будет отображаться в дальнейшем, когда-либо.</span><span class="sxs-lookup"><span data-stu-id="12f9f-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="12f9f-136">При утере, она будет создана toogenerate новый ключ.</span><span class="sxs-lookup"><span data-stu-id="12f9f-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="12f9f-137">Это будет hello **CLIENT_SECRET** API вызывает.</span><span class="sxs-lookup"><span data-stu-id="12f9f-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![настройка приложения][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="12f9f-139">Этот ключ истекает в конце hello длительность hello, поэтому убедитесь, что toorenew, когда наступает время hello в противном случае API проверки подлинности работать не будет больше заданной.</span><span class="sxs-lookup"><span data-stu-id="12f9f-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="12f9f-140">Если вам кажется, что ключ был скомпрометирован, удалите его и создайте заново.</span><span class="sxs-lookup"><span data-stu-id="12f9f-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="12f9f-141">Щелкните **Просмотр конечных ТОЧЕК** кнопки теперь которого будет открыть hello **конечные точки приложения** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="12f9f-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="12f9f-142">Из диалогового окна конечные точки приложения hello, скопируйте hello **конечная точка МАРКЕРА OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="12f9f-143">Эта конечная точка будет находиться в следующие формы, где hello GUID в URL-АДРЕСЕ hello hello вашей **TENANT_ID** поэтому запомните или запишите его:</span><span class="sxs-lookup"><span data-stu-id="12f9f-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="12f9f-144">Теперь мы продолжится tooconfigure hello разрешения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="12f9f-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="12f9f-145">Для этого необходимо будет tooopen копирование hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12f9f-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="12f9f-146">Щелкните **групп ресурсов** и найти hello **мобильного охвата** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="12f9f-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="12f9f-147">Щелкните hello **Mobile Engagement** ресурсов группы и перейдите toohello **параметры** здесь колонку.</span><span class="sxs-lookup"><span data-stu-id="12f9f-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="12f9f-148">Щелкните **пользователей** в hello колонку параметров и выберите команду **добавить** tooadd пользователя.</span><span class="sxs-lookup"><span data-stu-id="12f9f-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="12f9f-149">Нажмите кнопку **Выбрать роль**</span><span class="sxs-lookup"><span data-stu-id="12f9f-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="12f9f-150">Нажмите кнопку **Владелец**</span><span class="sxs-lookup"><span data-stu-id="12f9f-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="12f9f-151">Найдите имя своего приложения hello **AD\_приложения\_имя** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="12f9f-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="12f9f-152">Здесь оно не отображается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="12f9f-152">You will not see this by default here.</span></span> <span data-ttu-id="12f9f-153">После обнаружения, выберите его и щелкните **выберите** hello нижней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="12f9f-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="12f9f-154">На hello **Добавление доступа к** колонки, он будет отображаться как **1 пользователь, 0 групп**.</span><span class="sxs-lookup"><span data-stu-id="12f9f-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="12f9f-155">Нажмите кнопку **ОК** об этом изменении hello tooconfirm колонку.</span><span class="sxs-lookup"><span data-stu-id="12f9f-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="12f9f-156">Hello необходимые конфигурации AAD успешно завершена, и являются все hello toocall набор API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="12f9f-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



