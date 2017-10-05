---
title: "Выполнение Azure CLI с помощью Jenkins | Документация Майкрософт"
description: "Сведения об использовании Azure CLI для развертывания веб-приложения Java в Azure в конвейере Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="88fa8-103">Развертывание в службу приложений Azure с помощью Jenkins и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88fa8-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="88fa8-104">Для развертывания веб-приложения Java в Azure можно использовать Azure CLI в [конвейере Jenkins](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="88fa8-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="88fa8-105">В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="88fa8-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88fa8-106">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="88fa8-107">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-107">Configure Jenkins</span></span>
> * <span data-ttu-id="88fa8-108">Создание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="88fa8-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="88fa8-109">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="88fa8-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="88fa8-110">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="88fa8-111">Запуск конвейера и проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="88fa8-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="88fa8-112">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="88fa8-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="88fa8-113">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="88fa8-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="88fa8-114">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88fa8-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="88fa8-115">Создание и настройка экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="88fa8-116">Если у вас нет главного экземпляра, воспользуйтесь [шаблоном решений](install-jenkins-solution-template.md), который по умолчанию содержит необходимый подключаемый модуль [Учетные данные Azure](https://plugins.jenkins.io/azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="88fa8-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="88fa8-117">Подключаемый модуль учетных данных Azure позволяет хранить учетные данные субъекта-службы Microsoft Azure в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="88fa8-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="88fa8-118">В версии 1.2 добавлена соответствующая поддержка, поэтому конвейер Jenkins может получать учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa8-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="88fa8-119">Убедитесь, что у вас установлена версия 1.2 или более поздняя:</span><span class="sxs-lookup"><span data-stu-id="88fa8-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="88fa8-120">На панели мониторинга Jenkins последовательно выберите **Manage Jenkins -> Plugin Manager ->** (Управление Jenkins -> Диспетчер подключаемых модулей) и выполните поиск **учетных данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="88fa8-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="88fa8-121">Если используется версия более ранняя, чем 1.2, обновите подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="88fa8-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="88fa8-122">В главном экземпляре Jenkins также требуются Java JDK и Maven.</span><span class="sxs-lookup"><span data-stu-id="88fa8-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="88fa8-123">Чтобы выполнить установку, войдите в главный экземпляр с помощью SSH-подключения и выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="88fa8-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="88fa8-124">Добавление субъекта-службы Azure в учетные данные Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="88fa8-125">Для выполнения Azure CLI необходимы учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa8-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="88fa8-126">На панели мониторинга Jenkins выберите **Credentials -> System ->**(Учетные данные -> Система).</span><span class="sxs-lookup"><span data-stu-id="88fa8-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="88fa8-127">Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).</span><span class="sxs-lookup"><span data-stu-id="88fa8-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="88fa8-128">Щелкните **Add Credentials** (Добавить учетные данные), чтобы добавить [субъект-службу Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) путем ввода следующих значений: идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="88fa8-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="88fa8-129">Укажите идентификатор, который будет использоваться в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="88fa8-129">Provide an ID for use in subsequent step.</span></span>

