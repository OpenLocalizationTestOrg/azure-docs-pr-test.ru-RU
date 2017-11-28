---
title: "Основные веб-приложение Azure в IntelliJ aaaCreate | Документы Microsoft"
description: "Этот учебник показывает, как toouse hello Azure Toolkit для IntelliJ toocreate веб-приложения Hello World для Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="6217e-103">Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="6217e-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="6217e-104">В этом учебнике показано как toocreate и развертывание основных tooAzure приложения Hello World как веб-приложения с помощью hello [средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="6217e-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="6217e-105">Для простоты мы приводим базовый пример на JSP, но схожие действия подойдут и для сервлета Java, если речь идет о развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="6217e-106">После завершения этого учебника, приложение будет выглядеть аналогично toohello при просмотре в веб-браузере следующие иллюстрации:</span><span class="sxs-lookup"><span data-stu-id="6217e-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Пример веб-страницы][01]

## <a name="prerequisites"></a><span data-ttu-id="6217e-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6217e-108">Prerequisites</span></span>
* <span data-ttu-id="6217e-109">Пакет SDK для Java (JDK) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="6217e-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="6217e-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="6217e-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="6217e-111">Его можно скачать по адресу <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="6217e-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="6217e-112">Дистрибутив веб-сервера или сервера приложений на основе Java, например [Apache Tomcat] или [Jetty].</span><span class="sxs-lookup"><span data-stu-id="6217e-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="6217e-113">Подписка на Azure, которую можно получить, перейдя по ссылке <https://azure.microsoft.com/free/> или <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="6217e-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="6217e-114">Hello [средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="6217e-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="6217e-115">Сведения об установке средств Azure hello см. в разделе [hello установка набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="6217e-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="6217e-116">toocreate приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="6217e-116">toocreate a Hello World application</span></span>
<span data-ttu-id="6217e-117">Сначала необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="6217e-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="6217e-118">Запустите IntelliJ и нажмите кнопку hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="6217e-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Файл > Создать > Проект][02]
2. <span data-ttu-id="6217e-120">В диалоговом окне нового проекта hello, выберите **Java**, затем **веб-приложение**и нажмите кнопку **New** tooadd SDK проекта.</span><span class="sxs-lookup"><span data-stu-id="6217e-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Диалоговое окно "Новый проект"][03a]
   
