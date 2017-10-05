---
title: "Создание первого веб-приложения Java в Azure"
description: "Узнайте, как запускать веб-приложения в службе приложений, развернув базовое приложение Java."
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
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="37de0-103">Создание первого веб-приложения Java в Azure</span><span class="sxs-lookup"><span data-stu-id="37de0-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="37de0-104">[Веб-приложения](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) [службы приложений Azure](../app-service/app-service-value-prop-what-is.md) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="37de0-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="37de0-105">В этом кратком руководстве показано, как развернуть веб-приложение Java в службе приложений с помощью [интегрированной среды разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="37de0-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="37de0-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="37de0-108">Prerequisites</span></span>

<span data-ttu-id="37de0-109">Для работы с этим кратким руководством установите:</span><span class="sxs-lookup"><span data-stu-id="37de0-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="37de0-110">Бесплатную [интегрированную среду разработки Eclipse для разработчиков Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="37de0-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="37de0-111">В этом кратком руководстве используется Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="37de0-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="37de0-112">[Набор средств Azure для Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="37de0-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="37de0-113">Создание динамических веб-проектов в Eclipse</span><span class="sxs-lookup"><span data-stu-id="37de0-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="37de0-114">В Eclipse щелкните **File** (Файл) > **New** (Создать) > **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="37de0-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="37de0-115">В диалоговом окне **New Dynamic Web Project** (Новый динамический веб-проект) присвойте проекту имя **MyFirstJavaOnAzureWebApp** и нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="37de0-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Диалоговое окно создания динамического веб-проекта](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="37de0-117">Добавление страницы JSP</span><span class="sxs-lookup"><span data-stu-id="37de0-117">Add a JSP page</span></span>

<span data-ttu-id="37de0-118">Если обозреватель проектов не отображается, разверните его.</span><span class="sxs-lookup"><span data-stu-id="37de0-118">If Project Explorer is not displayed, restore it.</span></span>

![Рабочая область Java EE для Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="37de0-120">В обозревателе проектов разверните проект **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="37de0-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="37de0-121">Щелкните правой кнопкой мыши **WebContent**, а затем щелкните **New** (Создать) > **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="37de0-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Меню для нового JSP-файла в обозревателе проектов](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="37de0-123">В диалоговом окне **New JSP File** (Создание JSP-файла):</span><span class="sxs-lookup"><span data-stu-id="37de0-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="37de0-124">Назовите файл **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="37de0-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="37de0-125">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="37de0-125">Select **Finish**.</span></span>

  ![Диалоговое окно New JSP File (Создание JSP-файла)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="37de0-127">В файле index.jsp замените элемент `<body></body>` следующей разметкой:</span><span class="sxs-lookup"><span data-stu-id="37de0-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="37de0-128">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="37de0-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="37de0-129">Публикация веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="37de0-129">Publish the web app to Azure</span></span>

<span data-ttu-id="37de0-130">В обозревателе проектов щелкните правой кнопкой мыши проект и выберите **Azure** > **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="37de0-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Контекстное меню Publish as Azure Web App (Опубликовать как веб-приложение Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="37de0-132">В диалоговом окне **Azure Sign In** (Вход в Azure) оставьте параметр **Interactive** (Интерактивный), а затем выберите **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="37de0-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="37de0-133">Следуйте инструкциям по входу.</span><span class="sxs-lookup"><span data-stu-id="37de0-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="37de0-134">Диалоговое окно развертывания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="37de0-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="37de0-135">После входа в учетную запись Azure отобразится диалоговое окно **Deploy Web App** (Развертывание веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="37de0-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="37de0-136">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37de0-136">Select **Create**.</span></span>

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="37de0-138">Диалоговое окно "Создание службы приложений"</span><span class="sxs-lookup"><span data-stu-id="37de0-138">Create App Service dialog box</span></span>

<span data-ttu-id="37de0-139">Откроется диалоговое окно **Create App Service** (Создание службы приложений) со значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37de0-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="37de0-140">Число **170602185241**, показанное на следующем изображении, отличается от числа, которое появится в вашем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="37de0-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="37de0-142">В диалоговом окне **Create App Service** (Создание службы приложений):</span><span class="sxs-lookup"><span data-stu-id="37de0-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="37de0-143">Оставьте созданное имя для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="37de0-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="37de0-144">Это имя должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="37de0-144">This name must be unique across Azure.</span></span> <span data-ttu-id="37de0-145">Имя является частью URL-адреса веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="37de0-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="37de0-146">Например, если имя веб-приложения — **MyJavaWebApp**, то URL-адрес будет *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="37de0-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="37de0-147">Оставьте веб-контейнер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37de0-147">Keep the default web container.</span></span>
* <span data-ttu-id="37de0-148">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="37de0-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="37de0-149">На вкладке **App service plan** (План службы приложений):</span><span class="sxs-lookup"><span data-stu-id="37de0-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="37de0-150">**Create new** (Создать). Оставьте имя по умолчанию, которое является именем плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="37de0-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="37de0-151">**Location** (Расположение): Выберите **West Europe** (Западная Европа) или ближайшее расположение.</span><span class="sxs-lookup"><span data-stu-id="37de0-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="37de0-152">**Pricing tier** (Ценовая категория). Выберите бесплатный вариант.</span><span class="sxs-lookup"><span data-stu-id="37de0-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="37de0-153">Сведения о функциях см. на странице [цен на службу приложений](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="37de0-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Диалоговое окно "Создание службы приложений"](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="37de0-155">Вкладка Resource group (Группа ресурсов)</span><span class="sxs-lookup"><span data-stu-id="37de0-155">Resource group tab</span></span>

<span data-ttu-id="37de0-156">Выберите вкладку **Resource group** (Группа ресурсов). Оставьте значение по умолчанию для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37de0-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Вкладка Resource group (Группа ресурсов)](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="37de0-158">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37de0-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="37de0-159">Набор средств Azure создает веб-приложение и отображает диалоговое окно хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="37de0-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Диалоговое окно Create App Service Progress (Прогресс создания службы приложений)](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="37de0-161">Диалоговое окно развертывания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="37de0-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="37de0-162">В диалоговом окне **Deploy Web App** (Развертывание веб-приложения) установите флажок **Deploy to root** (Развернуть в корень).</span><span class="sxs-lookup"><span data-stu-id="37de0-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="37de0-163">Если у вас есть служба приложений в *wingtiptoys.azurewebsites.net* и вы не выполните развертывание в корневой каталог, тогда веб-приложение **MyFirstJavaOnAzureWebApp** будет развернуто в каталоге *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="37de0-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Диалоговое окно развертывания веб-приложения](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="37de0-165">В диалоговом окне отображаются выбранные значения Azure, JDK и веб-контейнера.</span><span class="sxs-lookup"><span data-stu-id="37de0-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="37de0-166">Нажмите кнопку **Deploy** (Развернуть) для публикации веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="37de0-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="37de0-167">После завершения публикации щелкните ссылку **Опубликовано** в диалоговом окне **Журнал действий Azure**.</span><span class="sxs-lookup"><span data-stu-id="37de0-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Диалоговое окно "Журнал действий Azure"](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="37de0-169">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="37de0-169">Congratulations!</span></span> <span data-ttu-id="37de0-170">Веб-приложение успешно развернуто в Azure.</span><span class="sxs-lookup"><span data-stu-id="37de0-170">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="37de0-173">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="37de0-173">Update the web app</span></span>

<span data-ttu-id="37de0-174">Измените пример кода JSP на другое сообщение.</span><span class="sxs-lookup"><span data-stu-id="37de0-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="37de0-175">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="37de0-175">Save the changes.</span></span>

<span data-ttu-id="37de0-176">В обозревателе проектов щелкните правой кнопкой мыши проект и выберите **Azure** > **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="37de0-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="37de0-177">Появится диалоговое окно **Deploy Web App** (Развертывание веб-приложения) с ранее созданной службой приложений.</span><span class="sxs-lookup"><span data-stu-id="37de0-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="37de0-178">Устанавливайте флажок **Deploy to root** (Развернуть в корень) при каждой публикации.</span><span class="sxs-lookup"><span data-stu-id="37de0-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="37de0-179">Выберите веб-приложение и щелкните **Deploy** (Развернуть) для публикации изменений.</span><span class="sxs-lookup"><span data-stu-id="37de0-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="37de0-180">Когда появится ссылка **Publishing** (Публикация), щелкните ее и перейдите к веб-приложению, чтобы увидеть изменения.</span><span class="sxs-lookup"><span data-stu-id="37de0-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="37de0-181">Управление веб-приложением</span><span class="sxs-lookup"><span data-stu-id="37de0-181">Manage the web app</span></span>

<span data-ttu-id="37de0-182">Перейдите на <a href="https://portal.azure.com" target="_blank">портал Azure</a>, чтобы увидеть созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="37de0-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="37de0-183">В меню слева выберите **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="37de0-183">From the left menu, select **Resource Groups**.</span></span>

![Переход к группе ресурсов](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="37de0-185">Выберите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37de0-185">Select the resource group.</span></span> <span data-ttu-id="37de0-186">На странице отображаются ресурсы, созданные в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="37de0-186">The page shows the resources that you created in this quickstart.</span></span>

![Группа ресурсов myresourcegroup.](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="37de0-188">Выберите веб-приложение (**webapp-170602193915** на предыдущем рисунке).</span><span class="sxs-lookup"><span data-stu-id="37de0-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="37de0-189">Появится страница **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="37de0-189">The **Overview** page appears.</span></span> <span data-ttu-id="37de0-190">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="37de0-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="37de0-191">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="37de0-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="37de0-192">На вкладках в левой части страницы отображаются различные конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="37de0-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Страница службы приложений на портале Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="37de0-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37de0-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="37de0-195">Сопоставление пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="37de0-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
