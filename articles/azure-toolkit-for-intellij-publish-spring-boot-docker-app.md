---
title: "aaaPublish Spring загрузки приложения в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="ae1e4-103">Опубликовать приложение Spring загрузки как контейнер Docker с помощью hello Azure Toolkit для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ae1e4-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="ae1e4-104">Hello [Spring Framework] — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ae1e4-105">Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="ae1e4-106">[Docker] — это решение открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="ae1e4-107">Этот учебник поможет выполнить toodeploy действия hello приложение Spring загрузки как tooMicrosoft контейнера Docker Azure с помощью hello Azure Toolkit для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="ae1e4-108">Клонировать репозиторий Docker Spring загрузки по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="ae1e4-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="ae1e4-109">Hello следующие шаги описывают клонирования репозитория hello Spring загрузки Docker с помощью IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="ae1e4-110">Если toouse командной строки, см. [развернуть приложение в Linux в службе контейнера Azure Spring загрузки][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="ae1e4-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="ae1e4-111">Откройте IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="ae1e4-112">На экране приветствия hello выберите hello **GitHub** параметр в hello **извлечь из системы управления версиями** списка.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Параметр GitHub для управления версиями][CL01]

1. <span data-ttu-id="ae1e4-114">Введите свои учетные данные, если запрос toolog в.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="ae1e4-115">Если вы используете toolog имя пользователя и пароль в tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="ae1e4-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Диалоговое окно для ввода имени пользователя и пароля для входа в GitHub][CL02a]

   * <span data-ttu-id="ae1e4-117">При использовании маркера toolog в tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="ae1e4-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Диалоговое окно для ввода токена GitHub][CL02b]

1. <span data-ttu-id="ae1e4-119">Введите **https://github.com/spring-guides/gs-spring-boot-docker.git** URL-адрес репозитория hello, укажите локальный путь и сведения о папке и нажмите кнопку **клон**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Диалоговое окно "Clone Repository" (Клонирование репозитория)][CL03]

1. <span data-ttu-id="ae1e4-121">При запросе toocreate IntelliJ проекта, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Отклонение toocreate проекте IntelliJ][CL04]

1. <span data-ttu-id="ae1e4-123">На начальной странице приветствия нажмите кнопку **Импорт проекта**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-123">On hello welcome page, click **Import Project**.</span></span>

   ![Пункт "Импорт проекта"][CL05]

1. <span data-ttu-id="ae1e4-125">Найти путь hello, где клонирования репозитория загрузки Spring hello, выберите hello **завершения** папку в корневой hello, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Выбор папки для импорта][CL06]

1. <span data-ttu-id="ae1e4-127">При появлении запроса выберите **Создать проект из существующих источников**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Параметр toocreate проекта из существующих источников][CL07]

1. <span data-ttu-id="ae1e4-129">Укажите имя проекта или примите значение по умолчанию hello, проверьте hello правильный путь toohello **завершения** папки, а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Укажите имя проекта hello][CL08]

1. <span data-ttu-id="ae1e4-131">Настройте все каталоги для импорта и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Выбор каталогов][CL09]

1. <span data-ttu-id="ae1e4-133">Просмотрите tooimport hello библиотеки и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Просмотр библиотек проекта][CL10]

1. <span data-ttu-id="ae1e4-135">Просмотрите структуру модуля hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-135">Review hello module structure, and then click **Next**.</span></span>

   ![Просмотр структуры модулей][CL11]

1. <span data-ttu-id="ae1e4-137">Укажите свой JDK и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-137">Specify your JDK, and then click **Next**.</span></span>

   ![Указание JDK][CL12]

1. <span data-ttu-id="ae1e4-139">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="ae1e4-139">Click **Finish**.</span></span>

   ![Кнопка "Готово"][CL13]