![Добавить учетные данные](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="88fa8-131">Создание службы приложений Azure для развертывания веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="88fa8-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="88fa8-132">Создайте план службы приложений Azure с ценовой категорией **Бесплатный** с помощью команды CLI [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="88fa8-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="88fa8-133">От плана службы приложений зависят физические ресурсы, используемые для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="88fa8-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="88fa8-134">Все приложения, назначенные плану службы приложений, совместно используют ресурсы, которые позволяют сэкономить при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="88fa8-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="88fa8-135">После создания плана в Azure CLI отобразится приблизительно такой результат:</span><span class="sxs-lookup"><span data-stu-id="88fa8-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="88fa8-136">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="88fa8-136">Create an Azure Web app</span></span>

 <span data-ttu-id="88fa8-137">С помощью команды CLI [az webapp create](/cli/azure/appservice/web#create) создайте определение веб-приложения в плане службы приложений `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="88fa8-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="88fa8-138">Определение веб-приложения предоставляет URL-адрес для доступа к приложению и настраивает несколько параметров для развертывания кода в Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa8-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="88fa8-139">Замените заполнитель `<app_name>` уникальным именем своего приложения.</span><span class="sxs-lookup"><span data-stu-id="88fa8-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="88fa8-140">Это уникальное имя используется в доменном имени по умолчанию для веб-приложения, поэтому оно должно быть уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa8-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="88fa8-141">Позже можно сопоставить запись личного доменного имени с веб-приложением, прежде чем предоставлять его пользователям.</span><span class="sxs-lookup"><span data-stu-id="88fa8-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="88fa8-142">Когда вы создадите определение веб-приложения, в Azure CLI отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="88fa8-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="88fa8-143">Настройка Java</span><span class="sxs-lookup"><span data-stu-id="88fa8-143">Configure Java</span></span> 

<span data-ttu-id="88fa8-144">Настройте конфигурацию среды выполнения Java, необходимую для работы приложения, с помощью команды [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="88fa8-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="88fa8-145">Следующая команда настраивает веб-приложение для запуска в Java 8 JDK и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="88fa8-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="88fa8-146">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="88fa8-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="88fa8-147">Откройте репозиторий [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) (Простое веб-приложение Java для Azure).</span><span class="sxs-lookup"><span data-stu-id="88fa8-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="88fa8-148">Чтобы создать разветвление репозитория для своей учетной записи GitHub, нажмите кнопку **Fork** (Разветвление) в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="88fa8-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="88fa8-149">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="88fa8-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="88fa8-150">Щелкните значок с изображением карандаша, чтобы изменить этот файл для обновления группы ресурсов и имени веб-приложения в строках 20 и 21, соответственно.</span><span class="sxs-lookup"><span data-stu-id="88fa8-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="88fa8-151">Измените строку 23 для обновления идентификатора учетных данных в вашем экземпляре Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="88fa8-152">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="88fa8-153">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="88fa8-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="88fa8-154">Укажите имя задания и выберите **Pipeline** (Конвейер).</span><span class="sxs-lookup"><span data-stu-id="88fa8-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="88fa8-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88fa8-155">Click **OK**.</span></span>
* <span data-ttu-id="88fa8-156">Откройте вкладку **Pipeline** (Конвейер), находящуюся рядом.</span><span class="sxs-lookup"><span data-stu-id="88fa8-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="88fa8-157">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="88fa8-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="88fa8-158">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="88fa8-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="88fa8-159">Введите URL-адрес GitHub для разветвленного репозитория: https:\<разветвленный репозиторий\>.git</span><span class="sxs-lookup"><span data-stu-id="88fa8-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="88fa8-160">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="88fa8-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="88fa8-161">Тестирование конвейера</span><span class="sxs-lookup"><span data-stu-id="88fa8-161">Test your pipeline</span></span>
* <span data-ttu-id="88fa8-162">Перейдите созданный в конвейер и щелкните **Build Now** (Собрать).</span><span class="sxs-lookup"><span data-stu-id="88fa8-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="88fa8-163">Процесс должен завершиться в течение нескольких секунд, после чего можно перейти к сборке и щелкнуть **Console Output** (Вывод консоли), чтобы просмотреть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="88fa8-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="88fa8-164">Проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="88fa8-164">Verify your web app</span></span>
<span data-ttu-id="88fa8-165">Чтобы проверить успешное развертывание WAR-файла в веб-приложении:</span><span class="sxs-lookup"><span data-stu-id="88fa8-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="88fa8-166">Откройте веб-браузер:</span><span class="sxs-lookup"><span data-stu-id="88fa8-166">Open a web browser:</span></span>

* <span data-ttu-id="88fa8-167">Перейдите по адресу: http://&lt;имя_приложения>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="88fa8-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="88fa8-168">Вот что вы увидите:</span><span class="sxs-lookup"><span data-stu-id="88fa8-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="88fa8-169">Перейдите по адресу: http://&lt;имя_приложени>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (замените &lt;x> и &lt;y> любыми числами) для получения суммы x и y.</span><span class="sxs-lookup"><span data-stu-id="88fa8-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="88fa8-171">Развертывание в веб-приложении Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="88fa8-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="88fa8-172">Теперь, когда вы знаете, как использовать Azure CLI в конвейере Jenkins, можно изменить сценарий для развертывания в веб-приложении Azure в Linux.</span><span class="sxs-lookup"><span data-stu-id="88fa8-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="88fa8-173">Для развертывания в веб-приложении в Linux поддерживается другой способ, который заключается в использовании Docker.</span><span class="sxs-lookup"><span data-stu-id="88fa8-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="88fa8-174">Чтобы выполнить развертывание, необходимо предоставить файл Dockerfile, который упаковывает веб-приложение со службой среды выполнения в образ Docker.</span><span class="sxs-lookup"><span data-stu-id="88fa8-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="88fa8-175">Затем подключаемый модуль создаст образ, отправит его в реестр Docker и развернет в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="88fa8-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="88fa8-176">Выполните описанные [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app) действия по созданию веб-приложения Azure на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="88fa8-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="88fa8-177">Установите Docker в экземпляре Jenkins, следуя инструкциям в этой [статье](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="88fa8-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="88fa8-178">Создайте реестр контейнеров на портале Azure, выполнив описанные [здесь](/azure/container-registry/container-registry-get-started-azure-cli) действия.</span><span class="sxs-lookup"><span data-stu-id="88fa8-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="88fa8-179">В том же разветвленном репозитории [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) (Простое веб-приложение Java для Azure) измените файл **Jenkinsfile2**:</span><span class="sxs-lookup"><span data-stu-id="88fa8-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="88fa8-180">В строках 18–21 обновите имена группы ресурсов, веб-приложения и ACR, соответственно.</span><span class="sxs-lookup"><span data-stu-id="88fa8-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="88fa8-181">В строке 24 обновите \<azsrvprincipal\> значением идентификатора учетных данных.</span><span class="sxs-lookup"><span data-stu-id="88fa8-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="88fa8-182">Создайте конвейер Jenkins, как вы делали это при развертывании в веб-приложение Azure в Windows, только на этот раз используйте **Jenkinsfile2**.</span><span class="sxs-lookup"><span data-stu-id="88fa8-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="88fa8-183">Запустите новое задание.</span><span class="sxs-lookup"><span data-stu-id="88fa8-183">Run your new job.</span></span>
* <span data-ttu-id="88fa8-184">Чтобы осуществить проверку, в Azure CLI выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="88fa8-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="88fa8-185">Вы получите следующий результат:</span><span class="sxs-lookup"><span data-stu-id="88fa8-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="88fa8-186">Перейдите по адресу: http://&lt;имя_приложения>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="88fa8-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="88fa8-187">Отобразится сообщение:</span><span class="sxs-lookup"><span data-stu-id="88fa8-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="88fa8-188">Перейдите по адресу: http://&lt;имя_приложени>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (замените &lt;x> и &lt;y> любыми числами) для получения суммы x и y.</span><span class="sxs-lookup"><span data-stu-id="88fa8-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="88fa8-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88fa8-189">Next steps</span></span>
<span data-ttu-id="88fa8-190">В этом руководстве вы настроили конвейер Jenkins, который извлекает исходный код в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="88fa8-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="88fa8-191">Он запускает Maven для построения WAR-файла, а затем использует Azure CLI для развертывания в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="88fa8-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="88fa8-192">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="88fa8-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="88fa8-193">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="88fa8-194">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-194">Configure Jenkins</span></span>
> * <span data-ttu-id="88fa8-195">Создание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="88fa8-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="88fa8-196">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="88fa8-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="88fa8-197">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="88fa8-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="88fa8-198">Запуск конвейера и проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="88fa8-198">Run the pipeline and verify the web app</span></span>
