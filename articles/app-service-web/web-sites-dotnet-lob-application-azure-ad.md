---
title: "Создание бизнес-приложения Azure с аутентификацией Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как создать бизнес-приложение ASP.NET MVC в службе приложений Azure, осуществляющее проверку подлинности с помощью Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="fbea3-103">Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbea3-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="fbea3-104">В этой статье показано, как создать бизнес-приложение .NET на основе [веб-приложения службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с использованием функции [Аутентификация или авторизация](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbea3-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="fbea3-105">Здесь также описано, как использовать [API Graph Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) , чтобы запросить данные каталога в приложении.</span><span class="sxs-lookup"><span data-stu-id="fbea3-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="fbea3-106">Используемый клиент Azure Active Directory может действовать исключительно как каталог Azure</span><span class="sxs-lookup"><span data-stu-id="fbea3-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="fbea3-107">или может быть [синхронизирован с локальной службой Active Directory](../active-directory/active-directory-aadconnect.md), что обеспечит единый вход для локальных и удаленных сотрудников.</span><span class="sxs-lookup"><span data-stu-id="fbea3-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="fbea3-108">В рамках этой статьи используется каталог учетной записи Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fbea3-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="fbea3-109">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="fbea3-109">What you will build</span></span>
<span data-ttu-id="fbea3-110">Вы создадите простое бизнес-приложение по шаблону «создать-прочитать-обновить-удалить» (CRUD) в веб-приложениях службы приложений, которое отслеживает рабочие элементы с помощью следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="fbea3-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="fbea3-111">аутентификация пользователей в службе Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="fbea3-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="fbea3-112">запросы пользователей и групп каталога с помощью [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="fbea3-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="fbea3-113">использование шаблона ASP.NET MVC *без аутентификации* .</span><span class="sxs-lookup"><span data-stu-id="fbea3-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="fbea3-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Дальнейшее действие](#next).</span><span class="sxs-lookup"><span data-stu-id="fbea3-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="fbea3-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="fbea3-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="fbea3-116">Чтобы выполнить инструкции этого учебника, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="fbea3-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="fbea3-117">Клиент Azure Active Directory с пользователями в различных группах</span><span class="sxs-lookup"><span data-stu-id="fbea3-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="fbea3-118">Разрешения на создание приложений в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbea3-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="fbea3-119">Visual Studio 2013 с обновлением 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fbea3-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="fbea3-120">Пакет Azure SDK версии 2.8.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fbea3-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="fbea3-121">Создание и развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="fbea3-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="fbea3-122">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="fbea3-123">Выберите **Веб-приложение ASP.NET**, введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="fbea3-124">Выберите шаблон **MVC** и задайте для аутентификации значение **Нет проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="fbea3-125">Установите флажок **Разместить в облаке** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="fbea3-126">В диалоговом окне **Создать службу приложений** щелкните **Добавить учетную запись** (а затем из раскрывающегося списка выберите **Добавить учетную запись**), чтобы войти в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="fbea3-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="fbea3-127">После этого перейдите на страницу "Настройка" веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="fbea3-127">Once logged in configure your web app.</span></span> <span data-ttu-id="fbea3-128">Нажмите кнопку **Создать** , чтобы создать группу ресурсов и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fbea3-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="fbea3-129">Чтобы продолжить, щелкните **Обзор дополнительных служб Azure** .</span><span class="sxs-lookup"><span data-stu-id="fbea3-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="fbea3-130">Чтобы добавить для приложения базу данных SQL, на вкладке **Службы** щелкните **+**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="fbea3-131">Чтобы создать экземпляр SQL Server, на вкладке **Настроить базу данных SQL** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="fbea3-132">Настройте экземпляр SQL Server на вкладке **Настроить SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="fbea3-133">Затем щелкните **ОК**, **ОК** и **Создать**, чтобы начать создание приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="fbea3-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="fbea3-134">Сведения о завершении создания приложения отображаются на вкладке **Действие службы приложений Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="fbea3-135">Щелкните **Опубликовать &lt;*имя_приложения*> в этом веб-приложении**, а затем — **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="fbea3-136">После завершения Visual Studio откроет опубликованное приложение в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="fbea3-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="fbea3-137">Настройка проверки подлинности и доступа к каталогу</span><span class="sxs-lookup"><span data-stu-id="fbea3-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="fbea3-138">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fbea3-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fbea3-139">В меню слева выберите **Службы приложений** > **&lt;*имя_приложения*>** > **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="fbea3-140">Чтобы включить аутентификацию Azure Active Directory, щелкните **Включено** > **Azure Active Directory** > **Экспресс** > **OК**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="fbea3-141">Щелкните в командной строке **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="fbea3-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="fbea3-142">После сохранения параметров проверки подлинности перейдите к своему приложению в браузере.</span><span class="sxs-lookup"><span data-stu-id="fbea3-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="fbea3-143">В соответствии с параметрами по умолчанию проверка подлинности применяется для всего приложения.</span><span class="sxs-lookup"><span data-stu-id="fbea3-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="fbea3-144">Если вход в систему не выполнен, откроется экран входа.</span><span class="sxs-lookup"><span data-stu-id="fbea3-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="fbea3-145">После входа откроется приложение, защищенное по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fbea3-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="fbea3-146">Далее необходимо включить доступ к данным каталога.</span><span class="sxs-lookup"><span data-stu-id="fbea3-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="fbea3-147">Перейдите на [классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fbea3-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="fbea3-148">В меню слева выберите **Active Directory** > **Каталог по умолчанию** > **Приложения** > **&lt;*имя_приложения*>**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="fbea3-149">Это приложение Azure Active Directory, созданное службой приложений для включения функции "Аутентификация или авторизация".</span><span class="sxs-lookup"><span data-stu-id="fbea3-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="fbea3-150">Чтобы проверить наличие пользователей и групп в каталоге, щелкните **Пользователи** и **Группы**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="fbea3-151">Если пользователи и группы отсутствуют, создайте несколько тестовых пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="fbea3-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="fbea3-152">Щелкните **Настройка** , чтобы настроить это приложение.</span><span class="sxs-lookup"><span data-stu-id="fbea3-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="fbea3-153">Прокрутите вниз до раздела **Ключи** и добавьте ключ, выбрав срок его действия.</span><span class="sxs-lookup"><span data-stu-id="fbea3-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="fbea3-154">Затем щелкните раскрывающийся список **Делегированные разрешения** и выберите разрешение **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="fbea3-155">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="fbea3-156">После сохранения параметров прокрутите вверх до раздела **Ключи** и нажмите кнопку **копирования**, чтобы скопировать клиентский ключ.</span><span class="sxs-lookup"><span data-stu-id="fbea3-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="fbea3-157">Если покинуть эту страницу сейчас, вы больше никогда не сможете получить доступ к этому клиентскому ключу.</span><span class="sxs-lookup"><span data-stu-id="fbea3-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="fbea3-158">Теперь необходимо настроить веб-приложение с этим ключом.</span><span class="sxs-lookup"><span data-stu-id="fbea3-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="fbea3-159">Войдите в [обозреватель ресурсов Azure](https://resources.azure.com) , используя учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="fbea3-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="fbea3-160">В верхней части страницы щелкните **Чтение и запись** , чтобы внести изменения в обозревателе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fbea3-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="fbea3-161">Перейдите к параметрам аутентификации приложения: "Подписки" > **&lt;*имя_подписки*>** > **resourceGroups** > **&lt;*имя_группы_ресурсов*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*имя_приложения*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="fbea3-162">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="fbea3-163">В области редактирования задайте свойство `clientSecret` и `additionalLoginParams`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fbea3-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="fbea3-164">Чтобы отправить изменения, в верхней части страницы нажмите кнопку **Поместить** .</span><span class="sxs-lookup"><span data-stu-id="fbea3-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="fbea3-165">Теперь, чтобы проверить наличие маркера авторизации для доступа к API Graph Azure Active Directory, просто перейдите в браузере по адресу **https://&lt;*имя_приложения*>.azurewebsites.net/.auth/me**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="fbea3-166">Если вы настроили все правильно, вы увидите свойство `access_token` в ответе JSON.</span><span class="sxs-lookup"><span data-stu-id="fbea3-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="fbea3-167">Путь URL-адреса `~/.auth/me` управляется функцией проверки подлинности и авторизации в службе приложений, благодаря чему вы можете получать сведения о сеансе с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="fbea3-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="fbea3-168">Дополнительные сведения см. в статье [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbea3-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fbea3-169">`access_token` имеет срок действия.</span><span class="sxs-lookup"><span data-stu-id="fbea3-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="fbea3-170">Тем не менее функция аутентификации и авторизации в службе приложений обеспечивает обновление маркера с использованием `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="fbea3-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="fbea3-171">Чтобы узнать больше об использовании этой функции, ознакомьтесь с [хранилищем маркеров службы приложений](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="fbea3-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="fbea3-172">В следующем разделе описываются действия, выполняемые с данными каталога.</span><span class="sxs-lookup"><span data-stu-id="fbea3-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="fbea3-173">Добавление функциональности бизнес-приложения к приложению</span><span class="sxs-lookup"><span data-stu-id="fbea3-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="fbea3-174">Теперь необходимо создать простое приложения CRUD для отслеживания рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="fbea3-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="fbea3-175">В папке ~\Models создайте файл класса с именем WorkItem.cs и замените `public class WorkItem {...}` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="fbea3-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="fbea3-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="fbea3-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="fbea3-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="fbea3-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="fbea3-178">}</span><span class="sxs-lookup"><span data-stu-id="fbea3-178">}</span></span>
   
     <span data-ttu-id="fbea3-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="fbea3-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="fbea3-180">}</span><span class="sxs-lookup"><span data-stu-id="fbea3-180">}</span></span>
2. <span data-ttu-id="fbea3-181">Постройте проект, чтобы сделать новую модель доступной для логики формирования шаблона в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fbea3-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="fbea3-182">Добавьте новый шаблонный элемент `WorkItemsController` в папку ~\Controllers (щелкните правой кнопкой мыши **Контроллеры**, выберите **Добавить**, а затем — **Создать шаблонный элемент**).</span><span class="sxs-lookup"><span data-stu-id="fbea3-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="fbea3-183">Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="fbea3-184">Выберите созданную модель, щелкните **+** и **Добавить**, чтобы добавить контекст данных, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="fbea3-185">В файле ~\Views\WorkItems\Create.cshtml (автоматически сформированный на основе шаблона элемент) найдите вспомогательный метод `Html.BeginForm` и добавьте следующие выделенные строки.</span><span class="sxs-lookup"><span data-stu-id="fbea3-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="fbea3-186">Обратите внимание, что `token` и `tenant` используются объектом `AadPicker` при вызовах API Graph Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbea3-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="fbea3-187">Объект `AadPicker` добавим позже.</span><span class="sxs-lookup"><span data-stu-id="fbea3-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="fbea3-188">Точно так же `token` и `tenant` можно получить с помощью `~/.auth/me` на стороне клиента, но это будет дополнительный вызов сервера.</span><span class="sxs-lookup"><span data-stu-id="fbea3-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="fbea3-189">Например:</span><span class="sxs-lookup"><span data-stu-id="fbea3-189">For example:</span></span>
   > 
   > <span data-ttu-id="fbea3-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="fbea3-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="fbea3-191">Внесите аналогичные изменения в файл ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="fbea3-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="fbea3-192">Объект `AadPicker` определяется в сценарии, который необходимо добавить в проект.</span><span class="sxs-lookup"><span data-stu-id="fbea3-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="fbea3-193">Щелкните папку ~\Scripts правой кнопкой мыши, выберите **Добавить**, а затем щелкните **Файл JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="fbea3-194">Ведите для имени файла значение `AadPickerLibrary` и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="fbea3-195">Скопируйте содержимое [отсюда](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) и вставьте его в файл ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="fbea3-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="fbea3-196">В сценарии объект `AadPicker` вызывает [API Graph Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) для поиска пользователей и групп, которые соответствуют введенным данным.</span><span class="sxs-lookup"><span data-stu-id="fbea3-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="fbea3-197">В файле ~\Scripts\AadPickerLibrary.js также используется [мини-приложение автозаполнения пользовательского интерфейса jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="fbea3-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="fbea3-198">Поэтому в проект необходимо добавить пользовательский интерфейс jQuery.</span><span class="sxs-lookup"><span data-stu-id="fbea3-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="fbea3-199">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="fbea3-200">В диспетчере пакетов NuGet щелкните "Обзор", введите в строке поиска **jquery-ui** и выберите **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="fbea3-201">В области справа щелкните **Установить** и нажмите кнопку **ОК**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="fbea3-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="fbea3-202">Откройте файл ~\App_Start\BundleConfig.cs и добавьте следующие выделенные строки.</span><span class="sxs-lookup"><span data-stu-id="fbea3-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="fbea3-203">Существуют и более производительные способы управления файлами CSS и JavaScript в приложении.</span><span class="sxs-lookup"><span data-stu-id="fbea3-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="fbea3-204">Однако для простоты используйте пакеты, предоставленные с каждым представлением.</span><span class="sxs-lookup"><span data-stu-id="fbea3-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="fbea3-205">И, наконец, в файле ~\Global.asax добавьте следующую строку кода в метод `Application_Start()`. Чтобы исправить все ошибки, связанные с разрешением имен, щелкните каждую ошибку и нажмите клавиши</span><span class="sxs-lookup"><span data-stu-id="fbea3-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="fbea3-206">`Ctrl`+`.` .</span><span class="sxs-lookup"><span data-stu-id="fbea3-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="fbea3-207">Вам нужна эта строка кода, так как шаблон MVC по умолчанию использует в некоторых действиях декорирование <code>[ValidateAntiForgeryToken]</code>.</span><span class="sxs-lookup"><span data-stu-id="fbea3-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="fbea3-208">Из-за поведения, описанного [Алленом Броком (Brock Allen)](https://twitter.com/BrockLAllen) в статье [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) (MVC 4, маркер защиты от подделки и утверждения), команда HTTP POST может завершиться ошибкой при проверке маркеров защиты от подделки по следующей причине:</span><span class="sxs-lookup"><span data-stu-id="fbea3-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="fbea3-209">Azure Active Directory не отправляет http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, что требуется по умолчанию для маркера защиты от подделки.</span><span class="sxs-lookup"><span data-stu-id="fbea3-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="fbea3-210">Если Azure Active Directory является каталогом, синхронизированным с AD FS, то средство доверия AD FS по умолчанию также не отправляет утверждение http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, хотя можно настроить вручную AD FS для отправки такого утверждения.</span><span class="sxs-lookup"><span data-stu-id="fbea3-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="fbea3-211">`ClaimTypes.NameIdentifies` определяет утверждение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, которое служба Azure Active Directory не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="fbea3-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="fbea3-212">Теперь опубликуйте изменения.</span><span class="sxs-lookup"><span data-stu-id="fbea3-212">Now, publish your changes.</span></span> <span data-ttu-id="fbea3-213">Щелкните свой проект правой кнопкой мыши и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="fbea3-214">Щелкните **Параметры**, убедитесь в наличии строки подключения к базе данных SQL, выберите **Обновить базу данных**, чтобы внести изменения в схему модели, и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="fbea3-215">В браузере перейдите на страницу https://&lt;*имя_приложения*>.azurewebsites.net/workitemss и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fbea3-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="fbea3-216">Щелкните поле **AssignedToName** .</span><span class="sxs-lookup"><span data-stu-id="fbea3-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="fbea3-217">В раскрывающемся списке должны отобразиться пользователи и группы из клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbea3-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="fbea3-218">Задайте условия фильтрации или используйте клавиши `Up` и `Down`, чтобы выбрать пользователя или группу.</span><span class="sxs-lookup"><span data-stu-id="fbea3-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="fbea3-219">Нажмите кнопку **Создать** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="fbea3-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="fbea3-220">Затем в созданном рабочем элементе щелкните **Изменить** , и вы сможете наблюдать за таким же поведением.</span><span class="sxs-lookup"><span data-stu-id="fbea3-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="fbea3-221">Поздравляем, теперь бизнес-приложение с доступом к каталогу запущено в Azure!</span><span class="sxs-lookup"><span data-stu-id="fbea3-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="fbea3-222">API Graph предлагает гораздо больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="fbea3-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="fbea3-223">Ознакомьтесь со [справочником по API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="fbea3-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="fbea3-224">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="fbea3-224">Next Step</span></span>
<span data-ttu-id="fbea3-225">Чтобы создать бизнес-приложение Azure с поддержкой управления доступом на основе ролей (RBAC), воспользуйтесь [образцом WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) , предоставленным рабочей группой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fbea3-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="fbea3-226">В нем показано, как включить роли для приложения Azure Active Directory, а затем авторизовать пользователей с оформлением `[Authorize]` .</span><span class="sxs-lookup"><span data-stu-id="fbea3-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="fbea3-227">Чтобы предоставить бизнес-приложению доступ к локальным данным, изучите статью [Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fbea3-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="fbea3-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fbea3-228">Further resources</span></span>
* [<span data-ttu-id="fbea3-229">Проверка подлинности и авторизация в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="fbea3-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="fbea3-230">Проверка подлинности в приложении Azure с помощью локального каталога Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbea3-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="fbea3-231">Создание веб-приложения .NET MVC в службе приложений Azure с аутентификацией AD FS</span><span class="sxs-lookup"><span data-stu-id="fbea3-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="fbea3-232">App Service Auth and the Azure AD Graph API (Проверка подлинности службы приложений и API Graph Azure AD)</span><span class="sxs-lookup"><span data-stu-id="fbea3-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="fbea3-233">Примеры и документация Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbea3-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="fbea3-234">Поддерживаемые типы маркеров и утверждений</span><span class="sxs-lookup"><span data-stu-id="fbea3-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
