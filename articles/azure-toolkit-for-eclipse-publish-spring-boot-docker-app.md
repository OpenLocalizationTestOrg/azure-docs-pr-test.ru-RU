---
title: "Здравствуйте, aaaPublish Spring загрузки приложения в качестве контейнера Docker с помощью средств Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="af943-103">Опубликовать приложение Spring загрузки как контейнер Docker с помощью hello набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="af943-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="af943-104">Hello [Spring Framework] — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="af943-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="af943-105">Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="af943-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="af943-106">[Docker] — это решение открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="af943-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="af943-107">Этот учебник поможет выполнить действия toodeploy hello приложение Spring загрузки как tooMicrosoft контейнера Docker Azure с помощью hello набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="af943-108">Клонирование репозитория Docker Spring загрузки по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="af943-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="af943-109">Общедоступный репозиторий hello импорта</span><span class="sxs-lookup"><span data-stu-id="af943-109">Import hello public repository</span></span>

<span data-ttu-id="af943-110">Hello следующие шаги описывают клонирования hello Docker загрузки Spring репозитория tooyour локального компьютера с помощью IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="af943-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="af943-111">Если toouse командной строки, см. [развернуть приложение в Linux в службе контейнера Azure Spring загрузки][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="af943-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="af943-112">Откройте Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-112">Open Eclipse.</span></span>

1. <span data-ttu-id="af943-113">Последовательно выберите **Файл** > **Импортировать**.</span><span class="sxs-lookup"><span data-stu-id="af943-113">Click **File** > **Import**.</span></span>

   ![Меню "File" (Файл) > "Import" (Импортировать)][CL01]

1. <span data-ttu-id="af943-115">Здравствуйте, когда **импорта** откроется диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="af943-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="af943-116">а.</span><span class="sxs-lookup"><span data-stu-id="af943-116">a.</span></span> <span data-ttu-id="af943-117">Разверните элемент **Git**.</span><span class="sxs-lookup"><span data-stu-id="af943-117">Expand **Git**.</span></span>

   <span data-ttu-id="af943-118">b.</span><span class="sxs-lookup"><span data-stu-id="af943-118">b.</span></span> <span data-ttu-id="af943-119">Выберите **Projects from Git** (Проекты из Git).</span><span class="sxs-lookup"><span data-stu-id="af943-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="af943-120">c.</span><span class="sxs-lookup"><span data-stu-id="af943-120">c.</span></span> <span data-ttu-id="af943-121">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-121">Click **Next**.</span></span>

   ![Диалоговое окно "Import" (Импорт)][CL02]

1. <span data-ttu-id="af943-123">На hello **Выбор источника репозитория** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="af943-124">а.</span><span class="sxs-lookup"><span data-stu-id="af943-124">a.</span></span> <span data-ttu-id="af943-125">Выберите **Клонировать URI**.</span><span class="sxs-lookup"><span data-stu-id="af943-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="af943-126">b.</span><span class="sxs-lookup"><span data-stu-id="af943-126">b.</span></span> <span data-ttu-id="af943-127">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-127">Click **Next**.</span></span>

   ![Страница "Выбор источника репозитория"][CL03]

