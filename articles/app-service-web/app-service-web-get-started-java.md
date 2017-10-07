---
title: "aaaCreate первый веб-приложения Java в Azure"
description: "Узнайте, как toorun веб-приложений в службе приложений путем развертывания базовое приложение Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="87885-103">Создание первого веб-приложения Java в Azure</span><span class="sxs-lookup"><span data-stu-id="87885-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="87885-104">Hello [веб-приложений](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) функция [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) предоставляет высокую степень масштабируемости, самостоятельно исправления веб-службе размещения.</span><span class="sxs-lookup"><span data-stu-id="87885-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="87885-105">Краткого руководства показано, как toodeploy Java веб-приложения tooApp службы с помощью hello [интегрированной среды разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="87885-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="87885-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="87885-108">Prerequisites</span></span>

<span data-ttu-id="87885-109">toocomplete краткого руководства, установить:</span><span class="sxs-lookup"><span data-stu-id="87885-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="87885-110">Hello свободного [интегрированной среды разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="87885-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="87885-111">В этом кратком руководстве используется Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="87885-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="87885-112">Hello [средств Azure для Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="87885-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="87885-113">Создание динамических веб-проектов в Eclipse</span><span class="sxs-lookup"><span data-stu-id="87885-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="87885-114">В Eclipse щелкните **File** (Файл) > **New** (Создать) > **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="87885-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="87885-115">В hello **динамический веб-проект** диалоговое окно, имя проекта hello **MyFirstJavaOnAzureWebApp**и выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="87885-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Диалоговое окно создания динамического веб-проекта](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="87885-117">Добавление страницы JSP</span><span class="sxs-lookup"><span data-stu-id="87885-117">Add a JSP page</span></span>

<span data-ttu-id="87885-118">Если обозреватель проектов не отображается, разверните его.</span><span class="sxs-lookup"><span data-stu-id="87885-118">If Project Explorer is not displayed, restore it.</span></span>

