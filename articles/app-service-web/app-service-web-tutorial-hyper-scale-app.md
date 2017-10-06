---
title: "aaaBuild крупномасштабных приложений в Azure | Документы Microsoft"
description: "Узнайте, как toomaximize toouse различных служб Azure hello производительности приложения ASP.NET в Azure."
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
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="a1f88-103">Создание гипермасштабируемого веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="a1f88-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="a1f88-104">Этот учебник показывает, как tooscale ожидания веб-приложение ASP.NET в Azure toomaximize пользователь запросов.</span><span class="sxs-lookup"><span data-stu-id="a1f88-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="a1f88-105">Перед запуском этого учебника, убедитесь, что [hello Azure CLI устанавливается](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a1f88-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="a1f88-106">Кроме того, [Visual Studio](https://www.visualstudio.com/vs/) в пример приложения hello toorun локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="a1f88-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="a1f88-107">Шаг 1. Получение примера приложения</span><span class="sxs-lookup"><span data-stu-id="a1f88-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="a1f88-108">На этом шаге настраивается hello локального проекта ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a1f88-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="a1f88-109">Репозиторий приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="a1f88-109">Clone hello application repository</span></span>

<span data-ttu-id="a1f88-110">Откройте hello командной строки терминалов по своему усмотрению и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="a1f88-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="a1f88-111">Затем hello выполнения следующих команд tooclone hello образца приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="a1f88-112">Запустить образец приложения hello в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1f88-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="a1f88-113">Откройте решение hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1f88-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="a1f88-114">Тип `F5` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="a1f88-115">Этот образец веб-приложения ASP.NET поступают из шаблона по умолчанию hello и сохраняет пользователя сеансов и использует hello кэша вывода.</span><span class="sxs-lookup"><span data-stu-id="a1f88-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="a1f88-116">Просмотрите `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="a1f88-117">Hello `Index()` метод добавляет часть данных toohello сеанса.</span><span class="sxs-lookup"><span data-stu-id="a1f88-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="a1f88-118">И hello `About()` и `Contact()` методы кэшировать свои выходные данные.</span><span class="sxs-lookup"><span data-stu-id="a1f88-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="a1f88-119">Шаг 2 - развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="a1f88-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="a1f88-120">На этом шаге создания веб-приложение Azure и развертывания вашего tooit приложения ASP.NET образца.</span><span class="sxs-lookup"><span data-stu-id="a1f88-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="a1f88-121">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a1f88-121">Create a resource group</span></span>   
<span data-ttu-id="a1f88-122">Используйте [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) toocreate [группы ресурсов](../azure-resource-manager/resource-group-overview.md) в Западной Европе hello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="a1f88-123">Группа ресурсов представляет размещения всех hello вместе, требуется toomanage ресурсы Azure, такие как серверный веб-приложения hello и любой базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a1f88-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="a1f88-124">toosee какие возможные значения следует использовать для `---location`, использовать hello [список расположений az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) команды.</span><span class="sxs-lookup"><span data-stu-id="a1f88-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a1f88-125">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="a1f88-125">Create an App Service plan</span></span>
<span data-ttu-id="a1f88-126">Используйте [создать план служб приложений az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate «B1» [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1f88-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="a1f88-127">План службы приложений — это единица масштабирования, которая может включать любое количество приложений должны tooscale вверх или out вместе over hello же инфраструктуры службы приложений.</span><span class="sxs-lookup"><span data-stu-id="a1f88-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="a1f88-128">Каждый план также имеет свою [ценовую категорию](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a1f88-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="a1f88-129">На более высоких уровнях используется лучшее оборудование и доступны дополнительные функции (например, дополнительные экземпляры масштабирования).</span><span class="sxs-lookup"><span data-stu-id="a1f88-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="a1f88-130">В этом учебнике B1 — hello минимального уровня, который позволяет масштабировать toothree экземпляров.</span><span class="sxs-lookup"><span data-stu-id="a1f88-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="a1f88-131">Приложения всегда можно переместить вверх или вниз hello ценовой категории позже, запустив [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="a1f88-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="a1f88-132">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a1f88-132">Create a web app</span></span>
<span data-ttu-id="a1f88-133">Используйте [создать az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate веб-приложения с уникальным именем в `$appName`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="a1f88-134">Сброс учетных данных развертывания</span><span class="sxs-lookup"><span data-stu-id="a1f88-134">Set deployment credentials</span></span>
<span data-ttu-id="a1f88-135">Используйте [web az appservice пользователь развертывание задан](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset учетные данные развертывания уровня учетной записи для приложения службы.</span><span class="sxs-lookup"><span data-stu-id="a1f88-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="a1f88-136">Настройка развертывания Git</span><span class="sxs-lookup"><span data-stu-id="a1f88-136">Configure Git deployment</span></span>
<span data-ttu-id="a1f88-137">Используйте [web системы управления версиями az appservice config локальной git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure локальное развертывание Git.</span><span class="sxs-lookup"><span data-stu-id="a1f88-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="a1f88-138">Эта команда предоставляет выход, который выглядит как следующий hello:</span><span class="sxs-lookup"><span data-stu-id="a1f88-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="a1f88-139">Используйте hello вернул tooconfigure URL-адрес вашего Git удаленной.</span><span class="sxs-lookup"><span data-stu-id="a1f88-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="a1f88-140">Hello следующая команда использует hello предшествующий пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a1f88-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="a1f88-141">Развертывание примера приложения hello</span><span class="sxs-lookup"><span data-stu-id="a1f88-141">Deploy hello sample application</span></span>
<span data-ttu-id="a1f88-142">Вы являются toodeploy теперь готовы к примеру приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="a1f88-143">Запустите `git push`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="a1f88-144">При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="a1f88-145">Обзор tooAzure веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a1f88-145">Browse tooAzure web app</span></span>
<span data-ttu-id="a1f88-146">Используйте [обзора web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee своего приложения, работающего в режиме реального времени в Azure, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a1f88-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="a1f88-147">Шаг 3 — подключить tooRedis</span><span class="sxs-lookup"><span data-stu-id="a1f88-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="a1f88-148">На этом шаге настраивается кэша Redis для Azure как внешних, размещение кэша tooyour веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f88-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="a1f88-149">Быстро, можно воспользоваться Redis toocache выходные данные страницы.</span><span class="sxs-lookup"><span data-stu-id="a1f88-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="a1f88-150">Кроме того, при дальнейшем масштабировании веб-приложения Redis поможет надежно сохранить пользовательские сеансы в нескольких экземплярах.</span><span class="sxs-lookup"><span data-stu-id="a1f88-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="a1f88-151">Создание кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="a1f88-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="a1f88-152">Используйте [az redis создать](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate кэша Redis для Azure и сохраните hello выходных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="a1f88-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="a1f88-153">Укажите уникальное имя в `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="a1f88-154">Настройка приложения hello toouse Redis</span><span class="sxs-lookup"><span data-stu-id="a1f88-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="a1f88-155">Формат hello строку подключения для вашего кэша.</span><span class="sxs-lookup"><span data-stu-id="a1f88-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="a1f88-156">Вторая строка Hello следует предоставить выход, выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a1f88-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="a1f88-157">В Visual Studio, создайте файл веб-конфигурации в корневом каталоге проекта, который называется `redis.config` и hello вставить следующий код в него.</span><span class="sxs-lookup"><span data-stu-id="a1f88-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="a1f88-158">В `value`, используйте строку подключения hello из hello выходные данные PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1f88-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="a1f88-159">Если взглянуть на hello `.gitignore` файла в репозиторий Git, вы увидите, что этот файл исключен из системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="a1f88-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="a1f88-160">Таким образом ваша конфиденциальная информация находится в безопасности.</span><span class="sxs-lookup"><span data-stu-id="a1f88-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="a1f88-161">Откройте `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-161">Open `Web.config`.</span></span> <span data-ttu-id="a1f88-162">Обратите внимание hello `<appSettings file="redis.config">` элемент, который получает приветствия, созданный в `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="a1f88-163">Найти комментарий hello раздел, содержащий `<sessionState>` и `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="a1f88-164">Раскомментируйте его.</span><span class="sxs-lookup"><span data-stu-id="a1f88-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="a1f88-165">Этот код осуществляет поиск строки подключения Redis hello вы определили в `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="a1f88-166">Теперь приложение использует сеансы toomanage Redis и кэширование.</span><span class="sxs-lookup"><span data-stu-id="a1f88-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="a1f88-167">Тип `F5` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="a1f88-168">При желании вы можете загрузить Redis управления toovisualize hello данные клиента, сохраняется toohello кэша.</span><span class="sxs-lookup"><span data-stu-id="a1f88-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="a1f88-169">Настройка строки подключения hello в Azure</span><span class="sxs-lookup"><span data-stu-id="a1f88-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="a1f88-170">Для toowork вашего приложения в Azure, необходимо tooconfigure hello же строка подключения Redis в Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="a1f88-171">Поскольку `redis.config` не сохраняется в системе управления версиями, не является развернутой tooAzure при выполнении развертывания Git.</span><span class="sxs-lookup"><span data-stu-id="a1f88-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="a1f88-172">Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) строка соединения hello tooadd с hello же имя (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="a1f88-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="a1f88-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a1f88-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="a1f88-174">Следует помнить, что `$connstring` содержит строку подключения в формате hello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="a1f88-175">Повторное развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="a1f88-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="a1f88-176">Использовать ваш tooAzure изменения toopush команды Git</span><span class="sxs-lookup"><span data-stu-id="a1f88-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="a1f88-177">При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="a1f88-178">Обзор toohello веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="a1f88-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="a1f88-179">Используйте [обзора web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) live toosee hello изменения в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f88-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="a1f88-180">Шаг 4 экземпляров toomultiple шкалы.</span><span class="sxs-lookup"><span data-stu-id="a1f88-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="a1f88-181">Hello план служб приложений является hello единица масштабирования для вашего веб-приложениях Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f88-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="a1f88-182">tooscale ожидания веб-приложения, масштабирование hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a1f88-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="a1f88-183">Используйте [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale экземпляров toothree план службы приложений hello, который является hello максимально допустимое hello B1 ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="a1f88-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="a1f88-184">Помните, что B1 hello ценовой категории, выбранные при создании hello ранее план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a1f88-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="a1f88-185">Шаг 5. Развертывание приложения в нескольких регионах</span><span class="sxs-lookup"><span data-stu-id="a1f88-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="a1f88-186">При масштабировании географически, приложение работает в нескольких регионах hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f88-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="a1f88-187">Эта программа установки балансировку нагрузки приложения дальнейшей основанной на географических объектах и сокращает время отклика hello, поместив ближе браузера tooclient приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="a1f88-188">На этом шаге масштабировать ваш ASP.NET web app tooa второй области с [диспетчера трафика Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="a1f88-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="a1f88-189">В конце шага hello hello будет запущен в Западной Европе (уже создан) веб-приложения и веб-приложение работает в Юго-Восточная Азия (еще не создан).</span><span class="sxs-lookup"><span data-stu-id="a1f88-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="a1f88-190">Оба приложения будут обслуживаться из hello же URL-адрес диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="a1f88-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="a1f88-191">Вертикальное масштабирование hello Europe приложения tooStandard уровня</span><span class="sxs-lookup"><span data-stu-id="a1f88-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="a1f88-192">В службе приложений интеграция с диспетчером трафика Azure требует hello ценовой категории Standard.</span><span class="sxs-lookup"><span data-stu-id="a1f88-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="a1f88-193">Используйте [обновление плана служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale копирование вашего tooS1 плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a1f88-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="a1f88-194">Создание профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="a1f88-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="a1f88-195">Используйте [создать профиль диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate диспетчера трафика профиль и добавить его tooyour группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1f88-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="a1f88-196">В параметре $dnsName укажите уникальное DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="a1f88-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="a1f88-197">`--routing-method Performance`Указывает, что этот профиль [направляет трафик пользователя toohello ближайшей конечной точкой](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="a1f88-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="a1f88-198">Получить идентификатор ресурса hello приложение hello Европа</span><span class="sxs-lookup"><span data-stu-id="a1f88-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="a1f88-199">Используйте [Показать web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello идентификатор ресурса веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="a1f88-200">Добавить конечную точку диспетчера трафика для Европы приложение hello</span><span class="sxs-lookup"><span data-stu-id="a1f88-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="a1f88-201">Используйте [создать конечную точку диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour конечной точки профиля диспетчера трафика и используйте идентификатор ресурса hello веб-приложения как hello целевой.</span><span class="sxs-lookup"><span data-stu-id="a1f88-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="a1f88-202">Получить URL-адрес конечной точки диспетчера трафика hello</span><span class="sxs-lookup"><span data-stu-id="a1f88-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="a1f88-203">Профиль диспетчера трафика теперь есть конечная точка, точки tooyour существующего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="a1f88-204">Используйте [Показать профиль диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a1f88-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="a1f88-205">Копировать выходные данные hello в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="a1f88-205">Copy hello output into your browser.</span></span> <span data-ttu-id="a1f88-206">Вы должны снова увидеть свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a1f88-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="a1f88-207">Создание кэша Redis для Azure в Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="a1f88-208">Теперь можно реплицировать региона Azure web app toohello Юго-Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="a1f88-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="a1f88-209">toostart, используйте [az redis создать](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate второй кэш Azure Redis в Юго-Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="a1f88-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="a1f88-210">Этот кэш должен toobe совместного размещения вместе с приложением в Азии.</span><span class="sxs-lookup"><span data-stu-id="a1f88-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="a1f88-211">`--name $cacheName-asia`Имя кэша hello hello кэша Западной Европе с hello hello дает `-asia` суффикс.</span><span class="sxs-lookup"><span data-stu-id="a1f88-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="a1f88-212">Создание плана службы приложений в Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="a1f88-213">Используйте [создать план служб приложений az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate план вторую службу приложения hello юго-восток Азиатско-Тихоокеанский регион, с помощью hello S1 того же уровня как план Западной Европе hello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="a1f88-214">Создание веб-приложения в Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-214">Create a web app in Asia</span></span>
<span data-ttu-id="a1f88-215">Используйте [создать az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate второй веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="a1f88-216">`--name $appName-asia`содержит имя приложения hello приложения hello Западной Европе, hello с hello `-asia` суффикс.</span><span class="sxs-lookup"><span data-stu-id="a1f88-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="a1f88-217">Настройка строки подключения hello для Redis</span><span class="sxs-lookup"><span data-stu-id="a1f88-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="a1f88-218">Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello веб-приложение hello строки подключения для hello кэша Юго-Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="a1f88-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="a1f88-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a1f88-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="a1f88-220">Настройка Git развертывания для приложения hello Азии.</span><span class="sxs-lookup"><span data-stu-id="a1f88-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="a1f88-221">Используйте [web системы управления версиями az appservice config локальной git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure локальное развертывание Git для hello второй веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="a1f88-222">Эта команда предоставляет выход, который выглядит как следующий hello:</span><span class="sxs-lookup"><span data-stu-id="a1f88-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="a1f88-223">Используйте hello вернул tooconfigure URL-адрес второй Git, удаленный для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1f88-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="a1f88-224">Hello следующая команда использует hello предшествующий пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a1f88-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="a1f88-225">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="a1f88-225">Deploy your sample application</span></span>
<span data-ttu-id="a1f88-226">Запустите `git push` toodeploy второй дистанционного Git образец приложения toohello.</span><span class="sxs-lookup"><span data-stu-id="a1f88-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="a1f88-227">При запросе пароля следует использовать hello пароль, указанный вами при запуске `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="a1f88-228">Обзор приложения toohello Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-228">Browse toohello Asia app</span></span>
<span data-ttu-id="a1f88-229">Используйте [обзора web az appservice](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify, динамическая работы вашего приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1f88-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="a1f88-230">Получить идентификатор ресурса hello приложение hello Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="a1f88-231">Используйте [Показать web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello идентификатор ресурса веб-приложения в Юго-Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="a1f88-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="a1f88-232">Добавить конечную точку диспетчера трафика для приложения hello Азии</span><span class="sxs-lookup"><span data-stu-id="a1f88-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="a1f88-233">Используйте [создать конечную точку диспетчера трафика сети az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd второй toohello конечной точки профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="a1f88-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="a1f88-234">Добавление приложений tooweb идентификатор региона</span><span class="sxs-lookup"><span data-stu-id="a1f88-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="a1f88-235">Используйте [обновление az appservice web конфигурации appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd переменной среды для конкретного региона.</span><span class="sxs-lookup"><span data-stu-id="a1f88-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="a1f88-236">Код приложения уже использует этот параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="a1f88-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="a1f88-237">Просмотрите `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a1f88-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="a1f88-238">Готово!</span><span class="sxs-lookup"><span data-stu-id="a1f88-238">Complete!</span></span>

<span data-ttu-id="a1f88-239">Попробуйте URL-адрес hello tooaccess вашего профиля диспетчера трафика с помощью браузеров в разных географических регионах.</span><span class="sxs-lookup"><span data-stu-id="a1f88-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="a1f88-240">В клиентских браузерах в Европе должно отображаться ASP.NET West Europe (ASP.NET, Западная Европа), а в браузерах клиентов из Азии — ASP.NET Southeast Asia (ASP.NET, Юго-Восточная Азия).</span><span class="sxs-lookup"><span data-stu-id="a1f88-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="a1f88-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a1f88-241">More resources</span></span>
