---
title: "aaaCreate basic Azure веб-приложения с помощью Eclipse | Документы Microsoft"
description: "Этот учебник показывает, как toouse hello набора средств Azure для Eclipse toocreate веб-приложения Hello World для Azure."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="d89e3-103">Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="d89e3-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="d89e3-104">В этом учебнике показано как toocreate и развертывание основных tooAzure приложения Hello World как веб-приложения с помощью hello [средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="d89e3-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="d89e3-105">Для простоты мы приводим базовый пример на JSP, но схожие действия подойдут и для сервлета Java, если речь идет о развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="d89e3-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="d89e3-106">После завершения этого учебника, приложение будет выглядеть аналогично toohello при просмотре в веб-браузере следующие иллюстрации:</span><span class="sxs-lookup"><span data-stu-id="d89e3-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][01]

## <a name="prerequisites"></a><span data-ttu-id="d89e3-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d89e3-108">Prerequisites</span></span>
* <span data-ttu-id="d89e3-109">Пакет SDK для Java (JDK) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d89e3-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="d89e3-110">Интегрированная среда разработки Eclipse для разработчиков Java EE, версия Luna или более поздняя.</span><span class="sxs-lookup"><span data-stu-id="d89e3-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="d89e3-111">Скачать ее можно на веб-странице <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="d89e3-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="d89e3-112">Дистрибутив веб-сервера или сервера приложений на основе Java, например [Apache Tomcat] или [Jetty].</span><span class="sxs-lookup"><span data-stu-id="d89e3-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="d89e3-113">Подписка на Azure, которую можно получить, перейдя по ссылке <https://azure.microsoft.com/free/> или <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="d89e3-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="d89e3-114">Hello [средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="d89e3-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="d89e3-115">Сведения об установке средств Azure hello см. в разделе [hello Установка средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="d89e3-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="d89e3-116">toocreate приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="d89e3-116">toocreate a Hello World application</span></span>
<span data-ttu-id="d89e3-117">Сначала необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="d89e3-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="d89e3-118">Запустите Eclipse и hello меню пункт **файл**, нажмите кнопку **New**и нажмите кнопку **динамический веб-проект**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="d89e3-119">(Если вы не видите **динамический веб-проект** после нажатия кнопки в списке доступных проектов **файл** и **New**, затем hello следующие: щелкните **файл**, нажмите кнопку **New**, нажмите кнопку **проекта...** , разверните **Web**, нажмите кнопку **динамический веб-проект**и нажмите кнопку **Далее**.)</span><span class="sxs-lookup"><span data-stu-id="d89e3-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="d89e3-120">В целях этого учебника назовите проект hello **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="d89e3-121">На экране появится примерно следующее toohello:</span><span class="sxs-lookup"><span data-stu-id="d89e3-121">Your screen will appear similar toohello following:</span></span>
   
    ![Создание динамического веб-проекта][02]
3. <span data-ttu-id="d89e3-123">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="d89e3-123">Click **Finish**.</span></span>
4. <span data-ttu-id="d89e3-124">В представлении обозревателя проектов в Eclipse разверните узел **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="d89e3-125">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="d89e3-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="d89e3-126">В hello **Создание JSP-файла** диалоговое окно, имя файла hello **index.jsp**, сохранить hello родительскую папку как **MyWebApp/WebContent**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="d89e3-127">В hello **Выбор шаблона JSP** диалоговом для целей этого учебника выберите **новый JSP-файл (html)**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="d89e3-128">При открытии файла index.jsp в Eclipse добавьте в виде текста toodynamically **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="d89e3-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="d89e3-129">в существующих hello `<body>` элемента.</span><span class="sxs-lookup"><span data-stu-id="d89e3-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="d89e3-130">Обновленный `<body>` содержимого должен быть похож на следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="d89e3-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="d89e3-131">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="d89e3-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="d89e3-132">toodeploy tooan вашего приложения Azure Web приложения контейнера</span><span class="sxs-lookup"><span data-stu-id="d89e3-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="d89e3-133">Существует несколько способов, с помощью которых можно развернуть tooAzure приложения Java web.</span><span class="sxs-lookup"><span data-stu-id="d89e3-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="d89e3-134">В данном учебнике один простой hello: приложение будет tooan развернутого приложения контейнера Azure веб - нет типа конкретного проекта, ни дополнительные средства необходимы.</span><span class="sxs-lookup"><span data-stu-id="d89e3-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="d89e3-135">Hello JDK и hello web контейнера программного обеспечения будут предоставляться автоматически Azure, поэтому нет необходимости tooupload собственные; все, что необходимо — веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="d89e3-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="d89e3-136">В результате hello процесс публикации для приложения может занять секунд, не минут.</span><span class="sxs-lookup"><span data-stu-id="d89e3-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="d89e3-137">В обозревателе проектов Eclipse щелкните правой кнопкой мыши **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="d89e3-138">Выберите в контекстном меню hello, **Azure**, нажмите кнопку **опубликовать как веб-приложения Azure...**</span><span class="sxs-lookup"><span data-stu-id="d89e3-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Опубликовать как веб-приложение Azure][03]
   
    <span data-ttu-id="d89e3-140">Кроме того, в обозревателе проектов hello выбран проекта веб-приложения, можно нажать кнопку hello **публикации** кнопку раскрывающегося списка на hello и отметьте **опубликовать как веб-приложения Azure** из него:</span><span class="sxs-lookup"><span data-stu-id="d89e3-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Опубликовать как веб-приложение Azure][14]
3. <span data-ttu-id="d89e3-142">Если вы еще не выполнили в Azure из Eclipse, запрашиваемые toosign будет в свою учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="d89e3-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Диалоговое окно входа в Azure][04]
   
    <span data-ttu-id="d89e3-144">При наличии нескольких учетных записей Azure некоторые запросы hello во время hello входа в процесс, могут отображаться несколько раз, даже если они отображаются toobe же hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="d89e3-145">В этом случае продолжение следующие инструкции для входа hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="d89e3-146">После успешного входа в учетную запись Azure, hello **управление подписками** появляется диалоговое окно список подписок, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="d89e3-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="d89e3-147">Если существует несколько перечисленных подписок и необходимо toowork с к определенному подмножеству из них, могут при необходимости снимите флажок hello тех, которые вы хотите toouse.</span><span class="sxs-lookup"><span data-stu-id="d89e3-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="d89e3-148">После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Диалоговое окно управления подписками][05]
