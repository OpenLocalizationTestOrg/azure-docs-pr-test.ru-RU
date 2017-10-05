---
title: "Создание веб-приложения Azure (цен. категория \"Базовый\") в IntelliJ | Документация Майкрософт"
description: "В этом учебнике показано, как с помощью набора средств Azure для IntelliJ создать веб-приложение Hello World для Azure."
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="d8454-103">Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ</span><span class="sxs-lookup"><span data-stu-id="d8454-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="d8454-104">В этом учебнике показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d8454-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="d8454-105">Для простоты мы приводим базовый пример на JSP, но схожие действия подойдут и для сервлета Java, если речь идет о развертывании в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="d8454-106">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8454-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Пример веб-страницы][01]

## <a name="prerequisites"></a><span data-ttu-id="d8454-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d8454-108">Prerequisites</span></span>
* <span data-ttu-id="d8454-109">Пакет SDK для Java (JDK) 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d8454-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="d8454-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="d8454-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="d8454-111">Его можно скачать по адресу <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="d8454-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="d8454-112">Дистрибутив веб-сервера или сервера приложений на основе Java, например [Apache Tomcat] или [Jetty].</span><span class="sxs-lookup"><span data-stu-id="d8454-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="d8454-113">Подписка на Azure, которую можно получить, перейдя по ссылке <https://azure.microsoft.com/free/> или <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="d8454-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="d8454-114">[средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d8454-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="d8454-115">Дополнительные сведения об установке см. в статье [Установка набора средств Azure для IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="d8454-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="d8454-116">Создание приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="d8454-116">To create a Hello World application</span></span>
<span data-ttu-id="d8454-117">Сначала необходимо создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="d8454-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="d8454-118">Запустите IntelliJ и щелкните меню **File** (Файл), затем щелкните **New** (Создать) и **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="d8454-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Файл > Создать > Проект][02]
2. <span data-ttu-id="d8454-120">В диалоговом окне "New Project" (Создание проекта) выберите **Java**, а затем установите флажок **Web Application** (Веб-приложение) и нажмите кнопку **New** (Создать), чтобы добавить пакет SDK для проектов.</span><span class="sxs-lookup"><span data-stu-id="d8454-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Диалоговое окно «Новый проект»][03a]
   
