---
title: "aaaExecute hello Azure CLI с Jenkins | Документы Microsoft"
description: "Узнайте, как Azure CLI toouse toodeploy Java веб-приложения tooAzure в конвейере Jenkins"
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
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="3b8a9-103">Развертывание службы приложений с Jenkins tooAzure и hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3b8a9-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="3b8a9-104">toodeploy tooAzure Java web app, можно использовать Azure CLI в [Jenkins конвейера](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="3b8a9-105">В этом учебнике мы создадим конвейер CI/CD на виртуальной машине Azure, включая следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b8a9-106">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="3b8a9-107">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-107">Configure Jenkins</span></span>
> * <span data-ttu-id="3b8a9-108">Создание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="3b8a9-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="3b8a9-109">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="3b8a9-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="3b8a9-110">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="3b8a9-111">Запустите конвейера hello и проверьте hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3b8a9-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="3b8a9-112">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3b8a9-113">версия toofind hello, запустите `az --version`.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="3b8a9-114">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="3b8a9-115">Создание и настройка экземпляра Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="3b8a9-116">Если главный Jenkins еще нет начните с hello [шаблон решения](install-jenkins-solution-template.md), включающее необходимые hello [учетные данные Azure](https://plugins.jenkins.io/azure-credentials) подключаемого модуля по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="3b8a9-117">Подключаемый модуль Hello учетных данных Azure позволяет основной учетных данных службы Microsoft Azure toostore в Jenkins.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="3b8a9-118">В версии 1.2 была добавлена поддержка hello, поэтому конвейера Jenkins можно получить hello учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="3b8a9-119">Убедитесь, что у вас установлена версия 1.2 или более поздняя:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="3b8a9-120">Панели мониторинга Jenkins hello, нажмите кнопку **Jenkins управления -> подключаемого модуля диспетчера ->** и выполните поиск **учетные данные Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="3b8a9-121">Обновление подключаемого модуля hello, если hello версия более ранняя, чем 1.2.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="3b8a9-122">В базе данных master Jenkins hello также требуются Java JDK и Maven.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="3b8a9-123">tooinstall, войдите в базе данных master tooJenkins с помощью SSH и запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="3b8a9-124">Добавление учетных данных участника tooJenkins службы Azure</span><span class="sxs-lookup"><span data-stu-id="3b8a9-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="3b8a9-125">Учетных данных Azure — необходимые tooexecute Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="3b8a9-126">Панели мониторинга Jenkins hello, нажмите кнопку **учетные данные -> Система ->**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="3b8a9-127">Щелкните **Global credentials (unrestricted)** (Глобальные учетные данные (неограниченные)).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="3b8a9-128">Нажмите кнопку **добавить учетные данные** tooadd [субъекта-службы Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) , заполнив hello идентификатор подписки, идентификатор клиента, секрет клиента и конечная точка маркера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="3b8a9-129">Укажите идентификатор, который будет использоваться в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-129">Provide an ID for use in subsequent step.</span></span>

![Добавить учетные данные](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="3b8a9-131">Создание службы приложения Azure для развертывания веб-приложения Java hello</span><span class="sxs-lookup"><span data-stu-id="3b8a9-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="3b8a9-132">Создать план службы приложений Azure с hello **FREE** ценовой категории с помощью hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команду CLI.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="3b8a9-133">план служб приложений Hello определяет toohost hello физические ресурсы, используемые приложения.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="3b8a9-134">Все приложения, назначенный tooan план служб приложений используют эти ресурсы, позволяя toosave затрат при размещении нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="3b8a9-135">При готовности плана hello hello Azure CLI показывает, как выходной toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="3b8a9-136">Создание веб-приложения Azure</span><span class="sxs-lookup"><span data-stu-id="3b8a9-136">Create an Azure Web app</span></span>

 <span data-ttu-id="3b8a9-137">Используйте hello [создать веб-приложение az](/cli/azure/appservice/web#create) toocreate команду CLI определение web app в hello `myAppServicePlan` план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="3b8a9-138">Определение приложения Hello web предоставляет приложению tooaccess URL-адрес и настраивает некоторые параметры toodeploy tooAzure вашего кода.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="3b8a9-139">Замена hello `<app_name>` заполнитель с именем собственный уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="3b8a9-140">Это уникальное имя является частью hello имя домена по умолчанию для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="3b8a9-141">Перед тем, как он tooyour пользователей можно сопоставить toohello входа пользовательского домена имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="3b8a9-142">При готовности определение приложения hello web hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="3b8a9-143">Настройка Java</span><span class="sxs-lookup"><span data-stu-id="3b8a9-143">Configure Java</span></span> 

<span data-ttu-id="3b8a9-144">Настройка конфигурации среды выполнения Java hello, необходимый вашему приложению hello [обновление конфигурации web appservice az](/cli/azure/appservice/web/config#update) команды.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="3b8a9-145">Hello следующая команда настраивает hello web app toorun на последние Java JDK 8 и [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="3b8a9-146">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="3b8a9-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="3b8a9-147">Откройте hello [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) репозитория.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="3b8a9-148">toofork hello репозитория tooyour владельцем учетной записи GitHub, нажмите кнопку hello **вилки** кнопку в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="3b8a9-149">В пользовательском веб-интерфейсе GitHub откройте файл **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="3b8a9-150">Нажмите кнопку tooedit значок карандаша hello этой группы ресурсов hello tooupdate файла и имя веб-приложения в строке, 20 и 21 соответственно.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="3b8a9-151">Измените идентификатор учетных данных 23 tooupdate строки в вашем экземпляре Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="3b8a9-152">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="3b8a9-153">Откройте Jenkins в веб-браузере, щелкните **New Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="3b8a9-154">Укажите имя для задания hello и выберите **конвейера**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="3b8a9-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-155">Click **OK**.</span></span>
* <span data-ttu-id="3b8a9-156">Нажмите кнопку hello **конвейера** вкладке рядом.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="3b8a9-157">Для параметра **Definition** (Определение) выберите значение **Pipeline script from SCM** (Сценарий конвейера из SCM).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="3b8a9-158">Для параметра **SCM** выберите значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="3b8a9-159">Введите hello GitHub URL-адрес для вашего разветвленного репозитория: https:\<репозиторию разветвленного\>.git</span><span class="sxs-lookup"><span data-stu-id="3b8a9-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="3b8a9-160">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="3b8a9-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="3b8a9-161">Тестирование конвейера</span><span class="sxs-lookup"><span data-stu-id="3b8a9-161">Test your pipeline</span></span>
* <span data-ttu-id="3b8a9-162">Go toohello конвейера, вы создали, щелкните **теперь построения**</span><span class="sxs-lookup"><span data-stu-id="3b8a9-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="3b8a9-163">Сборка должна выполняться в течение нескольких секунд, и вы можете вернуться toohello построения и нажмите кнопку **вывод на консоль** toosee hello сведения</span><span class="sxs-lookup"><span data-stu-id="3b8a9-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="3b8a9-164">Проверка веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3b8a9-164">Verify your web app</span></span>
<span data-ttu-id="3b8a9-165">tooverify hello WAR-файл успешно развернут tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="3b8a9-166">Откройте веб-браузер:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-166">Open a web browser:</span></span>

* <span data-ttu-id="3b8a9-167">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="3b8a9-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="3b8a9-168">Вот что вы увидите:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="3b8a9-169">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y</span><span class="sxs-lookup"><span data-stu-id="3b8a9-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Калькулятор: сложение](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="3b8a9-171">Развертывание tooAzure веб-приложения в Linux</span><span class="sxs-lookup"><span data-stu-id="3b8a9-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="3b8a9-172">Теперь, когда вы знаете, как конвейер toouse Azure CLI в вашей Jenkins, вы можете изменить tooan toodeploy hello скрипта веб-приложения Azure в Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="3b8a9-173">Веб-приложения на платформе Linux поддерживает развертывание hello toodo другим способом, который является toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="3b8a9-174">toodeploy, необходимо tooprovide Dockerfile, которая упаковывает веб-приложения в среде выполнения службы в Docker изображение.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="3b8a9-175">Подключаемый модуль Hello затем сборки образа hello, принудительно отправить его tooa реестра Docker и развертывания hello изображения tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="3b8a9-176">Выполните действия hello [здесь](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate на веб-приложения Azure, выполняемым на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="3b8a9-177">Установка Docker Jenkins экземпляра в соответствии с инструкциями hello в этом [статьи](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="3b8a9-178">Создание реестра контейнера в hello портал Azure с помощью действия hello [здесь](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3b8a9-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="3b8a9-179">В hello же [простого веб-приложения Java для Azure](https://github.com/azure-devops/javawebappsample) репозитория вы разделенными, изменить hello **Jenkinsfile2** файла:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="3b8a9-180">Строка 18-21, соответственно обновить имена toohello группы ресурсов, веб-приложения и контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="3b8a9-181">Строка 24, обновление \<azsrvprincipal\> tooyour идентификатор учетных данных</span><span class="sxs-lookup"><span data-stu-id="3b8a9-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="3b8a9-182">Создать новый конвейер Jenkins, как это было сделано при развертывании tooAzure веб-приложения в Windows, только на этот раз используйте **Jenkinsfile2** вместо него.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="3b8a9-183">Запустите новое задание.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-183">Run your new job.</span></span>
* <span data-ttu-id="3b8a9-184">tooverify, в Azure CLI, выполните:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="3b8a9-185">Вы получаете hello следующий результат:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="3b8a9-186">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="3b8a9-187">Отображается сообщение hello:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="3b8a9-188">Go toohttp: / /&lt;имя_приложения >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (подставьте &lt;x > и &lt;y > с любой цифры) сумма hello tooget x и y</span><span class="sxs-lookup"><span data-stu-id="3b8a9-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="3b8a9-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b8a9-189">Next steps</span></span>
<span data-ttu-id="3b8a9-190">В этом учебнике вы настроили Jenkins конвейера, который извлекает hello исходного кода в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="3b8a9-191">Выполняется Maven toobuild war-файл и затем использует Azure CLI toodeploy tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3b8a9-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="3b8a9-192">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3b8a9-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3b8a9-193">Создание виртуальной машины Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="3b8a9-194">Настройка Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-194">Configure Jenkins</span></span>
> * <span data-ttu-id="3b8a9-195">Создание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="3b8a9-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="3b8a9-196">Подготовка репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="3b8a9-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="3b8a9-197">Создание конвейера Jenkins</span><span class="sxs-lookup"><span data-stu-id="3b8a9-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="3b8a9-198">Запустите конвейера hello и проверьте hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="3b8a9-198">Run hello pipeline and verify hello web app</span></span>
