---
title: "aaaDeploy tooAzure службы приложений с помощью подключаемого модуля Jenkins | Документы Microsoft"
description: "Узнайте, как toouse Jenkins службы приложения Azure toodeploy Java для подключаемого модуля веб-приложения tooAzure в Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="e4c65-103">Развертывание tooAzure службы приложений с помощью подключаемого модуля Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="e4c65-104">toodeploy tooAzure Java web app, можно использовать Azure CLI в [конвейера Jenkins](/azure/jenkins/execute-cli-jenkins-pipeline) либо можно использовать hello [подключаемый модуль Azure приложение службы Jenkins](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="e4c65-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="e4c65-105">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="e4c65-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4c65-106">Настройка tooAzure toodeploy Jenkins службы приложений по протоколу FTP</span><span class="sxs-lookup"><span data-stu-id="e4c65-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="e4c65-107">Настройка tooAzure toodeploy Jenkins службы приложений на платформе Linux через Docker</span><span class="sxs-lookup"><span data-stu-id="e4c65-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="e4c65-108">Создание и настройка экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="e4c65-109">Если главный Jenkins еще нет начните с hello [шаблон решения](install-jenkins-solution-template.md), включая JDK8 и hello следующие необходимые подключаемые модули:</span><span class="sxs-lookup"><span data-stu-id="e4c65-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="e4c65-110">[подключаемый модуль Jenkins клиента Git](https://plugins.jenkins.io/git-client) версии 2.4.6;</span><span class="sxs-lookup"><span data-stu-id="e4c65-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="e4c65-111">[подключаемый модуль Docker Commons](https://plugins.jenkins.io/docker-commons) версии 1.4.0;</span><span class="sxs-lookup"><span data-stu-id="e4c65-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="e4c65-112">[учетные данные Azure](https://plugins.jenkins.io/azure-credentials) версии 1.2;</span><span class="sxs-lookup"><span data-stu-id="e4c65-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="e4c65-113">[служба приложений Azure](https://plugins.jenkins.io/azure-app-server) версии 0.1.</span><span class="sxs-lookup"><span data-stu-id="e4c65-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="e4c65-114">Можно использовать hello toodeploy службы приложения подключаемого модуля веб-приложения на всех языках (например, C#, PHP, Java и node.js и т.д.), поддерживаемых службой приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="e4c65-115">В этом учебнике мы используем hello пример приложения Java, [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="e4c65-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="e4c65-116">toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="e4c65-117">Для построения проекта Java hello требуются Java JDK и Maven.</span><span class="sxs-lookup"><span data-stu-id="e4c65-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="e4c65-118">Убедитесь, что компоненты hello в образец hello Jenkins или hello агент виртуальной Машины при использовании одного непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="e4c65-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="e4c65-119">tooinstall, войдите в экземпляре toohello Jenkins, с помощью SSH и запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e4c65-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="e4c65-120">Для развертывания tooApp службы в Linux, необходимо также tooinstall Docker в образец Jenkins hello или hello агента виртуальной Машины, используемого для построения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="e4c65-121">См. в статье toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="e4c65-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="e4c65-122">Добавление учетных данных участника tooJenkins службы Azure</span><span class="sxs-lookup"><span data-stu-id="e4c65-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="e4c65-123">Участник службы Azure является необходимые toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="e4c65-124">Используйте [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) или [портал Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate участника-службы Azure</span><span class="sxs-lookup"><span data-stu-id="e4c65-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="e4c65-125">Панели мониторинга Jenkins hello, нажмите кнопку **учетные данные -> Система ->**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="e4c65-126">Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).</span><span class="sxs-lookup"><span data-stu-id="e4c65-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="e4c65-127">Нажмите кнопку **добавить учетные данные** tooadd субъекта-службы Microsoft Azure, заполнив hello идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="e4c65-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="e4c65-128">Укажите идентификатор, **mySp**, который будет использоваться в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="e4c65-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="e4c65-129">Подключаемый модуль службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e4c65-129">Azure App Service plugin</span></span>

<span data-ttu-id="e4c65-130">V1.0 подключаемый модуль Azure службы приложений поддерживает tooAzure непрерывного развертывания веб-приложения через:</span><span class="sxs-lookup"><span data-stu-id="e4c65-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="e4c65-131">Git и FTP;</span><span class="sxs-lookup"><span data-stu-id="e4c65-131">Git and FTP</span></span>
* <span data-ttu-id="e4c65-132">Docker для веб-приложения в Linux.</span><span class="sxs-lookup"><span data-stu-id="e4c65-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="e4c65-133">Настройка Jenkins toodeploy веб-приложения по протоколу FTP, с помощью панели мониторинга hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="e4c65-134">toodeploy tooAzure вашего проекта веб-приложения можно отправить на артефактов сборки (например, файл .war в Java) с использованием Git или FTP.</span><span class="sxs-lookup"><span data-stu-id="e4c65-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="e4c65-135">Перед настройкой задания hello в Jenkins, требуется план службы приложений Azure и веб-приложения для запущенного приложения Java hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="e4c65-136">Создать план службы приложений Azure с hello **FREE** ценовой категории с помощью hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команду CLI.</span><span class="sxs-lookup"><span data-stu-id="e4c65-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="e4c65-137">план служб приложений Hello определяет toohost hello физические ресурсы, используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="e4c65-138">Все приложения, назначенный tooan план служб приложений используют эти ресурсы, позволяя toosave затрат при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="e4c65-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="e4c65-139">Создайте веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e4c65-139">Create a Web App.</span></span> <span data-ttu-id="e4c65-140">Можно либо использовать hello [портал Azure](/azure/app-service-web/web-sites-configure) или hello используйте следующую команду Az CLI:</span><span class="sxs-lookup"><span data-stu-id="e4c65-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="e4c65-141">Убедитесь, что настройка конфигурации среды выполнения Java hello, необходимый вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="e4c65-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="e4c65-142">следующую команду Azure CLI Hello настраивает hello web app toorun на последние Java JDK 8 и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="e4c65-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="e4c65-143">Настройка задания hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="e4c65-144">Создайте **универсальный** проект на панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e4c65-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="e4c65-145">Настройка **управление исходным кодом** toouse локального ветвления [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) , предоставляя hello **URL-адрес репозитория**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="e4c65-146">Например: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="e4c65-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="e4c65-147">Добавьте проект hello toobuild шаг построения, с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="e4c65-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="e4c65-148">Для этого добавьте **оболочку выполнения**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="e4c65-149">В этом примере мы должны hello *.war дополнительный шаг toorename файл в целевой папке tooROOT.war.</span><span class="sxs-lookup"><span data-stu-id="e4c65-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="e4c65-150">Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).</span><span class="sxs-lookup"><span data-stu-id="e4c65-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="e4c65-151">Питания, «mySp», участника службы Azure hello, хранящихся в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="e4c65-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="e4c65-152">В **Конфигурация приложения** выберите группу и веб-приложение hello ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="e4c65-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="e4c65-153">Hello подключаемого модуля автоматически определяет, является ли hello веб-приложения Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="e4c65-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="e4c65-154">Для веб-приложения на основе Windows представлен hello параметр «Опубликовать файлы».</span><span class="sxs-lookup"><span data-stu-id="e4c65-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="e4c65-155">Заливка в файлах hello требуется toodeploy (например, war пакет, если вы используете Java.) Исходный и целевой каталоги являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="e4c65-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="e4c65-156">Параметры Hello разрешить toospecify исходной и конечной папки при отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="e4c65-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="e4c65-157">Веб-приложение Java в Azure выполняется на сервере Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e4c65-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="e4c65-158">Поэтому пакет в формате WAR передается в папку веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="e4c65-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="e4c65-159">В этом примере значение **исходный каталог** слишком «target» и ввести «веб-приложений» **целевой каталог**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="e4c65-160">Следует toodeploy tooa слот, отличные от производственной можно также задать **слот** имя.</span><span class="sxs-lookup"><span data-stu-id="e4c65-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="e4c65-161">Сохраните проект hello и постройте его.</span><span class="sxs-lookup"><span data-stu-id="e4c65-161">Save hello project and build it.</span></span> <span data-ttu-id="e4c65-162">Веб-приложения — развернутой tooAzure после завершения построения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="e4c65-163">Развертывание веб-приложения по протоколу FTP с помощью конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="e4c65-164">Подключаемый модуль Hello — готовых конвейера.</span><span class="sxs-lookup"><span data-stu-id="e4c65-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="e4c65-165">Можно обратиться пример tooa в репозитории GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="e4c65-166">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="e4c65-167">Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке 11 и 12 соответственно.</span><span class="sxs-lookup"><span data-stu-id="e4c65-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="e4c65-168">Измените идентификатор учетных данных 14 tooupdate строки в вашем экземпляре Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e4c65-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="e4c65-169">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="e4c65-170">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="e4c65-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="e4c65-171">Укажите имя для задания hello и выберите **конвейера**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="e4c65-172">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-172">Click **OK**.</span></span>
3. <span data-ttu-id="e4c65-173">Нажмите кнопку hello **конвейера** вкладке рядом.</span><span class="sxs-lookup"><span data-stu-id="e4c65-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="e4c65-174">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="e4c65-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="e4c65-175">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="e4c65-176">Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:&lt;репозиторию разветвленного > .git</span><span class="sxs-lookup"><span data-stu-id="e4c65-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="e4c65-177">Обновление **путь к скрипту** слишком «Jenkinsfile_ftp_plugin»</span><span class="sxs-lookup"><span data-stu-id="e4c65-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="e4c65-178">Нажмите кнопку **Сохранить** и hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="e4c65-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="e4c65-179">Настройка Jenkins toodeploy веб-приложения на платформе Linux через Docker</span><span class="sxs-lookup"><span data-stu-id="e4c65-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="e4c65-180">Помимо Git и FTP веб-приложение в Linux поддерживает развертывания с помощью Docker.</span><span class="sxs-lookup"><span data-stu-id="e4c65-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="e4c65-181">с помощью Docker, toodeploy необходимо tooprovide Dockerfile, которая упаковывает веб-приложения в среде выполнения службы в docker изображение.</span><span class="sxs-lookup"><span data-stu-id="e4c65-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="e4c65-182">Затем подключаемый модуль hello построения образа hello, отправляющий ее tooa реестра docker и развертывает hello изображения tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="e4c65-183">Веб-приложения на платформе Linux также поддерживают традиционные способы, такие как Git и FTP, но только для встроенных языков (.NET Core, Node.js, PHP и Ruby).</span><span class="sxs-lookup"><span data-stu-id="e4c65-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="e4c65-184">Для других языков требуется toopackage выполнения кода и службы приложения вместе с помощью образа docker и использовать docker toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e4c65-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="e4c65-185">Перед настройкой задания hello в Jenkins, необходимо в качестве службы приложения Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="e4c65-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="e4c65-186">Реестр контейнера также необходимые toostore и управление образами закрытый контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="e4c65-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="e4c65-187">Вы можете использовать DockerHub. В этом примере используется реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="e4c65-188">Выполните действия hello [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate веб-приложения в Linux</span><span class="sxs-lookup"><span data-stu-id="e4c65-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="e4c65-189">Azure реестр контейнера является управляемый [Docker реестра] службы (https://docs.docker.com/registry/) на основании hello 2.0 реестра Docker открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="e4c65-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="e4c65-190">Выполните действия hello [здесь] (/ azure/container-registry/container-registry-get-started-azure-cli) Дополнительные рекомендации о том, как toodo так.</span><span class="sxs-lookup"><span data-stu-id="e4c65-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="e4c65-191">Кроме того, можно использовать DockerHub.</span><span class="sxs-lookup"><span data-stu-id="e4c65-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="e4c65-192">с помощью docker toodeploy:</span><span class="sxs-lookup"><span data-stu-id="e4c65-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="e4c65-193">Создайте универсальный проект на панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e4c65-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="e4c65-194">Настройка **управление исходным кодом** toouse локального ветвления [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) , предоставляя hello **URL-адрес репозитория**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="e4c65-195">Например: http://github.com/&lt;yourid>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="e4c65-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="e4c65-196">Добавьте проект hello toobuild шаг построения, с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="e4c65-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="e4c65-197">Сделать, добавив **выполнение оболочки** и добавить следующие строки в hello **команды**:</span><span class="sxs-lookup"><span data-stu-id="e4c65-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="e4c65-198">Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).</span><span class="sxs-lookup"><span data-stu-id="e4c65-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="e4c65-199">Укажите, **mySp**, хранящихся в предыдущем шаге, учетные данные Azure участника службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="e4c65-200">В **Конфигурация приложения** выберите группу ресурсов hello и веб-приложения Linux в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="e4c65-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="e4c65-201">Выберите публикацию через Docker.</span><span class="sxs-lookup"><span data-stu-id="e4c65-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="e4c65-202">Заполните путь **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="e4c65-203">Можно сохранить по умолчанию hello «/ Dockerfile» для **URL-адрес реестра Docker**указывайте в формате https:// hello&lt;myRegistry >. azurecr.io при использовании реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="e4c65-204">Не указывайте его при использовании DockerHub.</span><span class="sxs-lookup"><span data-stu-id="e4c65-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="e4c65-205">Для **учетные данные реестра**, добавьте hello учетные данные для hello реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="e4c65-206">Hello идентификатор пользователя и пароль можно получить, выполнив следующие команды в Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="e4c65-207">Первая команда Hello включает hello учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="e4c65-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="e4c65-208">Здравствуйте, имя образа docker и тег в **Дополнительно** вкладке являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="e4c65-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="e4c65-209">По умолчанию имя образа получается из образа hello имя, указанное в теге hello Azure портала (в контейнер Docker параметр.) создается на основе $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="e4c65-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="e4c65-210">Убедитесь в том, укажите имя образа hello либо портале Azure или задать значение для **образа Docker** в **Дополнительно** вкладки. В этом примере укажите &lt;yourRegistry >.azurecr.io/calculator в качестве значения для **образа Docker** и не указывайте **тег образа Docker**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="e4c65-211">Примечание. Развертывание завершается сбоем, если использовать параметр встроенного образа Docker.</span><span class="sxs-lookup"><span data-stu-id="e4c65-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="e4c65-212">Убедитесь, что изменение docker config toouse настраиваемого изображения в контейнер Docker параметр на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e4c65-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="e4c65-213">Для встроенного изображения используется toodeploy подход передачи файла.</span><span class="sxs-lookup"><span data-stu-id="e4c65-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="e4c65-214">Аналогичный подход toofile передачи, можно выбрать другой слот, отличные от рабочей.</span><span class="sxs-lookup"><span data-stu-id="e4c65-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="e4c65-215">Сохраните и постройте проект hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-215">Save and build hello project.</span></span> <span data-ttu-id="e4c65-216">Вы увидите образ контейнера помещается tooyour реестра и развернуть веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="e4c65-217">Развертывание приложения на платформе Linux через Docker с помощью конвейера Jenkins tooWeb</span><span class="sxs-lookup"><span data-stu-id="e4c65-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="e4c65-218">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="e4c65-219">Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке 11 и 12 соответственно.</span><span class="sxs-lookup"><span data-stu-id="e4c65-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="e4c65-220">Изменение строки 13 tooyour контейнер реестра сервера</span><span class="sxs-lookup"><span data-stu-id="e4c65-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="e4c65-221">Измените идентификатор учетных данных 16 tooupdate строки в вашем экземпляре Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="e4c65-222">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="e4c65-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="e4c65-223">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="e4c65-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="e4c65-224">Укажите имя для задания hello и выберите **конвейера**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="e4c65-225">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-225">Click **OK**.</span></span>
3. <span data-ttu-id="e4c65-226">Нажмите кнопку hello **конвейера** вкладке рядом.</span><span class="sxs-lookup"><span data-stu-id="e4c65-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="e4c65-227">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="e4c65-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="e4c65-228">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="e4c65-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="e4c65-229">Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:&lt;репозиторию разветвленного > .git</span><span class="sxs-lookup"><span data-stu-id="e4c65-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="e4c65-230">Обновление 7, **путь к скрипту** слишком «Jenkinsfile_container_plugin»</span><span class="sxs-lookup"><span data-stu-id="e4c65-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="e4c65-231">Нажмите кнопку **Сохранить** и hello выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="e4c65-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="e4c65-232">Проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e4c65-232">Verify your web app</span></span>

1. <span data-ttu-id="e4c65-233">tooverify hello WAR-файл успешно развернут tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e4c65-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="e4c65-234">Откройте веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="e4c65-234">Open a web browser.</span></span>
2. <span data-ttu-id="e4c65-235">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping отображается:</span><span class="sxs-lookup"><span data-stu-id="e4c65-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="e4c65-236">Вас приветствует tooJava веб-приложения!!!</span><span class="sxs-lookup"><span data-stu-id="e4c65-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="e4c65-237">Это обновленная версия!</span><span class="sxs-lookup"><span data-stu-id="e4c65-237">This is updated!</span></span>
   <span data-ttu-id="e4c65-238">17 июня, воскресенье, 16:39:10 UTC, 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e4c65-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="e4c65-239">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y</span><span class="sxs-lookup"><span data-stu-id="e4c65-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="e4c65-241">Для службы приложений под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="e4c65-241">For App service on Linux</span></span>

* <span data-ttu-id="e4c65-242">tooverify, в Azure CLI, выполните:</span><span class="sxs-lookup"><span data-stu-id="e4c65-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="e4c65-243">Вы получаете hello следующий результат:</span><span class="sxs-lookup"><span data-stu-id="e4c65-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="e4c65-244">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="e4c65-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="e4c65-245">Отображается сообщение hello:</span><span class="sxs-lookup"><span data-stu-id="e4c65-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="e4c65-246">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y</span><span class="sxs-lookup"><span data-stu-id="e4c65-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="e4c65-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4c65-247">Next steps</span></span>

<span data-ttu-id="e4c65-248">В этом учебнике используется tooAzure toodeploy подключаемого модуля службы приложений Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e4c65-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="e4c65-249">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e4c65-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4c65-250">Настройка Jenkins toodeploy службе приложений Azure по протоколу FTP</span><span class="sxs-lookup"><span data-stu-id="e4c65-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="e4c65-251">Настройка tooAzure toodeploy Jenkins службы приложений на платформе Linux через Docker</span><span class="sxs-lookup"><span data-stu-id="e4c65-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