![Рабочая область Java EE для Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="87885-120">В обозревателе проектов разверните hello **MyFirstJavaOnAzureWebApp** проекта.</span><span class="sxs-lookup"><span data-stu-id="87885-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="87885-121">Щелкните правой кнопкой мыши **WebContent**, а затем щелкните **New** (Создать) > **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="87885-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Меню для нового JSP-файла в обозревателе проектов](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="87885-123">В hello **Создание JSP-файла** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="87885-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="87885-124">Имя файла hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="87885-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="87885-125">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="87885-125">Select **Finish**.</span></span>

  ![Диалоговое окно New JSP File (Создание JSP-файла)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="87885-127">В файле index.jsp hello замените hello `<body></body>` элемент с hello следующая разметка:</span><span class="sxs-lookup"><span data-stu-id="87885-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="87885-128">Сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="87885-129">Публикация приложения tooAzure hello web</span><span class="sxs-lookup"><span data-stu-id="87885-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="87885-130">В обозревателе решений, правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как веб-приложения Azure**.</span><span class="sxs-lookup"><span data-stu-id="87885-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Контекстное меню Publish as Azure Web App (Опубликовать как веб-приложение Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="87885-132">В hello **входа в Azure** диалоговое окно, поддержания hello **Interactive** , а затем установите **входа**.</span><span class="sxs-lookup"><span data-stu-id="87885-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="87885-133">Следуйте инструкциям hello вход.</span><span class="sxs-lookup"><span data-stu-id="87885-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="87885-134">Диалоговое окно развертывания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="87885-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="87885-135">После входа в учетную запись Azure tooyour hello **развертывание веб-приложения** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="87885-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="87885-136">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="87885-136">Select **Create**.</span></span>

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="87885-138">Диалоговое окно "Создание службы приложений"</span><span class="sxs-lookup"><span data-stu-id="87885-138">Create App Service dialog box</span></span>

<span data-ttu-id="87885-139">Hello **Создание приложения службы** откроется диалоговое окно со значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="87885-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="87885-140">Здравствуйте, номер **170602185241** показано в следующих hello изображения отличается диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="87885-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="87885-142">В hello **Создание приложения службы** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="87885-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="87885-143">Оставьте имя hello созданный для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="87885-144">Это имя должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="87885-144">This name must be unique across Azure.</span></span> <span data-ttu-id="87885-145">Имя Hello является частью hello URL-адрес для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="87885-146">Например: Если имя веб-приложения hello **MyJavaWebApp**, URL-адрес является hello *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="87885-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="87885-147">Сохраните контейнер web по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="87885-147">Keep hello default web container.</span></span>
* <span data-ttu-id="87885-148">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="87885-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="87885-149">На hello **план обслуживания приложений** вкладки:</span><span class="sxs-lookup"><span data-stu-id="87885-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="87885-150">**Создать новый**: сохранить по умолчанию hello, которое является именем hello объекта hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="87885-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="87885-151">**Location** (Расположение): Выберите **West Europe** (Западная Европа) или ближайшее расположение.</span><span class="sxs-lookup"><span data-stu-id="87885-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="87885-152">**Ценовая категория**: выберите hello свободного параметр.</span><span class="sxs-lookup"><span data-stu-id="87885-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="87885-153">Сведения о функциях см. на странице [цен на службу приложений](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="87885-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="87885-155">Вкладка Resource group (Группа ресурсов)</span><span class="sxs-lookup"><span data-stu-id="87885-155">Resource group tab</span></span>

<span data-ttu-id="87885-156">Выберите hello **группы ресурсов** вкладки. Оставьте значение по умолчанию создается hello hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="87885-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Вкладка Resource group (Группа ресурсов)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="87885-158">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="87885-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="87885-159">Hello набора средств Azure создает веб-приложение hello и отображает диалоговое окно хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="87885-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Диалоговое окно Create App Service Progress (Прогресс создания службы приложений)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="87885-161">Диалоговое окно развертывания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="87885-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="87885-162">В hello **развертывание веб-приложения** выберите **развертывание tooroot**.</span><span class="sxs-lookup"><span data-stu-id="87885-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="87885-163">Если вы создали службу приложений в *wingtiptoys.azurewebsites.net* и не следует развертывать toohello корень, hello веб-приложения с именем **MyFirstJavaOnAzureWebApp** развертывается слишком *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="87885-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="87885-165">показывает диалоговое окно приветствия hello Azure, JDK и выбора контейнера web.</span><span class="sxs-lookup"><span data-stu-id="87885-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="87885-166">Выберите **развернуть** toopublish hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="87885-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="87885-167">По завершении публикации hello выберите hello **опубликовано** ссылку в hello **журнал действий Azure** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="87885-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Диалоговое окно "Журнал действий Azure"](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="87885-169">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="87885-169">Congratulations!</span></span> <span data-ttu-id="87885-170">Успешно завершены вашей tooAzure web app.</span><span class="sxs-lookup"><span data-stu-id="87885-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="87885-173">Обновить веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="87885-173">Update hello web app</span></span>

<span data-ttu-id="87885-174">Изменение hello образец JSP кода tooa другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="87885-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="87885-175">Сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-175">Save hello changes.</span></span>

<span data-ttu-id="87885-176">В обозревателе решений, правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как веб-приложения Azure**.</span><span class="sxs-lookup"><span data-stu-id="87885-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="87885-177">Hello **развертывание веб-приложения** откроется диалоговое окно и отображает hello службы приложений, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="87885-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="87885-178">Выберите **развертывание tooroot** каждый раз при публикации.</span><span class="sxs-lookup"><span data-stu-id="87885-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="87885-179">Выберите веб-приложение hello и выберите **развернуть**, который публикует изменения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="87885-180">Здравствуйте, когда **публикации** появляется ссылка, выберите его toobrowse toohello веб-приложение и просмотреть изменения hello.</span><span class="sxs-lookup"><span data-stu-id="87885-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="87885-181">Управление веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="87885-181">Manage hello web app</span></span>

<span data-ttu-id="87885-182">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toosee hello веб-приложения, созданный вами.</span><span class="sxs-lookup"><span data-stu-id="87885-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="87885-183">Hello в левом меню, выберите **групп ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="87885-183">From hello left menu, select **Resource Groups**.</span></span>

![Tooresource группы переходов портала](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="87885-185">Выберите группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="87885-185">Select hello resource group.</span></span> <span data-ttu-id="87885-186">Страница приветствия показывает hello ресурсы, созданные в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="87885-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Группа ресурсов myresourcegroup.](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="87885-188">Выберите hello веб-приложения (**170602193915 веб-приложение** в hello предшествующий изображения).</span><span class="sxs-lookup"><span data-stu-id="87885-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="87885-189">Hello **Обзор** появится страница.</span><span class="sxs-lookup"><span data-stu-id="87885-189">hello **Overview** page appears.</span></span> <span data-ttu-id="87885-190">Эта страница позволяет получить представление о том, как это приложение hello.</span><span class="sxs-lookup"><span data-stu-id="87885-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="87885-191">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="87885-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="87885-192">закладки Hello hello левой части страницы приветствия показывают hello различных конфигураций, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="87885-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Страница службы приложений на портале Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="87885-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87885-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87885-195">Сопоставление пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="87885-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
