---
title: "aaaCreate бизнес приложения Azure с проверкой подлинности Azure Active Directory | Документы Microsoft"
description: "Узнайте, как toocreate ASP.NET MVC для бизнес-приложения в службе приложений Azure, выполняющий проверку подлинности в Azure Active Directory"
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
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="61ad6-103">Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ad6-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="61ad6-104">В этой статье показано, как toocreate .NET из бизнес-приложения в [веб-приложениях службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью hello [проверки подлинности и авторизации](../app-service/app-service-authentication-overview.md) компонентов.</span><span class="sxs-lookup"><span data-stu-id="61ad6-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="61ad6-105">Здесь также показано, как toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery данных каталога в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="61ad6-106">Hello клиента Azure Active Directory, которая используется может быть каталогом только в Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="61ad6-107">Или может быть [синхронизированы с вашей локальной Active Directory](../active-directory/active-directory-aadconnect.md) toocreate входа единого для рабочих процессов, для локальных и удаленных.</span><span class="sxs-lookup"><span data-stu-id="61ad6-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="61ad6-108">В этой статье используется каталог по умолчанию hello для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="61ad6-109">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="61ad6-109">What you will build</span></span>
<span data-ttu-id="61ad6-110">Будет создать простое приложение создание-чтение-обновления и удаления (CRUD) бизнес-в веб-приложениях службы приложений, который отслеживает рабочие элементы с hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="61ad6-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="61ad6-111">аутентификация пользователей в службе Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="61ad6-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="61ad6-112">запросы пользователей и групп каталога с помощью [API Graph Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="61ad6-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="61ad6-113">Используйте hello ASP.NET MVC *без проверки подлинности* шаблона</span><span class="sxs-lookup"><span data-stu-id="61ad6-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="61ad6-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Дальнейшее действие](#next).</span><span class="sxs-lookup"><span data-stu-id="61ad6-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="61ad6-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="61ad6-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="61ad6-116">Требуется hello следующие toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="61ad6-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="61ad6-117">Клиент Azure Active Directory с пользователями в различных группах</span><span class="sxs-lookup"><span data-stu-id="61ad6-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="61ad6-118">Разрешения приложений toocreate на приветствия клиента Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ad6-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="61ad6-119">Visual Studio 2013 с обновлением 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="61ad6-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="61ad6-120">Пакет Azure SDK версии 2.8.1 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="61ad6-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="61ad6-121">Создание и развертывание приложения web tooAzure</span><span class="sxs-lookup"><span data-stu-id="61ad6-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="61ad6-122">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="61ad6-123">Выберите **Веб-приложение ASP.NET**, введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="61ad6-124">Выберите hello **MVC** шаблон, затем измените hello проверки подлинности слишком**без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="61ad6-125">Убедитесь, что **узлов в облаке hello** выбран и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="61ad6-126">В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **добавить учетную запись** (а затем **добавить учетную запись** в раскрывающемся списке hello) toolog в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="61ad6-127">После этого перейдите на страницу "Настройка" веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-127">Once logged in configure your web app.</span></span> <span data-ttu-id="61ad6-128">Создать группу ресурсов и новый план служб приложений, щелкнув соответствующий hello **New** кнопки.</span><span class="sxs-lookup"><span data-stu-id="61ad6-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="61ad6-129">Нажмите кнопку **Обзор дополнительных служб Azure** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="61ad6-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="61ad6-130">В hello **службы** щелкните  **+**  tooadd базы данных SQL для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="61ad6-131">В **Настройка базы данных SQL**, нажмите кнопку **New** toocreate экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="61ad6-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="61ad6-132">Настройте экземпляр SQL Server на вкладке **Настроить SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="61ad6-133">Нажмите кнопку **ОК**, **ОК**, и **создать** tookick отключить создание приложения hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="61ad6-134">В **активности службы приложения Azure**, можно увидеть, когда будет завершено создание приложения hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="61ad6-135">Нажмите кнопку  **публикации &lt;* appname*> toothis веб-приложения сейчас **, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="61ad6-136">После завершения выполнения Visual Studio, он открывается hello опубликовать приложение в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="61ad6-137">Настройка проверки подлинности и доступа к каталогу</span><span class="sxs-lookup"><span data-stu-id="61ad6-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="61ad6-138">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61ad6-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61ad6-139">Hello в левом меню, щелкните **службы приложений** > **&lt;*appname*> ** > **проверки подлинности и авторизации**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="61ad6-140">Чтобы включить аутентификацию Azure Active Directory, щелкните **Включено** > **Azure Active Directory** > **Экспресс** > **OК**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="61ad6-141">Нажмите кнопку **Сохранить** hello панели команд.</span><span class="sxs-lookup"><span data-stu-id="61ad6-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="61ad6-142">После сохранения параметров проверки подлинности hello повторите перемещение tooyour приложение еще раз в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="61ad6-143">Параметры по умолчанию обеспечивают проверку подлинности для всего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="61ad6-144">Если вы не выполнили вход, вы несете перенаправленный tooa экран входа.</span><span class="sxs-lookup"><span data-stu-id="61ad6-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="61ad6-145">После входа откроется приложение, защищенное по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="61ad6-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="61ad6-146">Далее необходимо tooenable доступа к данным toodirectory.</span><span class="sxs-lookup"><span data-stu-id="61ad6-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="61ad6-147">Перейдите toohello [классический портал](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="61ad6-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="61ad6-148">Hello в левом меню, щелкните **Active Directory** > **каталог по умолчанию** > **приложений**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="61ad6-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="61ad6-149">Это приложение hello Azure Active Directory, служба приложения создала для вас tooenable hello авторизации и проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="61ad6-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="61ad6-150">Нажмите кнопку **пользователей** и **группы** toomake, что у некоторых пользователей и групп в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="61ad6-151">Если пользователи и группы отсутствуют, создайте несколько тестовых пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="61ad6-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="61ad6-152">Нажмите кнопку **Настройка** tooconfigure этого приложения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="61ad6-153">Прокрутите вниз toohello **ключей** раздел и добавить ключ, выбрав длительность.</span><span class="sxs-lookup"><span data-stu-id="61ad6-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="61ad6-154">Затем щелкните раскрывающийся список **Делегированные разрешения** и выберите разрешение **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="61ad6-155">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="61ad6-156">После сохранения параметров пролистать назад toohello **ключей** и нажмите кнопку hello **копирования** ключ клиента hello toocopy кнопки.</span><span class="sxs-lookup"><span data-stu-id="61ad6-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="61ad6-157">Если покинуть эту страницу сейчас, не будет возможности tooaccess, когда-либо еще раз ключа этого клиента.</span><span class="sxs-lookup"><span data-stu-id="61ad6-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="61ad6-158">Далее необходимо tooconfigure веб-приложения с данным ключом.</span><span class="sxs-lookup"><span data-stu-id="61ad6-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="61ad6-159">Войдите в toohello [обозревателя ресурсов Azure](https://resources.azure.com) с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="61ad6-160">В начале hello страницы приветствия, нажмите кнопку **чтения и записи** toomake изменения в hello обозревателя ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="61ad6-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="61ad6-161">Найти hello параметры проверки подлинности для приложения, расположенный в подписки >  **&lt;* имя_подписки*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **поставщики** > **Microsoft.Web**  >  **сайтов** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="61ad6-162">Нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="61ad6-163">В области редактирования hello, задайте hello `clientSecret` и `additionalLoginParams` свойства следующим образом.</span><span class="sxs-lookup"><span data-stu-id="61ad6-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="61ad6-164">Нажмите кнопку **поместить** на hello top toosubmit изменения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="61ad6-165">Теперь tootest, если у вас имеется разрешение hello маркера hello tooaccess Azure Active Directory Graph API, перейдя в  **https://&lt;*appname*>.azurewebsites.net/.auth/me** в вашей Обозреватель.</span><span class="sxs-lookup"><span data-stu-id="61ad6-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="61ad6-166">Если вы настроили все правильно, вы увидите hello `access_token` свойство в hello ответ JSON.</span><span class="sxs-lookup"><span data-stu-id="61ad6-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="61ad6-167">Hello `~/.auth/me` URL-адрес находится под управлением приложения проверки подлинности службы или toogive авторизации, вы все hello сведения, связанные с проверкой подлинности tooyour сеанса.</span><span class="sxs-lookup"><span data-stu-id="61ad6-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="61ad6-168">Дополнительные сведения см. в статье [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61ad6-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="61ad6-169">Hello `access_token` имеет срок действия.</span><span class="sxs-lookup"><span data-stu-id="61ad6-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="61ad6-170">Тем не менее функция аутентификации и авторизации в службе приложений обеспечивает обновление маркера с использованием `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="61ad6-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="61ad6-171">Дополнительные сведения о том, как toouse, в разделе [маркер службы App Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="61ad6-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="61ad6-172">В следующем разделе описываются действия, выполняемые с данными каталога.</span><span class="sxs-lookup"><span data-stu-id="61ad6-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="61ad6-173">Добавить функциональные возможности бизнес-приложение tooyour</span><span class="sxs-lookup"><span data-stu-id="61ad6-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="61ad6-174">Теперь необходимо создать простое приложения CRUD для отслеживания рабочих элементов.</span><span class="sxs-lookup"><span data-stu-id="61ad6-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="61ad6-175">В папке ~\Models hello, создайте файл класса с именем WorkItem.cs и замените `public class WorkItem {...}` с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="61ad6-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="61ad6-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="61ad6-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="61ad6-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="61ad6-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="61ad6-178">}</span><span class="sxs-lookup"><span data-stu-id="61ad6-178">}</span></span>
   
     <span data-ttu-id="61ad6-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="61ad6-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="61ad6-180">}</span><span class="sxs-lookup"><span data-stu-id="61ad6-180">}</span></span>
2. <span data-ttu-id="61ad6-181">Построение проекта toomake hello новая логика формирование шаблонов модели доступен toohello, в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61ad6-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="61ad6-182">Добавить новый элемент формирования шаблонов `WorkItemsController` toohello ~\Controllers папку (щелкните правой кнопкой мыши **контроллеров**, слишком точки**добавить**и выберите **новый элемент формирования шаблонов**).</span><span class="sxs-lookup"><span data-stu-id="61ad6-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="61ad6-183">Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="61ad6-184">Выберите hello созданной модели, нажмите кнопку  **+**  и затем **добавить** tooadd контекст данных, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="61ad6-185">В ~\Views\WorkItems\Create.cshtml (автоматического формирования шаблонов элемента), найти hello `Html.BeginForm` вспомогательный метод и внесите следующие выделенные изменения hello:</span><span class="sxs-lookup"><span data-stu-id="61ad6-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
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
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="61ad6-186">Обратите внимание, что `token` и `tenant` используются hello `AadPicker` toomake объекта, вызывает Azure Active Directory Graph API.</span><span class="sxs-lookup"><span data-stu-id="61ad6-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="61ad6-187">Объект `AadPicker` добавим позже.</span><span class="sxs-lookup"><span data-stu-id="61ad6-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="61ad6-188">Точно так же можно получить `token` и `tenant` из hello на стороне клиента с `~/.auth/me`, но может быть вызов дополнительного сервера.</span><span class="sxs-lookup"><span data-stu-id="61ad6-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="61ad6-189">Например:</span><span class="sxs-lookup"><span data-stu-id="61ad6-189">For example:</span></span>
   > 
   > <span data-ttu-id="61ad6-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="61ad6-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="61ad6-191">Внести аналогичные изменения с hello ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="61ad6-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="61ad6-192">Hello `AadPicker` объект определен в сценарии необходимые tooadd tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="61ad6-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="61ad6-193">Щелкните правой кнопкой мыши папку ~\Scripts hello, укажите слишком**добавить**и нажмите кнопку **файл JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="61ad6-194">Тип `AadPickerLibrary` hello имя файла и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="61ad6-195">Копировать содержимое hello [здесь](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) в ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="61ad6-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="61ad6-196">В сценарии hello hello `AadPicker` вызывает [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch для пользователей и групп, соответствующих входных данных hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="61ad6-197">~\Scripts\AadPickerLibrary.js также использует hello [мини-приложение автозаполнения пользовательского интерфейса jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="61ad6-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="61ad6-198">Поэтому необходимо tooadd jQuery UI tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="61ad6-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="61ad6-199">Щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="61ad6-200">Hello диспетчера пакетов NuGet, нажмите кнопку Обзор, тип **пользовательского интерфейса jquery** в hello панель поиска и нажмите кнопку **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="61ad6-201">Hello правой панели щелкните **установить**, нажмите кнопку **ОК** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="61ad6-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="61ad6-202">Откройте ~\App_Start\BundleConfig.cs и внесите следующие выделенные изменения hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
    
    <span data-ttu-id="61ad6-203">Существуют дополнительные toomanage способов высокопроизводительных JavaScript и CSS-файлов в приложении.</span><span class="sxs-lookup"><span data-stu-id="61ad6-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="61ad6-204">Однако для простоты мы будем просто toopiggyback на пакеты hello, загруженных в каждом представлении.</span><span class="sxs-lookup"><span data-stu-id="61ad6-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="61ad6-205">Наконец, в ~ \Global.asax, добавить следующие строки кода в hello hello `Application_Start()` метод.</span><span class="sxs-lookup"><span data-stu-id="61ad6-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="61ad6-206">`Ctrl`+`.`на каждое разрешение имен ошибка слишком ее устранению.</span><span class="sxs-lookup"><span data-stu-id="61ad6-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="61ad6-207">Необходимо эту строку кода, так как использует шаблона MVC по умолчанию hello <code>[ValidateAntiForgeryToken]</code> оформления на некоторых действиях hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="61ad6-208">Из-за toohello поведение, описываемого [Аллен Brock](https://twitter.com/BrockLAllen) в [MVC 4, AntiForgeryToken и утверждений](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) вашей HTTP POST возможен сбой проверки маркера защиты от подделки, поскольку:</span><span class="sxs-lookup"><span data-stu-id="61ad6-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="61ad6-209">Azure Active Directory не отправляет http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, требуемой по умолчанию токен борьбы с фальсификацией hello.</span><span class="sxs-lookup"><span data-stu-id="61ad6-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="61ad6-210">Если Azure Active Directory — каталог, синхронизированные с AD FS, hello AD FS доверия по умолчанию не отправляет hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider утверждения, несмотря на то, что можно вручную настроить AD FS toosend Это утверждение.</span><span class="sxs-lookup"><span data-stu-id="61ad6-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="61ad6-211">`ClaimTypes.NameIdentifies`Указывает hello утверждения `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, который поддерживает Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61ad6-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="61ad6-212">Теперь опубликуйте изменения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-212">Now, publish your changes.</span></span> <span data-ttu-id="61ad6-213">Щелкните свой проект правой кнопкой мыши и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="61ad6-214">Нажмите кнопку **параметры**, убедитесь в отсутствии tooyour строку подключения базы данных SQL, выберите **обновление базы данных** toomake hello изменений схемы в модели и нажмите кнопку **публикации** .</span><span class="sxs-lookup"><span data-stu-id="61ad6-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="61ad6-215">В браузере hello перейдите toohttps: / /&lt;*appname*>.azurewebsites.net/workitems и нажмите кнопку **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="61ad6-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="61ad6-216">Нажмите кнопку в hello **AssignedToName** поле.</span><span class="sxs-lookup"><span data-stu-id="61ad6-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="61ad6-217">В раскрывающемся списке должны отобразиться пользователи и группы из клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61ad6-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="61ad6-218">Введите toofilter или использовать hello `Up` или `Down` или щелкните tooselect hello пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="61ad6-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="61ad6-219">Нажмите кнопку **создать** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="61ad6-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="61ad6-220">Нажмите кнопку **изменить** hello создания рабочего элемента tooobserve hello такое же поведение.</span><span class="sxs-lookup"><span data-stu-id="61ad6-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="61ad6-221">Поздравляем, теперь бизнес-приложение с доступом к каталогу запущено в Azure!</span><span class="sxs-lookup"><span data-stu-id="61ad6-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="61ad6-222">Нет hello Graph API гораздо больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="61ad6-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="61ad6-223">Ознакомьтесь со [справочником по API Graph Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="61ad6-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="61ad6-224">Дальнейшее действие</span><span class="sxs-lookup"><span data-stu-id="61ad6-224">Next Step</span></span>
<span data-ttu-id="61ad6-225">Если управление доступом на основе ролей (RBAC) требуется для бизнес-приложения в azure, см. раздел [WebApp RoleClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) образец hello группы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61ad6-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="61ad6-226">Там показано, как tooenable роли для приложения Azure Active Directory и затем авторизовать пользователей с hello `[Authorize]` оформления.</span><span class="sxs-lookup"><span data-stu-id="61ad6-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="61ad6-227">Если бизнес-приложения требуется доступ к данным tooon организациями, см. раздел [доступа к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61ad6-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="61ad6-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="61ad6-228">Further resources</span></span>
* [<span data-ttu-id="61ad6-229">Проверка подлинности и авторизация в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="61ad6-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="61ad6-230">Проверка подлинности в приложении Azure с помощью локального каталога Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ad6-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="61ad6-231">Создание веб-приложения .NET MVC в службе приложений Azure с аутентификацией AD FS</span><span class="sxs-lookup"><span data-stu-id="61ad6-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="61ad6-232">Проверка подлинности службы приложения и hello API Azure AD Graph</span><span class="sxs-lookup"><span data-stu-id="61ad6-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="61ad6-233">Примеры и документация Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ad6-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="61ad6-234">Поддерживаемые типы маркеров и утверждений</span><span class="sxs-lookup"><span data-stu-id="61ad6-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