3. <span data-ttu-id="d8454-122">В диалоговом окне "Select Home Directory for JDK" (Выбор корневого каталога для JDK) выберите папку для установки JDK, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8454-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="d8454-123">Нажмите кнопку **Next** (Далее) в диалоговом окне "New Project" (Создание проекта), чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="d8454-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Указание корневого каталога JDK][03b]
4. <span data-ttu-id="d8454-125">Укажите имя проекта **Java-Web-App-On-Azure** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="d8454-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Диалоговое окно "Новый проект"][04]
5. <span data-ttu-id="d8454-127">В представлении обозревателя проектов IntelliJ разверните **Java-Web-App-On-Azure**, а затем разверните **web** и дважды щелкните **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="d8454-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Открытие страницы индексации][05c]
6. <span data-ttu-id="d8454-129">При открытии в IntelliJ файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="d8454-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="d8454-130">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="d8454-130">within the existing `<body>` element.</span></span> <span data-ttu-id="d8454-131">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="d8454-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="d8454-132">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="d8454-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="d8454-133">Развертывание приложения в контейнере веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="d8454-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="d8454-134">Существует несколько способов, с помощью которых можно развернуть веб-приложение Java в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="d8454-135">В этом учебнике описывается один из самых простых: ваше приложение будет развернуто в контейнер веб-приложения Azure — для этого не нужно выбирать особый тип проекта и не требуются дополнительные инструменты.</span><span class="sxs-lookup"><span data-stu-id="d8454-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="d8454-136">JDK и программное обеспечение веб-контейнера будут предоставлены Azure, поэтому нет необходимости загружать их самостоятельно. Все, что вам нужно — ваше веб-приложение Java.</span><span class="sxs-lookup"><span data-stu-id="d8454-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="d8454-137">В результате процесс публикации приложения занимает несколько секунд, а не минут.</span><span class="sxs-lookup"><span data-stu-id="d8454-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="d8454-138">Прежде чем публиковать приложение, необходимо сначала настроить параметры модуля.</span><span class="sxs-lookup"><span data-stu-id="d8454-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="d8454-139">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d8454-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="d8454-140">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="d8454-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="d8454-141">В открывшемся контекстном меню щелкните **Open Module Settings** (Открыть параметры модуля).</span><span class="sxs-lookup"><span data-stu-id="d8454-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Открытие параметров модуля][05a]
2. <span data-ttu-id="d8454-143">В отобразившемся диалоговом окне "Project Structure" (Структура проекта) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="d8454-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="d8454-144">а.</span><span class="sxs-lookup"><span data-stu-id="d8454-144">a.</span></span> <span data-ttu-id="d8454-145">В списке **Project Settings** (Параметры проекта) щелкните **Artifacts** (Артефакты).</span><span class="sxs-lookup"><span data-stu-id="d8454-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="d8454-146">b.</span><span class="sxs-lookup"><span data-stu-id="d8454-146">b.</span></span> <span data-ttu-id="d8454-147">Измените имя артефакта в поле **Name** (Имя) таким образом, чтобы оно не содержало пробелы или специальные знаки. Это необходимо, так как имя будет использоваться в универсальном коде ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="d8454-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="d8454-148">В.</span><span class="sxs-lookup"><span data-stu-id="d8454-148">c.</span></span> <span data-ttu-id="d8454-149">Измените значение параметра **Type** (Тип) на **Web Application: Archive** (Веб-приложение: архив).</span><span class="sxs-lookup"><span data-stu-id="d8454-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="d8454-150">d.</span><span class="sxs-lookup"><span data-stu-id="d8454-150">d.</span></span> <span data-ttu-id="d8454-151">Нажмите кнопку **OK**, чтобы закрыть диалоговое окно "Project Structure" (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="d8454-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Открытие параметров модуля][05b]

<span data-ttu-id="d8454-153">После настройки параметров модуля можно опубликовать приложение в Azure, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d8454-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="d8454-154">Щелкните правой кнопкой мыши по проекту **Java-Web-App-On-Azure** в обозревателе проектов IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="d8454-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="d8454-155">В контекстном меню выберите **Azure**, а затем щелкните **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="d8454-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Контекстное меню публикации в Azure][06]
2. <span data-ttu-id="d8454-157">Если вы еще не вошли в Azure из IntelliJ, появится запрос на вход в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="d8454-158">При наличии нескольких учетных записей Azure некоторые запросы во время входа в систему могут отображаться несколько раз, даже если они выглядят одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="d8454-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="d8454-159">Если это происходит, выполните вход согласно указаниям.</span><span class="sxs-lookup"><span data-stu-id="d8454-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Диалоговое окно входа в Azure][07]
3. <span data-ttu-id="d8454-161">После успешного входа в учетную запись Azure в диалоговом окне **Управление подписками** отобразится список подписок, связанных с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="d8454-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="d8454-162">(Если список содержит несколько подписок и вы будете работать только с некоторыми из них, снимите флажки для подписок, которые не будете использовать.) После выбора подписок щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="d8454-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Управление подписками][08]
4. <span data-ttu-id="d8454-164">При открытии диалогового окна **Deploy to Azure Web App Container** (Развертывание в контейнер веб-приложения Azure) в нем будут показаны все контейнеры веб-приложений, созданные ранее. Если вы не создали ни одного контейнера, список будет пустым.</span><span class="sxs-lookup"><span data-stu-id="d8454-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Контейнеры приложений][09]
5. <span data-ttu-id="d8454-166">Если вы не создавали контейнер веб-приложения Azure или хотите опубликовать приложение в новый контейнер, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d8454-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="d8454-167">В противном случае выберите существующий контейнер веб-приложения и перейдите к шагу 6 ниже.</span><span class="sxs-lookup"><span data-stu-id="d8454-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="d8454-168">Нажмите **+**</span><span class="sxs-lookup"><span data-stu-id="d8454-168">Click **+**</span></span>
      
       ![Добавление контейнера приложения][10]
   2. <span data-ttu-id="d8454-170">Откроется окно **Новый контейнер веб-приложения** , которым мы воспользуемся для нескольких следующих шагов.</span><span class="sxs-lookup"><span data-stu-id="d8454-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Создание контейнера приложения][11a]
   3. <span data-ttu-id="d8454-172">Укажите **метку DNS** для контейнера веб-приложения. Она образует метку листа DNS для URL-адреса узла веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="d8454-173">(Примечание. Имя должно быть доступным и соответствовать требованиям к именованию веб-приложений Azure.)</span><span class="sxs-lookup"><span data-stu-id="d8454-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="d8454-174">В раскрывающемся меню **Веб-контейнер** выберите для своего приложения соответствующее программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="d8454-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="d8454-175">На данный момент можно выбрать Tomcat 8, Tomcat 7 или Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="d8454-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="d8454-176">Последний дистрибутив выбранного программного обеспечения, предоставленный Azure, будет запущен в последнем дистрибутиве JDK 8, созданном Oracle и предоставленном Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="d8454-177">В раскрывающемся меню **Подписка** выберите подписку, которую вы хотите использовать для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="d8454-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="d8454-178">В раскрывающемся меню **Группа ресурсов** выберите группу ресурсов, с которой вы хотите связать свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d8454-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="d8454-179">(Группы ресурсов Azure позволяют сгруппировать связанные ресурсы, чтобы, например, удалить их одновременно.)</span><span class="sxs-lookup"><span data-stu-id="d8454-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="d8454-180">Можно выбрать существующую группу ресурсов (если она есть) и перейти к шагу g ниже, или создать новую, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="d8454-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="d8454-181">Из раскрывающегося меню **Группы ресурсов** выберите пункт **&lt;&lt;Создать новую группу ресурсов&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="d8454-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="d8454-182">Откроется диалоговое окно **Новая группа ресурсов** :</span><span class="sxs-lookup"><span data-stu-id="d8454-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Создание группы ресурсов][12]
      * <span data-ttu-id="d8454-184">В текстовое поле **Имя** введите имя новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8454-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="d8454-185">В раскрывающемся меню **Регион** выберите расположение центра обработки данных Azure для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8454-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="d8454-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8454-186">Click **OK**.</span></span>
   7. <span data-ttu-id="d8454-187">В раскрывающемся меню **План службы приложений** перечислены планы службы приложений, связанные с выбранной группой ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d8454-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="d8454-188">В плане службы приложений указываются такие сведения, как расположение веб-приложения, ценовая категория и размер вычислительной операции.</span><span class="sxs-lookup"><span data-stu-id="d8454-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="d8454-189">Один план службы приложений можно использовать для нескольких веб-приложений, поэтому он поддерживается отдельно от развертывания конкретного веб-приложения.)</span><span class="sxs-lookup"><span data-stu-id="d8454-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="d8454-190">Можно выбрать существующий план службы приложений (если он есть) и перейти к шагу h ниже, или создать новый, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="d8454-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="d8454-191">Из раскрывающегося меню **План службы приложений** выберите пункт **&lt;&lt;Создать новый план службы приложений&gt;&gt;**.</span><span class="sxs-lookup"><span data-stu-id="d8454-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="d8454-192">Откроется диалоговое окно **Новый план службы приложений** :</span><span class="sxs-lookup"><span data-stu-id="d8454-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Новый план службы приложений][13]
      * <span data-ttu-id="d8454-194">В текстовое поле **Имя** введите имя нового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d8454-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="d8454-195">В раскрывающемся меню **Расположение** выберите расположение центра обработки данных Azure для плана.</span><span class="sxs-lookup"><span data-stu-id="d8454-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="d8454-196">В раскрывающемся меню **Ценовая категория** выберите соответствующую ценовую категорию для плана.</span><span class="sxs-lookup"><span data-stu-id="d8454-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="d8454-197">Для тестирования можно выбрать категорию **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="d8454-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="d8454-198">В раскрывающемся меню **Размер экземпляра** выберите для плана соответствующий размер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d8454-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="d8454-199">Для тестирования можно выбрать **Маленький**.</span><span class="sxs-lookup"><span data-stu-id="d8454-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="d8454-200">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8454-200">Click **OK**.</span></span>
   8. <span data-ttu-id="d8454-201">(Необязательно.) По умолчанию Azure автоматически развернет последний дистрибутив Java 8 в ваш контейнер веб-приложения в качестве виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="d8454-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="d8454-202">Тем не менее можно выбрать другую версию и дистрибутив виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="d8454-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="d8454-203">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d8454-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="d8454-204">Щелкните вкладку **JDK** в диалоговом окне **New Web App Container** (Создание контейнера веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="d8454-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="d8454-205">Можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="d8454-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="d8454-206">Развернуть пакет JDK по умолчанию, предлагаемый в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="d8454-207">Развернуть сторонний пакет JDK из раскрывающегося списка дополнительных пакетов JDK, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="d8454-208">Развернуть пользовательский пакет JDK, который должен быть упакован в виде ZIP-файла и быть общедоступным или находиться в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d8454-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Вкладка JDK в окне создания контейнера приложения][11b]
   9. <span data-ttu-id="d8454-210">После завершения всех описанных выше действий диалоговое окно "Новый контейнер веб-приложения" должно выглядеть примерно так, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d8454-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Создание контейнера приложения][14]
   10. <span data-ttu-id="d8454-212">Нажмите кнопку **ОК** , чтобы создать контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="d8454-213">Подождите несколько секунд. Когда список контейнеров веб-приложений обновится, созданный контейнер веб-приложения должен быть выбран в списке.</span><span class="sxs-lookup"><span data-stu-id="d8454-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="d8454-214">Теперь все готово для начального развертывания веб-приложения в Azure. Нажмите кнопку **ОК**, чтобы развернуть приложение Java в выбранный контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="d8454-215">По умолчанию приложение будет развернуто в подкаталог сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="d8454-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="d8454-216">Чтобы развернуть приложение в качестве корневого приложения, установите флажок **Deploy to root** (Развернуть в корень) перед нажатием кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8454-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Развертывание в Azure][15]
