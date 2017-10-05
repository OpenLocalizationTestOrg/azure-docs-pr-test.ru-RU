---
title: "Создание гипермасштабируемого приложения в Azure | Документация Майкрософт"
description: "Сведения об использовании различных служб Azure для максимального повышения производительности приложения ASP.NET в Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="9cd38-103">Создание гипермасштабируемого веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="9cd38-104">Это руководство содержит сведения о масштабировании веб-приложения ASP.NET в Azure для увеличения количества запросов пользователей.</span><span class="sxs-lookup"><span data-stu-id="9cd38-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="9cd38-105">Прежде чем начать работу с этим руководством, убедитесь, что на вашем компьютере [установлен Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9cd38-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="9cd38-106">Кроме того, вам потребуется запустить пример приложения на локальном компьютере с помощью [Visual Studio](https://www.visualstudio.com/vs/).</span><span class="sxs-lookup"><span data-stu-id="9cd38-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="9cd38-107">Шаг 1. Получение примера приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="9cd38-108">На этом шаге вы настроите локальный проект ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9cd38-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="9cd38-109">Клонирование репозитория приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-109">Clone the application repository</span></span>

<span data-ttu-id="9cd38-110">Откройте терминал и `CD` в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="9cd38-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="9cd38-111">Затем клонируйте пример приложения, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9cd38-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="9cd38-112">Запуск примера приложения в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cd38-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="9cd38-113">Откройте решение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cd38-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="9cd38-114">Нажмите клавишу `F5`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9cd38-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="9cd38-115">Этот пример веб-приложения ASP.NET создан на основе шаблона по умолчанию. Он сохраняет пользовательские сеансы и использует кэш вывода.</span><span class="sxs-lookup"><span data-stu-id="9cd38-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="9cd38-116">Просмотрите `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="9cd38-117">Метод `Index()` добавляет фрагмент данных в сеанс.</span><span class="sxs-lookup"><span data-stu-id="9cd38-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="9cd38-118">А методы `About()` и `Contact()` кэшируют свои выходные данные.</span><span class="sxs-lookup"><span data-stu-id="9cd38-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="9cd38-119">Шаг 2. Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="9cd38-120">На этом шаге вы создадите веб-приложение Azure и развернете в него пример приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9cd38-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="9cd38-121">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9cd38-121">Create a resource group</span></span>   
<span data-ttu-id="9cd38-122">Чтобы создать [группу ресурсов](../azure-resource-manager/resource-group-overview.md) в регионе "Западная Европа", выполните команду [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="9cd38-123">В группе ресурсов будут размещаться все ресурсы Azure, которыми вы хотите управлять совместно, например веб-приложение и любая серверная часть базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9cd38-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="9cd38-124">Чтобы увидеть доступные значения для `---location`, выполните команду [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="9cd38-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="9cd38-125">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="9cd38-125">Create an App Service plan</span></span>
<span data-ttu-id="9cd38-126">Чтобы создать [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) B1, выполните команду [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="9cd38-127">План службы приложений — это единица масштабирования, которая может включать любое количество приложений, масштаб которых необходимо увеличить или уменьшить в пределах одной инфраструктуры службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9cd38-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="9cd38-128">Каждый план также имеет свою [ценовую категорию](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="9cd38-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="9cd38-129">На более высоких уровнях используется лучшее оборудование и доступны дополнительные функции (например, дополнительные экземпляры масштабирования).</span><span class="sxs-lookup"><span data-stu-id="9cd38-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="9cd38-130">В этом руководстве используется уровень B1. Это минимальный уровень, который позволяет масштабировать до трех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="9cd38-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="9cd38-131">Вы всегда сможете изменить ценовую категорию позже, выполнив команду [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="9cd38-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="9cd38-132">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-132">Create a web app</span></span>
<span data-ttu-id="9cd38-133">Чтобы создать веб-приложение с уникальным именем в `$appName`, выполните команду [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="9cd38-134">Сброс учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="9cd38-134">Set deployment credentials</span></span>
<span data-ttu-id="9cd38-135">Чтобы настроить учетные данные развертывания на уровне учетной записи, выполните команду[az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set).</span><span class="sxs-lookup"><span data-stu-id="9cd38-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="9cd38-136">Настройка развертывания Git</span><span class="sxs-lookup"><span data-stu-id="9cd38-136">Configure Git deployment</span></span>
<span data-ttu-id="9cd38-137">Чтобы настроить локальное развертывание Git, выполните команду [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git).</span><span class="sxs-lookup"><span data-stu-id="9cd38-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="9cd38-138">В результате вы получите выходные данные, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9cd38-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="9cd38-139">Настройте удаленный репозиторий Git, используя возвращенный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9cd38-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="9cd38-140">Следующая команда использует пример предыдущих выходных данных:</span><span class="sxs-lookup"><span data-stu-id="9cd38-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="9cd38-141">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-141">Deploy the sample application</span></span>
<span data-ttu-id="9cd38-142">Теперь все готово для развертывания примера приложения.</span><span class="sxs-lookup"><span data-stu-id="9cd38-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="9cd38-143">Запустите `git push`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="9cd38-144">При появлении запроса на ввод пароля используйте пароль, указанный при выполнении `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="9cd38-145">Переход к веб-приложению Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-145">Browse to Azure web app</span></span>
<span data-ttu-id="9cd38-146">Чтобы увидеть работу приложения в Azure в реальном времени, выполните команду [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse).</span><span class="sxs-lookup"><span data-stu-id="9cd38-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="9cd38-147">Шаг 3. Подключение к Redis</span><span class="sxs-lookup"><span data-stu-id="9cd38-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="9cd38-148">На этом шаге вы настроите кэш Redis для Azure в качестве внешнего кэша, совместно размещенного с веб-приложением Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd38-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="9cd38-149">Вы можете быстро использовать Redis, чтобы кэшировать выходные данные страницы.</span><span class="sxs-lookup"><span data-stu-id="9cd38-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="9cd38-150">Кроме того, при дальнейшем масштабировании веб-приложения Redis поможет надежно сохранить пользовательские сеансы в нескольких экземплярах.</span><span class="sxs-lookup"><span data-stu-id="9cd38-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="9cd38-151">Создание кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="9cd38-152">Чтобы создать кэш Redis для Azure и сохранить выходные данные JSON, выполните команду [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="9cd38-153">Укажите уникальное имя в `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="9cd38-154">Настройка приложения для использования Redis</span><span class="sxs-lookup"><span data-stu-id="9cd38-154">Configure the application to use Redis</span></span>
<span data-ttu-id="9cd38-155">Отформатируйте строку подключения для кэша.</span><span class="sxs-lookup"><span data-stu-id="9cd38-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="9cd38-156">Во второй строке должны отобразиться выходные данные, аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="9cd38-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="9cd38-157">В Visual Studio создайте файл веб-конфигурации `redis.config` в корневом каталоге проекта и вставьте в него указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9cd38-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="9cd38-158">В `value` укажите строку подключения из выходных данных PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cd38-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="9cd38-159">Если взглянуть на файл `.gitignore` в репозитории Git, вы увидите, что этот файл исключен из системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="9cd38-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="9cd38-160">Таким образом ваша конфиденциальная информация находится в безопасности.</span><span class="sxs-lookup"><span data-stu-id="9cd38-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="9cd38-161">Откройте `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-161">Open `Web.config`.</span></span> <span data-ttu-id="9cd38-162">Обратите внимание на элемент `<appSettings file="redis.config">`, который получает параметры, созданные в `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="9cd38-163">Найдите раздел с комментариями, содержащий сведения `<sessionState>` и `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="9cd38-164">Раскомментируйте его.</span><span class="sxs-lookup"><span data-stu-id="9cd38-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="9cd38-165">Этот код ищет строку подключения Redis, определенную в `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="9cd38-166">Теперь для управления сеансами и кэширования ваше приложение использует Redis.</span><span class="sxs-lookup"><span data-stu-id="9cd38-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="9cd38-167">Нажмите клавишу `F5`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="9cd38-167">Type `F5` to run the application.</span></span> <span data-ttu-id="9cd38-168">При необходимости можно скачать клиент управления Redis, чтобы визуализировать данные, сохраненные в кэше.</span><span class="sxs-lookup"><span data-stu-id="9cd38-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="9cd38-169">Настройка строки подключения в Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="9cd38-170">Для работы приложения в Azure необходимо настроить ту же строку подключения Redis в веб-приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd38-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="9cd38-171">Так как файл `redis.config` не поддерживается в системе управления версиями, то при выполнении развертывания Git он не будет развертываться в Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd38-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="9cd38-172">Выполните команду [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update), чтобы добавить строку подключения с таким же именем (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="9cd38-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="9cd38-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9cd38-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="9cd38-174">Помните, что `$connstring` содержит форматированную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="9cd38-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="9cd38-175">Повторное развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="9cd38-176">Чтобы отправить изменения в Azure, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9cd38-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="9cd38-177">При появлении запроса на ввод пароля используйте пароль, указанный при выполнении `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="9cd38-178">Переход к веб-приложению Azure</span><span class="sxs-lookup"><span data-stu-id="9cd38-178">Browse to the Azure web app</span></span>
<span data-ttu-id="9cd38-179">Чтобы просмотреть изменения в Azure, выполните команду [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse).</span><span class="sxs-lookup"><span data-stu-id="9cd38-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="9cd38-180">Шаг 4. Масштабирование до нескольких экземпляров</span><span class="sxs-lookup"><span data-stu-id="9cd38-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="9cd38-181">План службы приложений — это единица масштабирования для веб-приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd38-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="9cd38-182">Чтобы увеличить масштаб веб-приложения, необходимо добавить экземпляры в плане службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9cd38-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="9cd38-183">Выполните команду [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update), чтобы масштабировать план службы приложений до трех экземпляров. Это максимальное количество, допустимое в ценовой категории B1.</span><span class="sxs-lookup"><span data-stu-id="9cd38-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="9cd38-184">Помните, что B1 — это ценовая категория, выбранная во время создания плана службы приложений ранее.</span><span class="sxs-lookup"><span data-stu-id="9cd38-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="9cd38-185">Шаг 5. Развертывание приложения в нескольких регионах</span><span class="sxs-lookup"><span data-stu-id="9cd38-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="9cd38-186">Вы можете развернуть ваше приложение в облаке Azure в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="9cd38-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="9cd38-187">Эта настройка балансирует нагрузку приложения в зависимости от географического расположения и снижает время ответа, размещая приложение рядом с клиентскими браузерами.</span><span class="sxs-lookup"><span data-stu-id="9cd38-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="9cd38-188">На этом этапе вы развернете веб-приложение ASP.NET во втором регионе с помощью [диспетчера трафика Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="9cd38-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="9cd38-189">По завершении этого этапа уже созданное веб-приложение будет запущено в Западной Европе, а приложение, которое мы создадим позже, — в Юго-Восточной Азии.</span><span class="sxs-lookup"><span data-stu-id="9cd38-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="9cd38-190">Оба приложения будут обслуживаться с использованием одного URL-адреса диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="9cd38-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="9cd38-191">Перенос приложения в Европе на уровень "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="9cd38-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="9cd38-192">Чтобы интегрировать диспетчер трафика Azure в службе приложений, требуется ценовая категория "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="9cd38-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="9cd38-193">Чтобы настроить для плана службы приложений уровень S1, выполните команду [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="9cd38-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="9cd38-194">Создание профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="9cd38-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="9cd38-195">Чтобы создать профиль диспетчера трафика и добавить его в группу ресурсов, выполните команду [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="9cd38-196">В параметре $dnsName укажите уникальное DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="9cd38-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="9cd38-197">`--routing-method Performance` указывает, что профиль [направляет пользовательский трафик в ближайшую конечную точку](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="9cd38-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="9cd38-198">Получение идентификатора ресурса приложения в Европе</span><span class="sxs-lookup"><span data-stu-id="9cd38-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="9cd38-199">Чтобы получить идентификатор ресурса веб-приложения, выполните команду [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show).</span><span class="sxs-lookup"><span data-stu-id="9cd38-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="9cd38-200">Добавление конечной точки диспетчера трафика для приложения в Европе</span><span class="sxs-lookup"><span data-stu-id="9cd38-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="9cd38-201">Чтобы добавить конечную точку в профиль диспетчера трафика и использовать в качестве целевого объекта идентификатор ресурса веб-приложения, выполните команду [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="9cd38-202">Получение URL-адреса конечной точки диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="9cd38-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="9cd38-203">Профиль диспетчера трафика теперь содержит конечную точку, указывающую на существующее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9cd38-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="9cd38-204">Чтобы получить URL-адрес, выполните команду [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show).</span><span class="sxs-lookup"><span data-stu-id="9cd38-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="9cd38-205">Скопируйте выходные данные в браузер.</span><span class="sxs-lookup"><span data-stu-id="9cd38-205">Copy the output into your browser.</span></span> <span data-ttu-id="9cd38-206">Вы должны снова увидеть свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="9cd38-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="9cd38-207">Создание кэша Redis для Azure в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="9cd38-208">Теперь необходимо реплицировать веб-приложение Azure в Юго-Восточную Азию.</span><span class="sxs-lookup"><span data-stu-id="9cd38-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="9cd38-209">Для начала выполните команду [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create), чтобы создать второй кэш Redis для Azure в Юго-Восточной Азии.</span><span class="sxs-lookup"><span data-stu-id="9cd38-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="9cd38-210">Этот кэш должен быть совместно размещен с вашим приложением в Азии.</span><span class="sxs-lookup"><span data-stu-id="9cd38-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="9cd38-211">`--name $cacheName-asia` присваивает имя кэша Западной Европы с добавлением суффикса `-asia`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="9cd38-212">Создание плана службы приложений в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="9cd38-213">Выполните команду [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create), чтобы создать второй план службы приложений в Юго-Восточной Азии, используя тот же уровень S1, что и для плана Западной Европы.</span><span class="sxs-lookup"><span data-stu-id="9cd38-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="9cd38-214">Создание веб-приложения в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-214">Create a web app in Asia</span></span>
<span data-ttu-id="9cd38-215">Чтобы создать второе веб-приложение, выполните команду [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="9cd38-216">`--name $appName-asia` присваивает имя приложения Западной Европы с добавлением суффикса `-asia`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="9cd38-217">Настройка строки подключения для Redis</span><span class="sxs-lookup"><span data-stu-id="9cd38-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="9cd38-218">Чтобы добавить в веб-приложение строку подключения для кэша Юго-Восточной Азии, выполните команду [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update).</span><span class="sxs-lookup"><span data-stu-id="9cd38-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="9cd38-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9cd38-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="9cd38-220">Настройка развертывания Git для приложения в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="9cd38-221">Чтобы настроить локальное развертывание Git для второго веб-приложения, выполните команду [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git).</span><span class="sxs-lookup"><span data-stu-id="9cd38-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="9cd38-222">В результате вы получите выходные данные, которые выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9cd38-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="9cd38-223">Используйте возвращенный URL-адрес, чтобы настроить второй удаленный репозиторий Git для локального репозитория.</span><span class="sxs-lookup"><span data-stu-id="9cd38-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="9cd38-224">Следующая команда использует пример предыдущих выходных данных:</span><span class="sxs-lookup"><span data-stu-id="9cd38-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="9cd38-225">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-225">Deploy your sample application</span></span>
<span data-ttu-id="9cd38-226">Чтобы развернуть пример приложения во втором удаленном репозитории Git, выполните команду `git push`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="9cd38-227">При появлении запроса на ввод пароля используйте пароль, указанный при выполнении `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="9cd38-228">Переход в приложение в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-228">Browse to the Asia app</span></span>
<span data-ttu-id="9cd38-229">Чтобы убедиться, что приложение запущено в Azure, выполните команду [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse).</span><span class="sxs-lookup"><span data-stu-id="9cd38-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="9cd38-230">Получение идентификатора ресурса приложения в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="9cd38-231">Чтобы получить идентификатор ресурса веб-приложения в Юго-Восточной Азии, выполните команду [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show).</span><span class="sxs-lookup"><span data-stu-id="9cd38-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="9cd38-232">Добавление конечной точки диспетчера трафика для приложения в Азии</span><span class="sxs-lookup"><span data-stu-id="9cd38-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="9cd38-233">Чтобы добавить вторую конечную точку в профиль диспетчера трафика, выполните команду [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create).</span><span class="sxs-lookup"><span data-stu-id="9cd38-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="9cd38-234">Добавление идентификатора региона в веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9cd38-234">Add region identifier to web apps</span></span>
<span data-ttu-id="9cd38-235">Чтобы добавить переменные среды для конкретного региона, выполните команду [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update).</span><span class="sxs-lookup"><span data-stu-id="9cd38-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="9cd38-236">Код приложения уже использует этот параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="9cd38-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="9cd38-237">Просмотрите `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9cd38-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="9cd38-238">Готово!</span><span class="sxs-lookup"><span data-stu-id="9cd38-238">Complete!</span></span>

<span data-ttu-id="9cd38-239">Теперь попробуйте перейти по URL-адресу профиля диспетчера трафика из браузеров в разных географических регионах.</span><span class="sxs-lookup"><span data-stu-id="9cd38-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="9cd38-240">В клиентских браузерах в Европе должно отображаться ASP.NET West Europe (ASP.NET, Западная Европа), а в браузерах клиентов из Азии — ASP.NET Southeast Asia (ASP.NET, Юго-Восточная Азия).</span><span class="sxs-lookup"><span data-stu-id="9cd38-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="9cd38-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9cd38-241">More resources</span></span>