3. <span data-ttu-id="6217e-122">В hello выберите домашний каталог диалогового окна JDK, hello выберите папку для установки JDK, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6217e-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="6217e-123">Нажмите кнопку **Далее** в toocontinue поле диалоговое окно нового проекта hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Указание корневого каталога JDK][03b]
4. <span data-ttu-id="6217e-125">В целях этого учебника назовите проект hello **Java-веб-приложения-на-Azure**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6217e-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Диалоговое окно "Новый проект"][04]
5. <span data-ttu-id="6217e-127">В представлении обозревателя проектов IntelliJ разверните **Java-Web-App-On-Azure**, а затем разверните **web** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="6217e-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Открытие страницы индексации][05c]
6. <span data-ttu-id="6217e-129">При открытии файла index.jsp в IntelliJ, добавьте в виде текста toodynamically **Здравствуй, мир!**</span><span class="sxs-lookup"><span data-stu-id="6217e-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="6217e-130">в существующих hello `<body>` элемента.</span><span class="sxs-lookup"><span data-stu-id="6217e-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="6217e-131">Обновленный `<body>` содержимого должен быть похож на следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="6217e-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="6217e-132">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="6217e-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="6217e-133">toodeploy tooan вашего приложения Azure Web приложения контейнера</span><span class="sxs-lookup"><span data-stu-id="6217e-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="6217e-134">Существует несколько способов, с помощью которых можно развернуть tooAzure приложения Java web.</span><span class="sxs-lookup"><span data-stu-id="6217e-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="6217e-135">В данном учебнике один простой hello: приложение будет tooan развернутого приложения контейнера Azure веб - нет типа конкретного проекта, ни дополнительные средства необходимы.</span><span class="sxs-lookup"><span data-stu-id="6217e-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="6217e-136">Hello JDK и hello web контейнера программного обеспечения будут предоставляться автоматически Azure, поэтому нет необходимости tooupload собственные; все, что необходимо — веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="6217e-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="6217e-137">В результате hello процесс публикации для приложения может занять секунд, не минут.</span><span class="sxs-lookup"><span data-stu-id="6217e-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="6217e-138">Прежде чем публиковать приложение, необходимо сначала tooconfigure параметры модуля.</span><span class="sxs-lookup"><span data-stu-id="6217e-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="6217e-139">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6217e-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="6217e-140">В обозревателе проектов IntelliJ щелкните правой кнопкой мыши hello **Java-веб-приложения-на-Azure** проекта.</span><span class="sxs-lookup"><span data-stu-id="6217e-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6217e-141">В появившемся контекстном меню hello перейдите **открыть параметры модуля**.</span><span class="sxs-lookup"><span data-stu-id="6217e-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Открытие параметров модуля][05a]
2. <span data-ttu-id="6217e-143">При отображении hello структура проекта-диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6217e-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="6217e-144">а.</span><span class="sxs-lookup"><span data-stu-id="6217e-144">a.</span></span> <span data-ttu-id="6217e-145">Нажмите кнопку **артефакты** в списке hello **параметры проекта**.</span><span class="sxs-lookup"><span data-stu-id="6217e-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="6217e-146">b.</span><span class="sxs-lookup"><span data-stu-id="6217e-146">b.</span></span> <span data-ttu-id="6217e-147">Изменение имени артефакта hello в hello **имя** , чтобы она не содержит пробелы или специальные символы; это необходимо, поскольку hello имя будет использоваться в hello универсальный код ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="6217e-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="6217e-148">c.</span><span class="sxs-lookup"><span data-stu-id="6217e-148">c.</span></span> <span data-ttu-id="6217e-149">Изменение hello **тип** слишком**веб-приложения: архив**.</span><span class="sxs-lookup"><span data-stu-id="6217e-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="6217e-150">d.</span><span class="sxs-lookup"><span data-stu-id="6217e-150">d.</span></span> <span data-ttu-id="6217e-151">Нажмите кнопку **ОК** tooclose hello структура проекта диалоговое окно «».</span><span class="sxs-lookup"><span data-stu-id="6217e-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Открытие параметров модуля][05b]