5. <span data-ttu-id="d89e3-150">Здравствуйте, когда **развертывание tooAzure контейнера приложения Web** диалоговое окно, будут отображаться все контейнеры веб-приложения, созданные ранее, если вы не создали все контейнеры, hello список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="d89e3-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Развертывание tooAzure контейнера приложения веб-диалоговое окно][06]
6. <span data-ttu-id="d89e3-152">Если не создано контейнере Azure Web приложения до, или если вы хотите toopublish tooa приложения в новый контейнер, используйте hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="d89e3-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="d89e3-153">В противном случае выберите существующий контейнер Web App и пропустить toostep ниже 7.</span><span class="sxs-lookup"><span data-stu-id="d89e3-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="d89e3-154">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="d89e3-154">Click **New...**</span></span>
      
       ![Развертывание tooAzure контейнера приложения веб-диалоговое окно][15]
   2. <span data-ttu-id="d89e3-156">Hello **новый контейнер веб-приложения** будет отображаться диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="d89e3-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Диалоговое окно нового контейнера веб-приложения][07a]
   3. <span data-ttu-id="d89e3-158">Введите **метка DNS** для Web App контейнера; оно сформирует hello конечного DNS метку hello URL-адрес узла для веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="d89e3-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="d89e3-159">(Обратите внимание, это имя hello должно быть доступны и соответствовать требованиям к именам tooAzure веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="d89e3-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="d89e3-160">В hello **контейнера Web** раскрывающееся меню, выберите hello соответствующее программное обеспечение для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="d89e3-161">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="d89e3-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="d89e3-162">Последние распространения программного обеспечения hello выбран будет предоставлено Azure, и он будет выполняться в последних распространения JDK 8 Oracle, созданные и предоставляемые Azure.</span><span class="sxs-lookup"><span data-stu-id="d89e3-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="d89e3-163">В hello **подписки** раскрывающееся меню, выберите hello подписку toouse для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="d89e3-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="d89e3-164">В hello **группы ресурсов** раскрывающееся меню, выберите hello группы ресурсов, с которой необходимо tooassociate веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="d89e3-165">(Групп ресурсов azure позволяют вам toogroup ресурсы, связанные с друг с другом, чтобы, например, их можно удалить вместе.)</span><span class="sxs-lookup"><span data-stu-id="d89e3-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="d89e3-166">(Если имеются), можно выбрать существующую группу ресурсов и пропустить toostep ж ниже или используйте hello указанные шаги toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d89e3-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="d89e3-167">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="d89e3-167">Click **New...**</span></span>
      * <span data-ttu-id="d89e3-168">Hello **новую группу ресурсов** будет отображаться диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="d89e3-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно новой группы ресурсов][08]
      * <span data-ttu-id="d89e3-170">В hello hello **имя** текстового поля, укажите имя для новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d89e3-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="d89e3-171">В hello hello **область** раскрывающееся меню, выберите hello соответствующие центра обработки данных Azure расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d89e3-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="d89e3-172">Необязательно: По умолчанию последних распределение Java 8 будут развернуты в Azure автоматически tooyour web app контейнера в качестве вашей виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="d89e3-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="d89e3-173">Тем не менее если это требуется для веб-приложения можно указать другой версии и распространение hello виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="d89e3-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="d89e3-174">hello toospecify JDK для веб-приложения щелкните hello **JDK** и выберите один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="d89e3-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="d89e3-175">**Развертывание по умолчанию hello JDK, предлагаемые службой веб-приложениях Azure**: этот параметр будет развертывать последние распределение Java 8.</span><span class="sxs-lookup"><span data-stu-id="d89e3-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="d89e3-176">**Развернуть сторонний пакет JDK, доступный в Azure**: этот параметр позволяет toochoose hello списке пакетов JDK, предоставляемых Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d89e3-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="d89e3-177">**Развертывание собственных JDK из этого расположения загрузки**: этот параметр позволяет toospecify собственные распространение JDK, которое необходимо упаковать в ZIP-файл и отправить tooeither расположения общедоступным загрузки или хранилище Azure учетной записи для которого вы имеете доступ.</span><span class="sxs-lookup"><span data-stu-id="d89e3-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Диалоговое окно нового контейнера веб-приложения][07b]
   7. <span data-ttu-id="d89e3-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-179">Click **OK**.</span></span>
   8. <span data-ttu-id="d89e3-180">Hello **план служб приложений** раскрывающемся списке перечислены hello планах службы приложений, связанных с hello выбранная группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d89e3-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="d89e3-181">(Планы служб приложений укажите сведения, такие как расположение веб-приложения, hello Ценовая категория и размер экземпляра вычислений hello hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="d89e3-182">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="d89e3-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="d89e3-183">Можно выбрать существующий план службы приложений (если имеются) и пропустить h toostep ниже или использовать hello выполнив эти действия, toocreate новый план служб приложений:</span><span class="sxs-lookup"><span data-stu-id="d89e3-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="d89e3-184">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="d89e3-184">Click **New...**</span></span>
      * <span data-ttu-id="d89e3-185">Hello **новый план служб приложений** будет отображаться диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="d89e3-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Диалоговое окно нового плана службы приложений][09]
      * <span data-ttu-id="d89e3-187">В hello hello **имя** текстового поля, укажите имя для нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d89e3-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="d89e3-188">В hello hello **расположение** раскрывающееся меню, выберите hello соответствующие центра обработки данных Azure расположение плана hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="d89e3-189">В hello hello **ценовую категорию** раскрывающееся меню, выберите hello соответствующие цены для плана hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="d89e3-190">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="d89e3-191">В hello hello **размер экземпляра** раскрывающееся меню, размер соответствующему экземпляру выберите hello hello плана.</span><span class="sxs-lookup"><span data-stu-id="d89e3-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="d89e3-192">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="d89e3-193">После завершения hello выше шаги диалоговое окно новый контейнер веб-приложения hello должна выглядеть hello следующие иллюстрации:</span><span class="sxs-lookup"><span data-stu-id="d89e3-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Диалоговое окно нового контейнера веб-приложения][10]
   10. <span data-ttu-id="d89e3-195">Нажмите кнопку **ОК** toocomplete hello Создание веб-приложения в новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="d89e3-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="d89e3-196">Подождите несколько секунд, чтобы список hello toobe контейнеры веб-приложения hello обновление, и приложение контейнера только что созданный веб теперь должен быть выбран в списке hello.</span><span class="sxs-lookup"><span data-stu-id="d89e3-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="d89e3-197">Теперь будут готовы toocomplete hello первоначального развертывания tooAzure вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="d89e3-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Развертывание tooAzure контейнера приложения веб-диалоговое окно][11]
   
    <span data-ttu-id="d89e3-199">Нажмите кнопку **ОК** toodeploy вашей toohello приложения Java выбранного веб-приложения контейнера.</span><span class="sxs-lookup"><span data-stu-id="d89e3-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="d89e3-200">По умолчанию приложение будет развертываться как подкаталог hello сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="d89e3-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="d89e3-201">Если вы хотите развернуть в качестве корневого приложения hello toobe проверьте hello **развертывание tooroot** флажок перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="d89e3-202">Далее вы увидите hello **журнал действий Azure** представление, которое будет указывать hello состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Журнал действий Azure][12]
   
    <span data-ttu-id="d89e3-204">процесс развертывания tooAzure вашего веб-приложения Hello займет всего несколько секунд toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d89e3-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="d89e3-205">При готовности вашего приложения, вы увидите ссылку с именем **опубликовано** в hello **состояние** столбца.</span><span class="sxs-lookup"><span data-stu-id="d89e3-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="d89e3-206">Если щелкнуть ссылку hello, займет Домашняя страница tooyour развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="d89e3-207">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d89e3-207">Updating your web app</span></span>