7. <span data-ttu-id="d8454-218">После этого вы должны увидеть представление **Журнал действий Azure** , в котором будет отображаться состояние развертывания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Индикатор хода выполнения][16]
   
    <span data-ttu-id="d8454-220">Процесс развертывания веб-приложения в Azure занимает всего несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="d8454-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="d8454-221">Когда процесс будет завершен, вы увидите ссылку **Опубликовано** in the **Состояние** .</span><span class="sxs-lookup"><span data-stu-id="d8454-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="d8454-222">При щелчке по ссылке вы перейдете на домашнюю страницу развернутого веб-приложения. Вы также можете найти свое веб-приложение, выполнив действия, описанные в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="d8454-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="d8454-223">Переход к веб-приложению в Azure</span><span class="sxs-lookup"><span data-stu-id="d8454-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="d8454-224">Чтобы перейти к веб-приложению в Azure, можно использовать представление **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d8454-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="d8454-225">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="d8454-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="d8454-226">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="d8454-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="d8454-227">Когда представление **Azure Explorer** откроется, выполните следующие действия, чтобы перейти к своему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="d8454-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="d8454-228">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="d8454-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="d8454-229">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="d8454-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="d8454-230">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d8454-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="d8454-231">В открывшемся контекстном меню выберите пункт **Открыть в браузере**.</span><span class="sxs-lookup"><span data-stu-id="d8454-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Просмотр веб-приложения][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="d8454-233">Обновление веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d8454-233">Updating your web app</span></span>
<span data-ttu-id="d8454-234">Обновить существующее и запущенное веб-приложение Azure быстро и просто. Сделать это можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="d8454-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="d8454-235">Можно обновить развертывание существующего веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="d8454-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="d8454-236">Можно опубликовать дополнительное приложение Java в тот же контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="d8454-237">Процесс в каждом случае идентичен и занимает несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="d8454-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="d8454-238">В обозревателе проектов IntelliJ щелкните правой кнопкой мыши приложение Java, которое вы хотите обновить или добавить в существующий контейнер веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="d8454-239">В контекстном меню выберите **Azure**, а затем щелкните **Опубликовать как веб-приложение Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8454-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="d8454-240">Так как ранее вы уже вошли в систему, вы увидите список существующих контейнеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d8454-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="d8454-241">Выберите контейнер, в котором вы хотите опубликовать или повторно опубликовать приложение Java, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d8454-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="d8454-242">Через несколько секунд в представлении **Журнал действий Azure** состояние обновленного развертывания изменится на **Опубликовано**, и вы сможете проверить свое обновленное приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="d8454-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="d8454-243">Запуск, остановка или перезапуск существующего веб-приложения</span><span class="sxs-lookup"><span data-stu-id="d8454-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="d8454-244">Запустить или остановить существующий контейнер веб-приложения Azure (включая все развернутые в нем приложения Java) можно в представлении **Обозреватель Azure** .</span><span class="sxs-lookup"><span data-stu-id="d8454-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="d8454-245">Если представление **Обозреватель Azure** еще не открыто, его можно открыть, щелкнув меню **View** (Представление) в IntelliJ и последовательно выбрав **Tool Windows** (Окна инструментов) и **Service Explorer** (Обозреватель служб).</span><span class="sxs-lookup"><span data-stu-id="d8454-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="d8454-246">Если ранее вы не вошли в систему, вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="d8454-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="d8454-247">Когда представление **Обозреватель Azure** откроется, выполните следующие действия для запуска или остановки веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d8454-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="d8454-248">Разверните узел **Azure** .</span><span class="sxs-lookup"><span data-stu-id="d8454-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="d8454-249">Разверните узел **Web Apps** (Веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="d8454-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="d8454-250">Щелкните правой кнопкой мыши необходимое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d8454-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="d8454-251">В открывшемся контекстном меню выберите **Запустить**, **Остановить** или **Перезапустить**.</span><span class="sxs-lookup"><span data-stu-id="d8454-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="d8454-252">Обратите внимание, что доступные меню контекстно зависимы, поэтому можно только остановить веб-приложение или запустить веб-приложение, которое в данный момент не запущено.</span><span class="sxs-lookup"><span data-stu-id="d8454-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Остановка веб-приложения][18]