<span data-ttu-id="ae1e4-141">IntelliJ импортирует приложение hello Spring загрузки как проект и отображает hello структуры после завершения импорта hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Приложение Spring Boot в IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="ae1e4-143">Создание приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ae1e4-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="ae1e4-144">Сборка приложения hello с помощью hello Maven POM</span><span class="sxs-lookup"><span data-stu-id="ae1e4-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="ae1e4-145">Если он еще не открыта, откройте окно инструментов Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="ae1e4-146">Последовательно выберите **Вид** > **Окна инструментов** > **Проекты Maven**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Окна инструментов и команды проектов Maven][BU01]

1. <span data-ttu-id="ae1e4-148">Щелкните правой кнопкой мыши в окне инструментов Maven hello, **пакета** и выберите **выполнить сборки Maven**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="ae1e4-149">(Если Maven проекта не отображается автоматически, нажмите кнопку hello **повторный импорт** значок на панели инструментов Maven hello.)</span><span class="sxs-lookup"><span data-stu-id="ae1e4-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Команда "Запуск сборки Maven"][BU02]

1. <span data-ttu-id="ae1e4-151">После успешного создания приложения Spring Boot IntelliJ отобразит сообщение **Сборка выполнена успешно**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Сообщение "Сборка выполнена успешно"][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="ae1e4-153">Создание готового к развертыванию артефакта</span><span class="sxs-lookup"><span data-stu-id="ae1e4-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="ae1e4-154">toopublish приложение Spring загрузки необходимо toocreate артефакта готовым к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="ae1e4-155">Используйте следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-155">Use hello following steps:</span></span>

1. <span data-ttu-id="ae1e4-156">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="ae1e4-157">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Команда "Project Structure" (Структура проекта)][ART01]

1. <span data-ttu-id="ae1e4-159">Щелкните зеленый плюс hello (**+**) символ tooadd артефакта, нажмите кнопку **JAR**и нажмите кнопку **пустой**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Добавление артефакта][ART02]

1. <span data-ttu-id="ae1e4-161">Имя вашего артефакта делая не tooadd hello расширение «.jar», а затем укажите hello целевую папку для вывода Maven приветствия.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Указание свойств артефакта][ART03]

1. <span data-ttu-id="ae1e4-163">Создайте манифест для артефакта (необязательно).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="ae1e4-164">а.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-164">a.</span></span> <span data-ttu-id="ae1e4-165">Нажмите кнопку **Create Manifest** (Создать манифест).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-165">Click **Create Manifest**.</span></span>

      ![Нажмите кнопку Создать манифест hello][ART04a]

   <span data-ttu-id="ae1e4-167">b.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-167">b.</span></span> <span data-ttu-id="ae1e4-168">Выберите путь по умолчанию hello для hello артефакта и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Указание пути к артефакту][ART04b]

   <span data-ttu-id="ae1e4-170">c.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-170">c.</span></span> <span data-ttu-id="ae1e4-171">Нажмите кнопку с многоточием hello (**...** ) toolocate hello основного класса.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Поиск основного (main) класса][ART04c]

   <span data-ttu-id="ae1e4-173">d.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-173">d.</span></span> <span data-ttu-id="ae1e4-174">Выберите основной класс и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-174">Choose your main class, and then click **OK**.</span></span>

      ![Указание основного (main) класса][ART04d]

1. <span data-ttu-id="ae1e4-176">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-176">Click **OK**.</span></span>

   ![Закройте диалоговое окно структуры проекта hello][ART05]

> [!NOTE]
> <span data-ttu-id="ae1e4-178">Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Настройка артефакты] на веб-сайте JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="ae1e4-179">Hello артефакт для развертывания сборки</span><span class="sxs-lookup"><span data-stu-id="ae1e4-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="ae1e4-180">Нажмите кнопку **Build** (Сборка), а затем кнопку **Artifacts** (Артефакты).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Команда "Build Artifacts" (Создать артефакты)][BU04]

1. <span data-ttu-id="ae1e4-182">Здравствуйте, когда **артефактов сборки** контекстное меню, нажмите кнопку **сборки**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Контекстное меню "Build Artifacts" (Создание артефакта)][BU05]