<span data-ttu-id="6217e-153">При настройке параметров модуля можно опубликовать tooAzure вашего приложения с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6217e-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="6217e-154">В обозревателе проектов IntelliJ щелкните правой кнопкой мыши hello **Java-веб-приложения-на-Azure** проекта.</span><span class="sxs-lookup"><span data-stu-id="6217e-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="6217e-155">В появившемся контекстном меню hello выберите **Azure**, а затем нажмите кнопку **опубликовать как веб-приложения Azure...**</span><span class="sxs-lookup"><span data-stu-id="6217e-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Контекстное меню публикации в Azure][06]
2. <span data-ttu-id="6217e-157">Если вы еще не выполнили в Azure из IntelliJ, запрашиваемые toosign будет в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="6217e-158">(При наличии нескольких учетных записей Azure, некоторые запросы hello процесса hello входа в систему, могут отображаться несколько раз, даже если они отображаются toobe же hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="6217e-159">В этом случае продолжение toofollow входа hello в инструкциях.)</span><span class="sxs-lookup"><span data-stu-id="6217e-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Диалоговое окно входа в Azure][07]
3. <span data-ttu-id="6217e-161">После успешного входа в учетную запись Azure, hello **управление подписками** появляется диалоговое окно список подписок, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="6217e-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="6217e-162">(Если имеется несколько подписок в списке, и требуется toowork с к определенному подмножеству из них, могут при необходимости снимите hello подписок, вы не хотите toouse.) После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="6217e-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Управление подписками][08]
4. <span data-ttu-id="6217e-164">Здравствуйте, когда **развертывание tooAzure контейнера приложения Web** диалоговое окно, будут отображаться все контейнеры веб-приложения, созданные ранее, если вы не создали все контейнеры, hello список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="6217e-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Контейнеры приложений][09]
5. <span data-ttu-id="6217e-166">Если не создано контейнере Azure Web приложения до, или если вы хотите toopublish tooa приложения в новый контейнер, используйте hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="6217e-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="6217e-167">В противном случае выберите существующий контейнер Web App и пропустить toostep 6 ниже.</span><span class="sxs-lookup"><span data-stu-id="6217e-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="6217e-168">Нажмите **+**</span><span class="sxs-lookup"><span data-stu-id="6217e-168">Click **+**</span></span>
      
       ![Добавление контейнера приложения][10]
   2. <span data-ttu-id="6217e-170">Hello **новый контейнер веб-приложения** отобразится диалоговое окно, которое будет использовать для hello рядом несколько шагов.</span><span class="sxs-lookup"><span data-stu-id="6217e-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Создание контейнера приложения][11a]
   3. <span data-ttu-id="6217e-172">Введите **метка DNS** для Web App контейнера; оно сформирует hello конечного DNS метку hello URL-адрес узла для веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="6217e-173">Обратите внимание, это имя hello должно быть доступны и соответствовать требованиям к именам tooAzure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="6217e-174">В hello **контейнера Web** раскрывающееся меню, выберите hello соответствующее программное обеспечение для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="6217e-175">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="6217e-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="6217e-176">Последние распространения программного обеспечения hello выбран будет предоставлено Azure, и он будет выполняться в последних распространения JDK 8 Oracle, созданные и предоставляемые Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="6217e-177">В hello **подписки** раскрывающееся меню, выберите hello подписку toouse для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="6217e-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="6217e-178">В hello **группы ресурсов** раскрывающееся меню, выберите hello группы ресурсов, с которой необходимо tooassociate веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="6217e-179">(Групп ресурсов azure позволяют вам toogroup ресурсы, связанные с друг с другом, чтобы, например, их можно удалить вместе.)</span><span class="sxs-lookup"><span data-stu-id="6217e-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="6217e-180">Можно выбрать существующую группу ресурсов (если имеются) и пропустить toostep ж ниже или используйте hello следующие шаги toocreate новой группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="6217e-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="6217e-181">Выберите  **&lt; &lt; создать новую группу ресурсов &gt; &gt;**  в hello **группы ресурсов** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="6217e-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="6217e-182">Hello **новую группу ресурсов** будет отображаться диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6217e-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Создание группы ресурсов][12]
      * <span data-ttu-id="6217e-184">В hello hello **имя** текстового поля, укажите имя для новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6217e-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="6217e-185">В hello hello **область** раскрывающееся меню, выберите hello соответствующие центра обработки данных Azure расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6217e-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="6217e-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6217e-186">Click **OK**.</span></span>
   7. <span data-ttu-id="6217e-187">Hello **план служб приложений** раскрывающемся списке перечислены hello планах службы приложений, связанных с hello выбранная группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6217e-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="6217e-188">(План службы приложений указывает сведения, такие как расположение веб-приложения, hello Ценовая категория и размер экземпляра вычислений hello hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="6217e-189">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="6217e-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="6217e-190">Можно выбрать существующий план службы приложений (если имеются) и пропустить h toostep ниже или использовать hello, выполнив шаги toocreate новый план служб приложений:</span><span class="sxs-lookup"><span data-stu-id="6217e-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="6217e-191">Выберите  **&lt; &lt; создать новый план служб приложений &gt; &gt;**  в hello **план служб приложений** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="6217e-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="6217e-192">Hello **новый план служб приложений** будет отображаться диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="6217e-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Новый план службы приложений][13]
      * <span data-ttu-id="6217e-194">В hello hello **имя** текстового поля, укажите имя для нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6217e-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="6217e-195">В hello hello **расположение** раскрывающееся меню, выберите hello соответствующие центра обработки данных Azure расположение плана hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="6217e-196">В hello hello **ценовую категорию** раскрывающееся меню, выберите hello соответствующие цены для плана hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="6217e-197">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="6217e-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="6217e-198">В hello hello **размер экземпляра** раскрывающееся меню, размер соответствующему экземпляру выберите hello hello плана.</span><span class="sxs-lookup"><span data-stu-id="6217e-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="6217e-199">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="6217e-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="6217e-200">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6217e-200">Click **OK**.</span></span>
   8. <span data-ttu-id="6217e-201">(Необязательно) По умолчанию последних распределение Java 8 будет развернут автоматически как вашей виртуальной машины Java Azure tooyour web app контейнером.</span><span class="sxs-lookup"><span data-stu-id="6217e-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="6217e-202">Тем не менее можно выбрать другую версию и распространение hello виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="6217e-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="6217e-203">Таким образом, toodo используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="6217e-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="6217e-204">Нажмите кнопку hello **JDK** на вкладке hello **новый контейнер веб-приложения** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6217e-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="6217e-205">Можно выбрать один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="6217e-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="6217e-206">Развертывание по умолчанию hello JDK, который предлагается в Azure</span><span class="sxs-lookup"><span data-stu-id="6217e-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="6217e-207">Развернуть сторонний пакет JDK из раскрывающегося списка дополнительных пакетов JDK, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="6217e-208">Развернуть пользовательский пакет JDK, который должен быть упакован в виде ZIP-файла и быть общедоступным или находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="6217e-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Вкладка JDK в окне создания контейнера приложения][11b]
   9. <span data-ttu-id="6217e-210">После завершения hello выше шаги диалоговое окно новый контейнер веб-приложения hello должна выглядеть hello следующие иллюстрации:</span><span class="sxs-lookup"><span data-stu-id="6217e-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Создание контейнера приложения][14]
   10. <span data-ttu-id="6217e-212">Нажмите кнопку **ОК** toocomplete hello Создание веб-приложения в новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="6217e-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="6217e-213">Подождите несколько секунд, чтобы список hello toobe контейнеры веб-приложения hello обновление, и приложение контейнера только что созданный веб теперь должен быть выбран в списке hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="6217e-214">Теперь вы находитесь готов toocomplete hello первоначального развертывания tooAzure вашего веб-приложения; Нажмите кнопку **ОК** toodeploy вашей toohello приложения Java выбранного веб-приложения контейнера.</span><span class="sxs-lookup"><span data-stu-id="6217e-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="6217e-215">По умолчанию приложение будет развертываться как подкаталог hello сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="6217e-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="6217e-216">Если вы хотите развернуть в качестве корневого приложения hello toobe проверьте hello **развертывание tooroot** флажок перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6217e-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Развертывание tooAzure][15]