1. <span data-ttu-id="af943-129">На hello **источника репозитории** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="af943-130">а.</span><span class="sxs-lookup"><span data-stu-id="af943-130">a.</span></span> <span data-ttu-id="af943-131">В поле **URI** введите `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="af943-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="af943-132">Этот шаг должен автоматически заполнять hello **узла** и **путь репозитория** поля с hello исправьте значения.</span><span class="sxs-lookup"><span data-stu-id="af943-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="af943-133">b.</span><span class="sxs-lookup"><span data-stu-id="af943-133">b.</span></span> <span data-ttu-id="af943-134">репозиторий Hello Spring загрузки является открытым, поэтому не следует tooenter Git имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="af943-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="af943-135">c.</span><span class="sxs-lookup"><span data-stu-id="af943-135">c.</span></span> <span data-ttu-id="af943-136">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-136">Click **Next**.</span></span>

   ![Страница "Исходный репозиторий Git"][CL04]

1. <span data-ttu-id="af943-138">На hello **ветвь выбора** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Страница "Выбор ветви"][CL05]

1. <span data-ttu-id="af943-140">На hello **локальной целевой** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="af943-141">а.</span><span class="sxs-lookup"><span data-stu-id="af943-141">a.</span></span> <span data-ttu-id="af943-142">Укажите локальную папку hello место вашего локального репозитория.</span><span class="sxs-lookup"><span data-stu-id="af943-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="af943-143">b.</span><span class="sxs-lookup"><span data-stu-id="af943-143">b.</span></span> <span data-ttu-id="af943-144">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-144">Click **Next**.</span></span>

   ![Страница "Локальное назначение"][CL06]

1. <span data-ttu-id="af943-146">На hello **toouse мастер импорта проектов выберите** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="af943-147">а.</span><span class="sxs-lookup"><span data-stu-id="af943-147">a.</span></span> <span data-ttu-id="af943-148">Выберите **Import as a general project** (Импортировать как универсальный проект).</span><span class="sxs-lookup"><span data-stu-id="af943-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="af943-149">b.</span><span class="sxs-lookup"><span data-stu-id="af943-149">b.</span></span> <span data-ttu-id="af943-150">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-150">Click **Next**.</span></span>

   ![Страница «Выбор toouse мастер импорта проектов»][CL07]

1. <span data-ttu-id="af943-152">На hello **импорта проектов** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="af943-153">а.</span><span class="sxs-lookup"><span data-stu-id="af943-153">a.</span></span> <span data-ttu-id="af943-154">Укажите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="af943-154">Specify your project name.</span></span>
   
   <span data-ttu-id="af943-155">b.</span><span class="sxs-lookup"><span data-stu-id="af943-155">b.</span></span> <span data-ttu-id="af943-156">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="af943-156">Click **Finish**.</span></span>

   ![Страница "Импорт проектов"][CL08]

1. <span data-ttu-id="af943-158">При клонировании репозитория hello можно увидеть все файлы hello, перечисленные в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Локальный репозиторий][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="af943-160">Создание проекта Maven из локального репозитория</span><span class="sxs-lookup"><span data-stu-id="af943-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="af943-161">репозиторий Hello Spring загрузки Docker содержит завершенный проект Maven, который будет использоваться для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="af943-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="af943-162">Последовательно выберите **Файл** > **Импортировать**.</span><span class="sxs-lookup"><span data-stu-id="af943-162">Click **File** > **Import**.</span></span>

   ![Команда «Импорт» в меню файл hello][CL01]

1. <span data-ttu-id="af943-164">Здравствуйте, когда **импорта** откроется диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="af943-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="af943-165">а.</span><span class="sxs-lookup"><span data-stu-id="af943-165">a.</span></span> <span data-ttu-id="af943-166">Разверните элемент **Maven**.</span><span class="sxs-lookup"><span data-stu-id="af943-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="af943-167">b.</span><span class="sxs-lookup"><span data-stu-id="af943-167">b.</span></span> <span data-ttu-id="af943-168">Выберите **Existing Maven Projects** (Существующие проекты Maven).</span><span class="sxs-lookup"><span data-stu-id="af943-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="af943-169">c.</span><span class="sxs-lookup"><span data-stu-id="af943-169">c.</span></span> <span data-ttu-id="af943-170">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="af943-170">Click **Next**.</span></span>

   ![Диалоговое окно "Import" (Импорт)][MV01]

1. <span data-ttu-id="af943-172">На hello **проекты Maven** страницы:</span><span class="sxs-lookup"><span data-stu-id="af943-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="af943-173">а.</span><span class="sxs-lookup"><span data-stu-id="af943-173">a.</span></span> <span data-ttu-id="af943-174">Для **корневой каталог**, укажите hello **завершения** папки в ваш локальный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="af943-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="af943-175">b.</span><span class="sxs-lookup"><span data-stu-id="af943-175">b.</span></span> <span data-ttu-id="af943-176">Разверните hello **Дополнительно** раздела и введите имя файла для **шаблона имени**.</span><span class="sxs-lookup"><span data-stu-id="af943-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="af943-177">c.</span><span class="sxs-lookup"><span data-stu-id="af943-177">c.</span></span> <span data-ttu-id="af943-178">Поле выберите hello hello **pom.xml** файл в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="af943-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="af943-179">d.</span><span class="sxs-lookup"><span data-stu-id="af943-179">d.</span></span> <span data-ttu-id="af943-180">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="af943-180">Click **Finish**.</span></span>

   ![Страница "Проекты Maven"][MV02]

1. <span data-ttu-id="af943-182">При открытии проекта Maven hello появится второй проект, перечисленные в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Локальный проект Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="af943-184">Построение приложения Spring Boot с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="af943-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="af943-185">Выберите проект Maven hello в hello обозревателя проектов Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="af943-186">Последовательно выберите **Запуск** > **Запуск от имени** > **Сборка Maven**.</span><span class="sxs-lookup"><span data-stu-id="af943-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Команды toorun как сборки Maven][BU01]

1. <span data-ttu-id="af943-188">Если приложение успешно создано, hello окна консоли отображается состояние hello.</span><span class="sxs-lookup"><span data-stu-id="af943-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Успешное выполнение сборки Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="af943-190">Публикация вашего tooAzure web app с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="af943-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="af943-191">Выберите проект Maven hello в hello обозревателя проектов Eclipse.</span><span class="sxs-lookup"><span data-stu-id="af943-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="af943-192">Нажмите кнопку hello Azure **публикации** меню, а затем нажмите **опубликовать как контейнер Docker**.</span><span class="sxs-lookup"><span data-stu-id="af943-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Команда публикации в виде контейнера Docker][PU01]

1. <span data-ttu-id="af943-194">Здравствуйте, когда **развертывание контейнера Docker в Azure** откроется диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="af943-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="af943-195">а.</span><span class="sxs-lookup"><span data-stu-id="af943-195">a.</span></span> <span data-ttu-id="af943-196">Введите пользовательское имя образа Docker.</span><span class="sxs-lookup"><span data-stu-id="af943-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="af943-197">b.</span><span class="sxs-lookup"><span data-stu-id="af943-197">b.</span></span> <span data-ttu-id="af943-198">Для **toodeploy артефакта**, укажите путь toohello hello **gs spring загрузки docker-0.1.0.jar** только что созданного файла.</span><span class="sxs-lookup"><span data-stu-id="af943-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Задание параметров Docker][PU02]

   <span data-ttu-id="af943-200">Отобразятся все существующие узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="af943-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="af943-201">Если выбрать существующий узел tooan toodeploy toostep 5 можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="af943-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="af943-202">В противном случае используйте следующие шаги toocreate узел hello:</span><span class="sxs-lookup"><span data-stu-id="af943-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="af943-203">а.</span><span class="sxs-lookup"><span data-stu-id="af943-203">a.</span></span> <span data-ttu-id="af943-204">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="af943-204">Click **Add**.</span></span>

      ![Добавление нового узла Docker][PU03]

   <span data-ttu-id="af943-206">b.</span><span class="sxs-lookup"><span data-stu-id="af943-206">b.</span></span> <span data-ttu-id="af943-207">Здравствуйте, когда **создать узел Docker** откроется диалоговое окно, можно выбрать значения по умолчанию hello tooaccept или можно задать пользовательские параметры для нового узла Docker.</span><span class="sxs-lookup"><span data-stu-id="af943-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="af943-208">(Подробное описание hello различные параметры в разделе [публикации веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Далее** после указания toouse какие параметры.</span><span class="sxs-lookup"><span data-stu-id="af943-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Задание параметров узла Docker][PU04]

   <span data-ttu-id="af943-210">c.</span><span class="sxs-lookup"><span data-stu-id="af943-210">c.</span></span> <span data-ttu-id="af943-211">Можно выбрать существующие учетные данные входа toouse хранилище ключей Azure или для выбора tooenter новые учетные данные входа Docker.</span><span class="sxs-lookup"><span data-stu-id="af943-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="af943-212">После задания параметров нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="af943-212">Click **Finish** when you have specified your options.</span></span>

      ![Задание учетных данных узла Docker][PU05]

1. <span data-ttu-id="af943-214">Выберите узел Docker и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="af943-214">Select your Docker host, and then click **Next**.</span></span>

   ![Выберите toouse узла Docker][PU06]

1. <span data-ttu-id="af943-216">На последней странице hello hello **развертывание контейнера Docker в Azure** диалоговом окне укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="af943-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="af943-217">а.</span><span class="sxs-lookup"><span data-stu-id="af943-217">a.</span></span> <span data-ttu-id="af943-218">Вы можете toospecify пользовательское имя для hello контейнер, который будет содержать контейнер Docker, либо может принимать по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="af943-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="af943-219">b.</span><span class="sxs-lookup"><span data-stu-id="af943-219">b.</span></span> <span data-ttu-id="af943-220">Введите hello TCP-портов для узла docker с помощью hello, используя синтаксис: *[внешний порт]*:*[внутренний порт]*.</span><span class="sxs-lookup"><span data-stu-id="af943-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="af943-221">Например **80:8080** указывает внешний порт 80 и hello по умолчанию внутренние загрузки Spring порт 8080.</span><span class="sxs-lookup"><span data-stu-id="af943-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="af943-222">После настройки вашей внутренний порт (например, путем редактирования файла application.yml hello) для правильного маршрутизации toooccur hello в Azure необходимо номер порта toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="af943-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="af943-223">c.</span><span class="sxs-lookup"><span data-stu-id="af943-223">c.</span></span> <span data-ttu-id="af943-224">После настройки этих параметров щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="af943-224">After you configure these options, click **Finish**.</span></span>

   ![Развертывание контейнера Docker в Azure][PU07]

1. <span data-ttu-id="af943-226">После завершения публикации hello Azure Toolkit hello отображается журнал действий Azure **опубликовано** статуса hello.</span><span class="sxs-lookup"><span data-stu-id="af943-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Успешно развернутый узел Docker][PU08]

## <a name="next-steps"></a><span data-ttu-id="af943-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af943-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