<span data-ttu-id="d89e3-208">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="d89e3-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="d89e3-209">Вы можете обновить развертывание hello существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="d89e3-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="d89e3-210">Вы можете опубликовать дополнительные toohello приложения Java же контейнера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="d89e3-211">В любом случае процесс hello идентичны и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="d89e3-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="d89e3-212">В обозревателе проектов Eclipse hello щелкните правой кнопкой мыши приложение Java hello требуется tooupdate или добавить tooan существующего контейнера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="d89e3-213">В появившемся контекстном меню hello выберите **Azure** и затем **опубликовать как веб-приложения Azure...**</span><span class="sxs-lookup"><span data-stu-id="d89e3-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="d89e3-214">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d89e3-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="d89e3-215">Здравствуйте, выберите один требуется toopublish или повторно опубликовать вашей tooand приложений Java, нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="d89e3-216">Здравствуйте, более поздней версии, через несколько секунд **журнал действий Azure** представлении будут показаны обновленные развертывание в качестве **опубликовано** и будет может tooverify обновленные приложения в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="d89e3-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="d89e3-217">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d89e3-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="d89e3-218">toostart или остановить существующий контейнер веб-приложения Azure, (включая все приложения Java hello развернут в нем), можно использовать hello **обозреватель Azure** представления.</span><span class="sxs-lookup"><span data-stu-id="d89e3-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="d89e3-219">Если hello **обозреватель Azure** представление еще не открыт, его можно открыть, щелкнув затем **окна** меню в Eclipse, щелкните **Показать представление**, затем **других...** , затем **Azure**, а затем нажмите кнопку **обозреватель Azure**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="d89e3-220">Если ранее был не выполнен вход, система предложит вам toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="d89e3-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="d89e3-221">Здравствуйте, когда **обозреватель Azure** отображается представление, используйте выполните эти шаги toostart или остановить веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="d89e3-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="d89e3-222">Разверните hello **Azure** узла.</span><span class="sxs-lookup"><span data-stu-id="d89e3-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="d89e3-223">Разверните hello **веб-приложений** узла.</span><span class="sxs-lookup"><span data-stu-id="d89e3-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="d89e3-224">Щелкните правой кнопкой мыши hello требуемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d89e3-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="d89e3-225">В появившемся контекстном меню hello перейдите **запустить**, **остановить**, или **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="d89e3-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="d89e3-226">Обратите внимание, что пункты меню hello контекстно зависимые, поэтому можно только остановить выполнение веб-приложение или запустить веб-приложение, в котором в данный момент не выполняется.</span><span class="sxs-lookup"><span data-stu-id="d89e3-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Остановка существующего веб-приложения][13]

## <a name="next-steps"></a><span data-ttu-id="d89e3-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d89e3-228">Next Steps</span></span>
<span data-ttu-id="d89e3-229">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="d89e3-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="d89e3-230">[средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d89e3-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d89e3-231">[hello Установка средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d89e3-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d89e3-232">*Создание веб-приложения Hello World для Azure в Eclipse (в этой статье)*</span><span class="sxs-lookup"><span data-stu-id="d89e3-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="d89e3-233">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="d89e3-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="d89e3-234">[Набор средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d89e3-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d89e3-235">[Установка hello Azure Toolkit для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d89e3-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d89e3-236">[Создание веб-приложения Hello World для Azure в IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d89e3-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="d89e3-237">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="d89e3-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="d89e3-238">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].</span><span class="sxs-lookup"><span data-stu-id="d89e3-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="d89e3-239">Дополнительные сведения о создании веб-приложения Azure см. в разделе hello [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="d89e3-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[средств Azure для Eclipse]: ../azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Hello World для Azure в IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[hello Установка средств Azure для Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Новые возможности средств Azure для Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Обзор веб-приложений]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