7. <span data-ttu-id="6217e-218">Далее вы увидите hello **журнал действий Azure** представление, которое будет указывать hello состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Индикатор хода выполнения][16]
   
    <span data-ttu-id="6217e-220">процесс развертывания tooAzure вашего веб-приложения Hello займет всего несколько секунд toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6217e-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="6217e-221">При готовности вашего приложения, вы увидите ссылку с именем **опубликовано** в hello **состояние** столбца.</span><span class="sxs-lookup"><span data-stu-id="6217e-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="6217e-222">При выборе ссылки hello, займет Домашняя страница tooyour развертывания веб-приложения или hello шаги можно использовать в следующий раздел toobrowse tooyour веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6217e-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="6217e-223">Просмотр tooyour веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="6217e-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="6217e-224">tooyour toobrowse веб-приложения в Azure, можно использовать hello **обозреватель Azure** представления.</span><span class="sxs-lookup"><span data-stu-id="6217e-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="6217e-225">Если hello **обозреватель Azure** представление еще не открыт, его можно открыть, щелкнув затем **представление** меню в IntelliJ, затем щелкните **окна инструментов**и нажмите кнопку  **Служба обозревателя**.</span><span class="sxs-lookup"><span data-stu-id="6217e-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6217e-226">Если ранее был не выполнен вход, система предложит вам toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="6217e-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="6217e-227">Здравствуйте, когда **обозреватель Azure** отображается представление, используйте выполните эти шаги toobrowse tooyour веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="6217e-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="6217e-228">Разверните hello **Azure** узла.</span><span class="sxs-lookup"><span data-stu-id="6217e-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="6217e-229">Разверните hello **веб-приложений** узла.</span><span class="sxs-lookup"><span data-stu-id="6217e-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="6217e-230">Щелкните правой кнопкой мыши hello требуемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="6217e-231">В появившемся контекстном меню hello перейдите **открыть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="6217e-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Просмотр веб-приложения][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="6217e-233">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6217e-233">Updating your web app</span></span>
<span data-ttu-id="6217e-234">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="6217e-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="6217e-235">Вы можете обновить развертывание hello существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="6217e-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="6217e-236">Вы можете опубликовать дополнительные toohello приложения Java же контейнера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="6217e-237">В любом случае процесс hello идентичны и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="6217e-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="6217e-238">В обозревателе проектов IntelliJ hello щелкните правой кнопкой мыши приложение Java hello требуется tooupdate или добавить tooan существующего контейнера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="6217e-239">В появившемся контекстном меню hello выберите **Azure** и затем **опубликовать как веб-приложения Azure...**</span><span class="sxs-lookup"><span data-stu-id="6217e-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="6217e-240">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="6217e-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="6217e-241">Здравствуйте, выберите один требуется toopublish или повторно опубликовать вашей tooand приложений Java, нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6217e-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="6217e-242">Здравствуйте, более поздней версии, через несколько секунд **журнал действий Azure** представлении будут показаны обновленные развертывание в качестве **опубликовано** и будет может tooverify обновленные приложения в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="6217e-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="6217e-243">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6217e-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="6217e-244">toostart или остановить существующий контейнер веб-приложения Azure, (включая все приложения Java hello развернут в нем), можно использовать hello **обозреватель Azure** представления.</span><span class="sxs-lookup"><span data-stu-id="6217e-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="6217e-245">Если hello **обозреватель Azure** представление еще не открыт, его можно открыть, щелкнув затем **представление** меню в IntelliJ, затем щелкните **окна инструментов**и нажмите кнопку  **Служба обозревателя**.</span><span class="sxs-lookup"><span data-stu-id="6217e-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="6217e-246">Если ранее был не выполнен вход, система предложит вам toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="6217e-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="6217e-247">Здравствуйте, когда **обозреватель Azure** отображается представление, используйте выполните эти шаги toostart или остановить веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="6217e-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="6217e-248">Разверните hello **Azure** узла.</span><span class="sxs-lookup"><span data-stu-id="6217e-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="6217e-249">Разверните hello **веб-приложений** узла.</span><span class="sxs-lookup"><span data-stu-id="6217e-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="6217e-250">Щелкните правой кнопкой мыши hello требуемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6217e-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="6217e-251">В появившемся контекстном меню hello перейдите **запустить**, **остановить**, или **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="6217e-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="6217e-252">Обратите внимание, что пункты меню hello контекстно зависимые, поэтому можно только остановить выполнение веб-приложение или запустить веб-приложение, в котором в данный момент не выполняется.</span><span class="sxs-lookup"><span data-stu-id="6217e-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Остановка веб-приложения][18]

