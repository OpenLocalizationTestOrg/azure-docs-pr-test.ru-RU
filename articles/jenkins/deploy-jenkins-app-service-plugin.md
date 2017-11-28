---
title: "Развертывание в службе приложений Azure с помощью подключаемого модуля Jenkins | Документация Майкрософт"
description: "Узнайте, как развернуть веб-приложение Java в Azure в Jenkins с использованием подключаемого модуля Jenkins службы приложений Azure."
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
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="68ffe-103">Развертывание в службе приложений Azure с использованием подключаемого модуля Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="68ffe-104">Для развертывания веб-приложения Java в Azure можно использовать Azure CLI в [конвейере Jenkins](/azure/jenkins/execute-cli-jenkins-pipeline) или [подключаемый модуль Jenkins службы приложений Azure](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="68ffe-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="68ffe-105">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="68ffe-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68ffe-106">Настройка Jenkins для развертывания в службе приложений Azure по протоколу FTP</span><span class="sxs-lookup"><span data-stu-id="68ffe-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="68ffe-107">Настройка Jenkins для развертывания в службе приложений Azure в Linux с помощью Docker</span><span class="sxs-lookup"><span data-stu-id="68ffe-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="68ffe-108">Создание и настройка экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="68ffe-109">Если у вас нет главного экземпляра, воспользуйтесь [шаблоном решений](install-jenkins-solution-template.md), который содержит JDK8 и следующие необходимые подключаемые модули:</span><span class="sxs-lookup"><span data-stu-id="68ffe-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="68ffe-110">[подключаемый модуль Jenkins клиента Git](https://plugins.jenkins.io/git-client) версии 2.4.6;</span><span class="sxs-lookup"><span data-stu-id="68ffe-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="68ffe-111">[подключаемый модуль Docker Commons](https://plugins.jenkins.io/docker-commons) версии 1.4.0;</span><span class="sxs-lookup"><span data-stu-id="68ffe-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="68ffe-112">[учетные данные Azure](https://plugins.jenkins.io/azure-credentials) версии 1.2;</span><span class="sxs-lookup"><span data-stu-id="68ffe-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="68ffe-113">[служба приложений Azure](https://plugins.jenkins.io/azure-app-server) версии 0.1.</span><span class="sxs-lookup"><span data-stu-id="68ffe-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="68ffe-114">Подключаемый модуль службы приложений можно использовать для развертывания веб-приложения на всех языках (например, C#, PHP, Java и Node.js и т. д.), поддерживаемых службой приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="68ffe-115">В этом руководстве мы используем пример приложения Java, [простое веб-приложение Java для Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="68ffe-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="68ffe-116">Чтобы создать разветвление репозитория для своей учетной записи GitHub, нажмите кнопку **Fork** (Разветвление) в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="68ffe-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="68ffe-117">Для создания проекта Java требуются Java JDK и Maven.</span><span class="sxs-lookup"><span data-stu-id="68ffe-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="68ffe-118">Убедитесь, что установлены компоненты в главном узле Jenkins или агенте виртуальной машины при их использовании для обеспечения непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="68ffe-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="68ffe-119">Чтобы выполнить установку, войдите в экземпляр Jenkins с помощью SSH-подключения и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="68ffe-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="68ffe-120">Для развертывания в службе приложений на платформе Linux также необходимо установить Docker в главном экземпляре Jenkins или агенте виртуальной машины, используемом для сборки.</span><span class="sxs-lookup"><span data-stu-id="68ffe-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="68ffe-121">Сведения об установке Docker см. в этой статье: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="68ffe-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="68ffe-122">Добавление субъекта-службы Azure в учетные данные Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="68ffe-123">Для развертывания в Azure требуется субъект-служба Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="68ffe-124">Используйте [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) или [портал Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) для создания субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="68ffe-125">На панели мониторинга Jenkins выберите **Credentials -> System ->**(Учетные данные -> Система).</span><span class="sxs-lookup"><span data-stu-id="68ffe-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="68ffe-126">Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).</span><span class="sxs-lookup"><span data-stu-id="68ffe-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="68ffe-127">Щелкните **Add Credentials** (Добавить учетные данные), чтобы добавить субъект-службу Microsoft Azure путем ввода следующих значений: идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="68ffe-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="68ffe-128">Укажите идентификатор, **mySp**, который будет использоваться в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="68ffe-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="68ffe-129">Подключаемый модуль службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="68ffe-129">Azure App Service plugin</span></span>

<span data-ttu-id="68ffe-130">Подключаемый модуль службы приложений Azure версии 1.0 поддерживает непрерывное развертывание в веб-приложение Azure через:</span><span class="sxs-lookup"><span data-stu-id="68ffe-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="68ffe-131">Git и FTP;</span><span class="sxs-lookup"><span data-stu-id="68ffe-131">Git and FTP</span></span>
* <span data-ttu-id="68ffe-132">Docker для веб-приложения в Linux.</span><span class="sxs-lookup"><span data-stu-id="68ffe-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="68ffe-133">Настройка Jenkins для развертывания веб-приложения по протоколу FTP с помощью панели мониторинга Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="68ffe-134">Чтобы развернуть проект в веб-приложении Azure, можно отправить артефакты сборки (например, WAR-файл на Java) с использованием Git или FTP.</span><span class="sxs-lookup"><span data-stu-id="68ffe-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="68ffe-135">Перед настройкой задания в Jenkins требуется план службы приложений Azure и веб-приложение для запуска приложения Java.</span><span class="sxs-lookup"><span data-stu-id="68ffe-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="68ffe-136">Создайте план службы приложений Azure с ценовой категорией **Бесплатный** с помощью команды CLI [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="68ffe-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="68ffe-137">От плана службы приложений зависят физические ресурсы, используемые для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="68ffe-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="68ffe-138">Все приложения, назначенные плану службы приложений, совместно используют ресурсы, которые позволяют сэкономить при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="68ffe-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="68ffe-139">Создайте веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="68ffe-139">Create a Web App.</span></span> <span data-ttu-id="68ffe-140">Воспользуйтесь [порталом Azure](/azure/app-service-web/web-sites-configure) или следующей командой az интерфейса командной строки:</span><span class="sxs-lookup"><span data-stu-id="68ffe-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="68ffe-141">Настройте конфигурацию среды выполнения Java, необходимую вашему приложению.</span><span class="sxs-lookup"><span data-stu-id="68ffe-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="68ffe-142">Следующая команда Azure CLI настраивает веб-приложение для запуска в Java 8 JDK и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="68ffe-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="68ffe-143">Настройка задания Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="68ffe-144">Создайте **универсальный** проект на панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="68ffe-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="68ffe-145">Настройте **управление исходным кодом** для использования локальной вилки [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample), указав **URL-адрес репозитория**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="68ffe-146">Например: http://github.com/&lt;yourID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="68ffe-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="68ffe-147">Добавьте шаг сборки для создания проекта с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="68ffe-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="68ffe-148">Для этого добавьте **оболочку выполнения**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="68ffe-149">В этом примере требуется дополнительный шаг для переименования WAR-файла в целевой папке на ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="68ffe-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="68ffe-150">Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).</span><span class="sxs-lookup"><span data-stu-id="68ffe-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="68ffe-151">Укажите mySp, субъект-службу Azure, которую мы сохранили на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="68ffe-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="68ffe-152">В разделе **Конфигурация приложения** выберите группу ресурсов и веб-приложение в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="68ffe-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="68ffe-153">Подключаемый модуль автоматически определяет платформу веб-приложения (Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="68ffe-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="68ffe-154">Для веб-приложения на базе Windows появляется параметр Publish Files (Публикация файлов).</span><span class="sxs-lookup"><span data-stu-id="68ffe-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="68ffe-155">Заполните файлы, которые нужно развернуть (например, пакет в формате WAR, если вы используете Java). Исходный и целевой каталоги являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="68ffe-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="68ffe-156">Эти параметры позволяют указать исходную и целевую папки при отправке файлов.</span><span class="sxs-lookup"><span data-stu-id="68ffe-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="68ffe-157">Веб-приложение Java в Azure выполняется на сервере Tomcat.</span><span class="sxs-lookup"><span data-stu-id="68ffe-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="68ffe-158">Поэтому пакет в формате WAR передается в папку веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="68ffe-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="68ffe-159">В этом примере задайте для **исходного каталога** значение target, а для **целевого каталога** — webapps.</span><span class="sxs-lookup"><span data-stu-id="68ffe-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="68ffe-160">Если вы хотите выполнить развертывание в слот, отличный от рабочего, можно также задать имя **слота**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="68ffe-161">Сохраните проект и создайте его.</span><span class="sxs-lookup"><span data-stu-id="68ffe-161">Save the project and build it.</span></span> <span data-ttu-id="68ffe-162">Веб-приложение развертывается в Azure после сборки.</span><span class="sxs-lookup"><span data-stu-id="68ffe-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="68ffe-163">Развертывание веб-приложения по протоколу FTP с помощью конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="68ffe-164">Подключаемый модуль готов к использованию в конвейере.</span><span class="sxs-lookup"><span data-stu-id="68ffe-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="68ffe-165">Пример доступен в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="68ffe-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="68ffe-166">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="68ffe-167">Щелкните значок с изображением карандаша, чтобы изменить этот файл для обновления группы ресурсов и имени веб-приложения в строках 11 и 12, соответственно.</span><span class="sxs-lookup"><span data-stu-id="68ffe-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="68ffe-168">Измените строку 14 для обновления идентификатора учетных данных в вашем экземпляре Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="68ffe-169">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="68ffe-170">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="68ffe-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="68ffe-171">Укажите имя задания и выберите **Pipeline** (Конвейер).</span><span class="sxs-lookup"><span data-stu-id="68ffe-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="68ffe-172">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-172">Click **OK**.</span></span>
3. <span data-ttu-id="68ffe-173">Откройте вкладку **Pipeline** (Конвейер), находящуюся рядом.</span><span class="sxs-lookup"><span data-stu-id="68ffe-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="68ffe-174">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="68ffe-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="68ffe-175">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="68ffe-176">Введите URL-адрес GitHub для разветвленного репозитория: https:&lt;разветвленный репозиторий>.git</span><span class="sxs-lookup"><span data-stu-id="68ffe-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="68ffe-177">Измените **путь к сценарию** на Jenkinsfile_ftp_plugin.</span><span class="sxs-lookup"><span data-stu-id="68ffe-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="68ffe-178">Нажмите кнопку **Сохранить** и запустите задание.</span><span class="sxs-lookup"><span data-stu-id="68ffe-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="68ffe-179">Настройка Jenkins для развертывания веб-приложения на платформе Linux с помощью Docker</span><span class="sxs-lookup"><span data-stu-id="68ffe-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="68ffe-180">Помимо Git и FTP веб-приложение в Linux поддерживает развертывания с помощью Docker.</span><span class="sxs-lookup"><span data-stu-id="68ffe-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="68ffe-181">Чтобы выполнить развертывание с помощью Docker, необходимо предоставить файл Dockerfile, который упаковывает веб-приложение со службой среды выполнения в образ Docker.</span><span class="sxs-lookup"><span data-stu-id="68ffe-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="68ffe-182">Затем подключаемый модуль создаст образ, отправит его в реестр Docker и развернет в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="68ffe-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="68ffe-183">Веб-приложения на платформе Linux также поддерживают традиционные способы, такие как Git и FTP, но только для встроенных языков (.NET Core, Node.js, PHP и Ruby).</span><span class="sxs-lookup"><span data-stu-id="68ffe-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="68ffe-184">Для других языков необходимо объединить код приложения и среду выполнения службы в образ Docker и использовать Docker для развертывания.</span><span class="sxs-lookup"><span data-stu-id="68ffe-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="68ffe-185">Перед настройкой задания в Jenkins вам понадобится служба приложений Azure в Linux,</span><span class="sxs-lookup"><span data-stu-id="68ffe-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="68ffe-186">а также реестр контейнеров для хранения частных образов контейнера Docker и управления ими.</span><span class="sxs-lookup"><span data-stu-id="68ffe-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="68ffe-187">Вы можете использовать DockerHub. В этом примере используется реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="68ffe-188">Выполните действия, указанные [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app), для создания веб-приложения в Linux.</span><span class="sxs-lookup"><span data-stu-id="68ffe-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="68ffe-189">Реестр контейнеров Azure — это управляемая служба [реестра Docker] (https://docs.docker.com/registry/) на базе реестра Docker версии 2.0 с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="68ffe-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="68ffe-190">Дополнительные сведения об этом см. [здесь] (/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68ffe-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="68ffe-191">Кроме того, можно использовать DockerHub.</span><span class="sxs-lookup"><span data-stu-id="68ffe-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="68ffe-192">Развертывание с помощью Docker</span><span class="sxs-lookup"><span data-stu-id="68ffe-192">To deploy using docker:</span></span>

1. <span data-ttu-id="68ffe-193">Создайте универсальный проект на панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="68ffe-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="68ffe-194">Настройте **управление исходным кодом** для использования локальной вилки [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample), указав **URL-адрес репозитория**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="68ffe-195">Например: http://github.com/&lt;yourid>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="68ffe-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="68ffe-196">Добавьте шаг сборки для создания проекта с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="68ffe-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="68ffe-197">Для этого добавьте **оболочку выполнения** и следующую строку в разделе **Команда**:</span><span class="sxs-lookup"><span data-stu-id="68ffe-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="68ffe-198">Добавьте действие после сборки, выбрав **Publish an Azure Web App** (Публикация веб-приложения Azure).</span><span class="sxs-lookup"><span data-stu-id="68ffe-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="68ffe-199">Укажите **mySp**, субъект-службу Azure, которую мы сохранили на предыдущем шаге в качестве учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="68ffe-200">В разделе **Конфигурация приложения** выберите группу ресурсов и веб-приложение Linux в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="68ffe-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="68ffe-201">Выберите публикацию через Docker.</span><span class="sxs-lookup"><span data-stu-id="68ffe-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="68ffe-202">Заполните путь **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="68ffe-203">Вы можете сохранить значение по умолчанию /Dockerfile для **URL-адреса реестра Docker. При использовании реестра контейнеров Azure** укажите его в формате https://&lt;myRegistry >.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="68ffe-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="68ffe-204">Не указывайте его при использовании DockerHub.</span><span class="sxs-lookup"><span data-stu-id="68ffe-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="68ffe-205">Добавьте **учетные данные реестра** для реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="68ffe-206">Идентификатор пользователя и пароль можно получить, выполнив следующие команды в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="68ffe-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="68ffe-207">Первая команда включает учетную запись администратора.</span><span class="sxs-lookup"><span data-stu-id="68ffe-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="68ffe-208">Имя образа Docker и тег на вкладке **Дополнительно** являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="68ffe-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="68ffe-209">По умолчанию имя образа можно получить из имени образа, настроенного на портале Azure (в параметрах контейнера Docker). Тег создается на основе $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="68ffe-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="68ffe-210">Убедитесь, что имя образа задано на портале Azure, или задайте значение для **образа Docker** на вкладке **Дополнительно**. В этом примере укажите &lt;yourRegistry >.azurecr.io/calculator в качестве значения для **образа Docker** и не указывайте **тег образа Docker**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="68ffe-211">Примечание. Развертывание завершается сбоем, если использовать параметр встроенного образа Docker.</span><span class="sxs-lookup"><span data-stu-id="68ffe-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="68ffe-212">Обязательно настройте конфигурацию Docker для использования пользовательского образа в контейнере Docker на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="68ffe-213">Для развертывания встроенного изображения используйте подход с передачей файла.</span><span class="sxs-lookup"><span data-stu-id="68ffe-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="68ffe-214">Кроме того, можно выбрать слот, отличный от рабочего. Этот способ аналогичный способу передачи файла.</span><span class="sxs-lookup"><span data-stu-id="68ffe-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="68ffe-215">Сохраните и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="68ffe-215">Save and build the project.</span></span> <span data-ttu-id="68ffe-216">После этого образ контейнера помещается в реестр, а веб-приложение развертывается.</span><span class="sxs-lookup"><span data-stu-id="68ffe-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="68ffe-217">Развертывание в веб-приложении на платформе Linux с помощью Docker с использованием конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="68ffe-218">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="68ffe-219">Щелкните значок с изображением карандаша, чтобы изменить этот файл для обновления группы ресурсов и имени веб-приложения в строках 11 и 12, соответственно.</span><span class="sxs-lookup"><span data-stu-id="68ffe-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="68ffe-220">Измените строку 13 на сервер контейнера реестра.</span><span class="sxs-lookup"><span data-stu-id="68ffe-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="68ffe-221">Измените строку 16 для обновления идентификатора учетных данных в своем экземпляре Jenkins.</span><span class="sxs-lookup"><span data-stu-id="68ffe-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="68ffe-222">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="68ffe-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="68ffe-223">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="68ffe-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="68ffe-224">Укажите имя задания и выберите **Pipeline** (Конвейер).</span><span class="sxs-lookup"><span data-stu-id="68ffe-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="68ffe-225">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-225">Click **OK**.</span></span>
3. <span data-ttu-id="68ffe-226">Откройте вкладку **Pipeline** (Конвейер), находящуюся рядом.</span><span class="sxs-lookup"><span data-stu-id="68ffe-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="68ffe-227">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="68ffe-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="68ffe-228">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="68ffe-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="68ffe-229">Введите URL-адрес GitHub для разветвленного репозитория: https:&lt;разветвленный репозиторий>.git</span><span class="sxs-lookup"><span data-stu-id="68ffe-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="68ffe-230">Измените **путь к сценарию** на Jenkinsfile_container_plugin.</span><span class="sxs-lookup"><span data-stu-id="68ffe-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="68ffe-231">Нажмите кнопку **Сохранить** и запустите задание.</span><span class="sxs-lookup"><span data-stu-id="68ffe-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="68ffe-232">Проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="68ffe-232">Verify your web app</span></span>

1. <span data-ttu-id="68ffe-233">Чтобы проверить успешное развертывание WAR-файла в веб-приложении:</span><span class="sxs-lookup"><span data-stu-id="68ffe-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="68ffe-234">Откройте веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="68ffe-234">Open a web browser.</span></span>
2. <span data-ttu-id="68ffe-235">Перейдите по адресу http://&lt;имя_приложения>.azurewebsites.net/api/calculator/ping. Отобразится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="68ffe-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="68ffe-236">Добро пожаловать в веб-приложение Java!!!</span><span class="sxs-lookup"><span data-stu-id="68ffe-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="68ffe-237">Это обновленная версия!</span><span class="sxs-lookup"><span data-stu-id="68ffe-237">This is updated!</span></span>
   <span data-ttu-id="68ffe-238">17 июня, воскресенье, 16:39:10 UTC, 2017 г.</span><span class="sxs-lookup"><span data-stu-id="68ffe-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="68ffe-239">Перейдите по адресу: http://&lt;имя_приложени>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (замените &lt;x> и &lt;y> любыми числами) для получения суммы x и y.</span><span class="sxs-lookup"><span data-stu-id="68ffe-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="68ffe-241">Для службы приложений под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="68ffe-241">For App service on Linux</span></span>

* <span data-ttu-id="68ffe-242">Чтобы осуществить проверку, в Azure CLI выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="68ffe-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="68ffe-243">Вы получите следующий результат:</span><span class="sxs-lookup"><span data-stu-id="68ffe-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="68ffe-244">Перейдите по адресу: http://&lt;имя_приложения>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="68ffe-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="68ffe-245">Отобразится сообщение:</span><span class="sxs-lookup"><span data-stu-id="68ffe-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="68ffe-246">Перейдите по адресу: http://&lt;имя_приложени>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (замените &lt;x> и &lt;y> любыми числами) для получения суммы x и y.</span><span class="sxs-lookup"><span data-stu-id="68ffe-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="68ffe-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68ffe-247">Next steps</span></span>

<span data-ttu-id="68ffe-248">В этом руководстве вы выполнили развертывание в Azure с помощью подключаемого модуля службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="68ffe-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="68ffe-249">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="68ffe-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="68ffe-250">Настройка Jenkins для развертывания в службе приложений Azure по протоколу FTP.</span><span class="sxs-lookup"><span data-stu-id="68ffe-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="68ffe-251">Настройка Jenkins для развертывания в службе приложений Azure в Linux с помощью Docker.</span><span class="sxs-lookup"><span data-stu-id="68ffe-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 