## <a name="next-steps"></a><span data-ttu-id="d8454-254">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8454-254">Next Steps</span></span>
<span data-ttu-id="d8454-255">Дополнительные сведения о наборах средств Azure для Java IDE см. по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="d8454-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="d8454-256">[Набор средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d8454-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d8454-257">[Установка набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d8454-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="d8454-258">[Создание веб-приложения Hello World для Azure в Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d8454-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="d8454-259">[Новые возможности набора средств Azure для Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d8454-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="d8454-260">[средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d8454-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d8454-261">[Установка набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d8454-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="d8454-262">*Создание веб-приложения Hello World для Azure в IntelliJ (в этой статье)*</span><span class="sxs-lookup"><span data-stu-id="d8454-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="d8454-263">[Новые возможности набора средств Azure для IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="d8454-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="d8454-264">См. также</span><span class="sxs-lookup"><span data-stu-id="d8454-264">See Also</span></span>
<span data-ttu-id="d8454-265">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure].</span><span class="sxs-lookup"><span data-stu-id="d8454-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="d8454-266">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="d8454-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Набор средств Azure для Eclipse]: ../azure-toolkit-for-eclipse.md
[средств Azure для IntelliJ]: ../azure-toolkit-for-intellij.md
[Создание веб-приложения Hello World для Azure в Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Установка набора средств Azure для Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Установка набора средств Azure для IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Новые возможности набора средств Azure для Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Новые возможности набора средств Azure для IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
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