<span data-ttu-id="ae1e4-184">В окне инструментов проекта hello IntelliJ отображать артефакта hello завершения Spring загрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Созданный артефакт][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="ae1e4-186">Публикация вашего tooAzure web app с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="ae1e4-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="ae1e4-187">Если вы не вошли в tooyour учетная запись Azure, следуйте указаниям hello [входа в инструкции для hello Azure Toolkit для IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="ae1e4-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="ae1e4-188">В окне инструментов обозревателя проектов hello, щелкните правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как контейнер Docker**.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Команда публикации в виде контейнера Docker][PU01]

1. <span data-ttu-id="ae1e4-190">Здравствуйте, когда **развертывания контейнера Docker в Azure** откроется диалоговое окно, отображаются все существующие узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="ae1e4-191">Если выбрать существующий узел tooan toodeploy toostep 4 можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="ae1e4-192">В противном случае используйте следующие шаги toocreate узел hello:</span><span class="sxs-lookup"><span data-stu-id="ae1e4-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="ae1e4-193">а.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-193">a.</span></span> <span data-ttu-id="ae1e4-194">Щелкните зеленый плюс hello (**+**) символов.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-194">Click hello green plus (**+**) symbol.</span></span>

      ![Добавление нового узла Docker][PU02]

   <span data-ttu-id="ae1e4-196">b.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-196">b.</span></span> <span data-ttu-id="ae1e4-197">Здравствуйте, когда **создать узел Docker** откроется диалоговое окно, можно выбрать значения по умолчанию hello tooaccept или можно задать пользовательские параметры для нового узла Docker.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="ae1e4-198">(Подробное описание hello различные параметры в разделе [публикации веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Далее** после указания toouse какие параметры.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Задание параметров узла Docker][PU03a]

   <span data-ttu-id="ae1e4-200">c.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-200">c.</span></span> <span data-ttu-id="ae1e4-201">Можно выбрать существующие учетные данные входа toouse хранилище ключей Azure или для выбора tooenter новые учетные данные входа Docker.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="ae1e4-202">После задания параметров нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-202">Click **Finish** when you have specified your options.</span></span>

      ![Задание учетных данных узла Docker][PU03b]

1. <span data-ttu-id="ae1e4-204">Выберите узел Docker и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-204">Select your Docker host, and then click **Next**.</span></span>

   ![Выберите узел toouse hello Docker][PU04]

1. <span data-ttu-id="ae1e4-206">На последней странице hello hello **развертывания контейнера Docker в Azure** диалоговом окне укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ae1e4-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="ae1e4-207">а.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-207">a.</span></span> <span data-ttu-id="ae1e4-208">Вы можете toospecify пользовательское имя для hello контейнер, который будет содержать контейнер Docker, либо может принимать по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="ae1e4-209">b.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-209">b.</span></span> <span data-ttu-id="ae1e4-210">Введите hello TCP-портов для узла docker с помощью hello, используя синтаксис: *[внешний порт]*:*[внутренний порт]*.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="ae1e4-211">Например **80:8080** указывает внешний порт 80 и hello по умолчанию внутренние загрузки Spring порт 8080.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="ae1e4-212">После настройки вашей внутренний порт (например, путем редактирования файла application.yml hello) для правильного маршрутизации toooccur hello в Azure необходимо номер порта toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="ae1e4-213">c.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-213">c.</span></span> <span data-ttu-id="ae1e4-214">После настройки этих параметров щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="ae1e4-214">After you have configured these options, click **Finish**.</span></span>

   ![Развертывание контейнера Docker в Azure][PU05]

1. <span data-ttu-id="ae1e4-216">После завершения публикации hello Azure Toolkit hello отображается журнал действий Azure **опубликовано** статуса hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Успешно развернутый узел Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="ae1e4-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae1e4-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="ae1e4-219">. в разделе toolearn о дополнительных методов для создания загрузочного Spring приложений с помощью IntelliJ, [Создание проектов Spring загрузки](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) на веб-сайте JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="ae1e4-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Настройка артефакты]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