## <a name="next-steps"></a><span data-ttu-id="6217e-254">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6217e-254">Next Steps</span></span>
<span data-ttu-id="6217e-255">Дополнительные сведения о hello наборы инструментов Azure для Java интегрированными средами разработки. в разделе hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="6217e-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="6217e-256">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6217e-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6217e-257">[Установка средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="6217e-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="6217e-258">[Создание веб-приложения Hello World для Azure в Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6217e-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="6217e-259">[Новые возможности средств Azure для Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="6217e-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="6217e-260">[средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6217e-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6217e-261">[hello установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="6217e-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="6217e-262">*Создание веб-приложения Hello World для Azure в IntelliJ (в этой статье)*</span><span class="sxs-lookup"><span data-stu-id="6217e-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="6217e-263">[Новые возможности средств Azure для IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="6217e-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="6217e-264">См. также</span><span class="sxs-lookup"><span data-stu-id="6217e-264">See Also</span></span>
<span data-ttu-id="6217e-265">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure].</span><span class="sxs-lookup"><span data-stu-id="6217e-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="6217e-266">Дополнительные сведения о создании веб-приложения Azure см. в разделе hello [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="6217e-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Набор средств Azure для Eclipse]: ../azure-toolkit-for-eclipse.md
[средств Azure для IntelliJ]: ../azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ../azure-toolkit-for-eclipse-installation.md
[hello установка набора средств Azure для IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Новые возможности средств Azure для Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Обзор веб-приложений]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
