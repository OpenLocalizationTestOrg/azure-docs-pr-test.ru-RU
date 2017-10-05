---
title: "Проверка подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия — настройка вручную"
description: "Описание ручной настройки проверки подлинности для REST API Служб мобильного взаимодействия"
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
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="e58c8-103">Проверка подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия — настройка вручную</span><span class="sxs-lookup"><span data-stu-id="e58c8-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="e58c8-104">Это приложение к статье [Проверка подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e58c8-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="e58c8-105">Сначала следует ознакомиться с данными в статье.</span><span class="sxs-lookup"><span data-stu-id="e58c8-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="e58c8-106">Здесь описывается альтернативный способ выполнения однократной настройки для настройки проверки подлинности с помощью интерфейсов REST API Служб мобильного взаимодействия на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e58c8-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="e58c8-107">Приведенные ниже инструкции основаны на этом [руководстве по Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md). Они настроены в соответствии с требованиями к проверке подлинности с помощью API Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="e58c8-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="e58c8-108">Ознакомьтесь с этим руководством, если хотите получить более подобные сведения о выполняемых действиях.</span><span class="sxs-lookup"><span data-stu-id="e58c8-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="e58c8-109">Войдите в свою учетную запись Azure через [классическую версию портала](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e58c8-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e58c8-110">Выберите **Active Directory** на левой панели.</span><span class="sxs-lookup"><span data-stu-id="e58c8-110">Select **Active Directory** from the left pane.</span></span>
   
     ![выбор Active Directory][1]
3. <span data-ttu-id="e58c8-112">На портале Azure выберите **Active Directory по умолчанию** .</span><span class="sxs-lookup"><span data-stu-id="e58c8-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![выбор каталога][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="e58c8-114">Этот подход работает только в том случае, если вы используете службу Active Directory по умолчанию вашей учетной записи. Он не будет работать, если вы выполняете действия в службе Active Directory, созданной в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e58c8-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="e58c8-115">Чтобы просмотреть приложения в каталоге, щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![просмотр приложений][3]
5. <span data-ttu-id="e58c8-117">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-117">Click on **ADD**.</span></span> 
   
     ![добавление приложения][4]
6. <span data-ttu-id="e58c8-119">Нажмите кнопку **Добавить приложение, которое разрабатывает моя организация**</span><span class="sxs-lookup"><span data-stu-id="e58c8-119">Click on **Add an application my organization is developing**</span></span>
   
     ![новое приложение][5]
7. <span data-ttu-id="e58c8-121">Введите имя приложения и в качестве типа приложения выберите **Веб-приложение и (или) веб-API** .</span><span class="sxs-lookup"><span data-stu-id="e58c8-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![указание имени приложения][6]
8. <span data-ttu-id="e58c8-123">В полях **URL-адрес входа** и **URI кода приложения** можно указать любые фиктивные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="e58c8-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="e58c8-124">Они не используются в этом сценарии и не проверяются.</span><span class="sxs-lookup"><span data-stu-id="e58c8-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![свойства приложения][7]
9. <span data-ttu-id="e58c8-126">В результате вы получите приложение AAD с указанным ранее именем.</span><span class="sxs-lookup"><span data-stu-id="e58c8-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="e58c8-127">Это имя **AD\_APP\_NAME**. Запомните его.</span><span class="sxs-lookup"><span data-stu-id="e58c8-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![имя приложения][8]
10. <span data-ttu-id="e58c8-129">Щелкните имя приложения и выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-129">Click on the app name and click on **Configure**.</span></span>
    
      ![настройка приложения][9]
11. <span data-ttu-id="e58c8-131">Запишите значение в поле "Идентификатор клиента", которое будет использоваться в качестве **CLIENT\_ID** для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="e58c8-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![настройка приложения][10]
12. <span data-ttu-id="e58c8-133">Прокрутите вниз до раздела **Ключи** и добавьте ключ с предпочтительной длительностью 2 года (срок действия), а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![настройка приложения][11]
13. <span data-ttu-id="e58c8-135">Сразу же скопируйте значение, которое отображается для ключа, так как оно доступно только в этот момент и не сохраняется.</span><span class="sxs-lookup"><span data-stu-id="e58c8-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="e58c8-136">Если вы потеряете его, потребуется создать новый ключ.</span><span class="sxs-lookup"><span data-stu-id="e58c8-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="e58c8-137">Это будет значение **client_secret** для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="e58c8-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![настройка приложения][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="e58c8-139">Срок действия ключа завершится при наступлении указанного времени, поэтому в нужный момент продлите срок действия, иначе проверка подлинности API больше не будет работать.</span><span class="sxs-lookup"><span data-stu-id="e58c8-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="e58c8-140">Если вам кажется, что ключ был скомпрометирован, удалите его и создайте заново.</span><span class="sxs-lookup"><span data-stu-id="e58c8-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="e58c8-141">Нажмите кнопку **Просмотр конечных точек**, после чего откроется диалоговое окно **Конечные точки приложения**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="e58c8-142">В этом диалоговом окне скопируйте значение в поле **КОНЕЧНАЯ ТОЧКА МАРКЕРА OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="e58c8-143">Эта конечная точка будет иметь следующий вид, где GUID в URL-адресе — это значение **tenant_id**, поэтому запишите его:</span><span class="sxs-lookup"><span data-stu-id="e58c8-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="e58c8-144">Перейдем к настройке разрешений для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e58c8-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="e58c8-145">Для этого необходимо открыть [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e58c8-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="e58c8-146">Щелкните **Группы ресурсов** и найдите группу **Службы мобильного взаимодействия**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="e58c8-147">Щелкните группу ресурсов **Службы мобильного взаимодействия** и перейдите к колонке **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="e58c8-148">В колонке "Параметры" щелкните **Пользователи**, а затем нажмите кнопку **Добавить**, чтобы добавить пользователя.</span><span class="sxs-lookup"><span data-stu-id="e58c8-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="e58c8-149">Нажмите кнопку **Выбрать роль**</span><span class="sxs-lookup"><span data-stu-id="e58c8-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="e58c8-150">Нажмите кнопку **Владелец**</span><span class="sxs-lookup"><span data-stu-id="e58c8-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="e58c8-151">В поле поиска найдите имя приложения в формате **AD\_APP\_NAME**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="e58c8-152">Здесь оно не отображается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e58c8-152">You will not see this by default here.</span></span> <span data-ttu-id="e58c8-153">Найдя имя, выберите его и щелкните **Выбрать** в нижней части колонки.</span><span class="sxs-lookup"><span data-stu-id="e58c8-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="e58c8-154">В колонке **Добавление доступа** будет отображаться **1 пользователь, 0 групп**.</span><span class="sxs-lookup"><span data-stu-id="e58c8-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="e58c8-155">В этой колонке нажмите кнопку **ОК** , чтобы подтвердить изменение.</span><span class="sxs-lookup"><span data-stu-id="e58c8-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="e58c8-156">Обязательная конфигурация AAD завершена, и все готово для вызова API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e58c8-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

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



