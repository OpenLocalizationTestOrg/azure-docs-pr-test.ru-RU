---
title: "aaaBuild Node.js и MongoDB веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как tooget приложение Node.js в Azure, с tooa подключения Cosmos DB базы данных со строкой соединения MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="5f7ab-103">Разработка веб-приложения на основе Node.js и MongoDB в Azure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="5f7ab-104">Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5f7ab-105">В этом учебнике показано, как веб-приложения в Azure и подключить его базы данных MongoDB tooa toocreate Node.js.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="5f7ab-106">После выполнения действий, описанных в этом руководстве, у вас появится приложение MEAN (MongoDB, Express, AngularJS и Node.js), выполняющееся в [службе приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="5f7ab-107">Для простоты примера приложения hello используется hello [MEAN.js веб-платформа](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="5f7ab-109">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f7ab-110">Создание базы данных MongoDB в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="5f7ab-111">Подключение tooMongoDB приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="5f7ab-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="5f7ab-112">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5f7ab-113">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5f7ab-114">Потоковая передача журналов диагностики из Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="5f7ab-115">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f7ab-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5f7ab-116">Prerequisites</span></span>

<span data-ttu-id="5f7ab-117">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-117">toocomplete this tutorial:</span></span>

1. <span data-ttu-id="5f7ab-118">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="5f7ab-118">[Install Git](https://git-scm.com/)</span></span>
1. <span data-ttu-id="5f7ab-119">[установите Node.j и NPM](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-119">[Install Node.js and NPM](https://nodejs.org/)</span></span>
1. <span data-ttu-id="5f7ab-120">[Gulp.js](http://gulpjs.com/) (требуется для [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started));</span><span class="sxs-lookup"><span data-stu-id="5f7ab-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. <span data-ttu-id="5f7ab-121">[Установите и запустите MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-121">[Install and run MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/)</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5f7ab-122">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5f7ab-123">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5f7ab-124">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="5f7ab-125">Проверка локальной базы данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f7ab-125">Test local MongoDB</span></span>

<span data-ttu-id="5f7ab-126">Hello откройте окно терминала и `cd` toohello `bin` каталог установки MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="5f7ab-127">Можно использовать это окно терминала toorun hello команды в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="5f7ab-128">Запустите `mongo` hello терминалов tooconnect tooyour локальном сервере, MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="5f7ab-129">Если подключение успешно установлено, это означает, что локальная база данных MongoDB запущена.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="5f7ab-130">В противном случае убедитесь, что локальной базы данных MongoDB запущена с hello процедуры, описанной в [установить MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="5f7ab-131">Часто MongoDB установлена, но по-прежнему нужна toostart его, выполнив `mongod`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="5f7ab-132">После завершения тестирования базы данных MongoDB, введите `Ctrl+C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="5f7ab-133">Создание локального приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="5f7ab-133">Create local Node.js app</span></span>

<span data-ttu-id="5f7ab-134">На этом шаге настраивается hello локального проекта Node.js.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="5f7ab-135">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="5f7ab-135">Clone hello sample application</span></span>

<span data-ttu-id="5f7ab-136">В окне терминала hello `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="5f7ab-137">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="5f7ab-138">Этот образец репозиторий содержит копию hello [MEAN.js репозитория](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="5f7ab-139">Это измененный toorun на службы приложений (Дополнительные сведения см. в разделе репозитория hello MEAN.js [файл README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="5f7ab-140">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-140">Run hello application</span></span>

<span data-ttu-id="5f7ab-141">Выполните следующие команды tooinstall hello необходимые пакеты hello и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="5f7ab-142">После полной загрузки приложение hello, вы увидите нечто похожее toohello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="5f7ab-143">Перейдите toohttp://localhost:3000 в браузере.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="5f7ab-144">Нажмите кнопку **зарегистрироваться** в верхнем меню hello и Создание тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="5f7ab-145">MEAN.js пример приложения Hello хранятся данные пользователя в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="5f7ab-146">Если не возникает при создании пользователя, и вход в приложение записи базы данных локального MongoDB данных toohello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js успешно подключается tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="5f7ab-148">Выберите **администрирования > Управление статьи** tooadd некоторые статьи.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="5f7ab-149">toostop Node.js в любой момент нажмите `Ctrl+C` в hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="5f7ab-150">Создание рабочей базы данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f7ab-150">Create production MongoDB</span></span>

<span data-ttu-id="5f7ab-151">На этом шаге вы создадите базу данных MongoDB в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="5f7ab-152">Когда приложение будет развернутой tooAzure, база данных облака используется.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="5f7ab-153">В качестве MongoDB в этом руководстве используется [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="5f7ab-154">Cosmos DB поддерживает подключения клиентов MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5f7ab-155">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-155">Log in tooAzure</span></span>

<span data-ttu-id="5f7ab-156">Вы будете использовать приложение toohost ресурсы, необходимые для hello toocreate hello Azure CLI 2.0 в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="5f7ab-157">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="5f7ab-158">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5f7ab-158">Create a resource group</span></span>

<span data-ttu-id="5f7ab-159">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="5f7ab-160">Hello следующий пример создает группу ресурсов в Западной Европе hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="5f7ab-161">Используйте hello [список расположений az appservice](/cli/azure/appservice#list-locations) Azure CLI команды toolist доступных расположений.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="5f7ab-162">Создание учетной записи Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5f7ab-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="5f7ab-163">Создать учетную запись Cosmos DB с hello [az cosmosdb создать](/cli/azure/cosmosdb#create) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="5f7ab-164">Hello следующую команду, подставьте уникальное имя для hello Cosmos DB  *\<cosmosdb_name >* заполнителя.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="5f7ab-165">Это имя используется в рамках hello hello Cosmos DB конечной точки, `https://<cosmosdb_name>.documents.azure.com/`, поэтому hello имя должно toobe уникальный всех учетных записей, Cosmos DB в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="5f7ab-166">Hello имя должно содержать только строчные буквы, цифры и знак дефиса (-) hello и должен находиться в диапазоне от 3 до 50 символов.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="5f7ab-167">Hello *--kind MongoDB* обеспечивает MongoDB клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="5f7ab-168">При создании hello учетной записи Cosmos DB hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="5f7ab-169">Подключение приложения tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f7ab-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="5f7ab-170">На этом шаге подключиться MEAN.js образец приложения toohello Cosmos DB базы данных только что созданный, используя строку подключения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="5f7ab-171">Получить ключ hello базы данных</span><span class="sxs-lookup"><span data-stu-id="5f7ab-171">Retrieve hello database key</span></span>

<span data-ttu-id="5f7ab-172">tooconnect toohello Cosmos DB базы данных, необходим ключ hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="5f7ab-173">Используйте hello [список ключей az cosmosdb](/cli/azure/cosmosdb#list-keys) команда tooretrieve hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="5f7ab-174">Hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Скопируйте значение hello `primaryMasterKey`. <span data-ttu-id="5f7ab-176">Эти сведения в следующем шаге hello необходимы.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="5f7ab-177">Настройка строки подключения hello в приложении Node.js</span><span class="sxs-lookup"><span data-stu-id="5f7ab-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="5f7ab-178">В репозитории MEAN.js откройте файл _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="5f7ab-179">В hello `db` объекта, обновите значение hello `uri`:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="5f7ab-180">Замените hello двух  *\<cosmosdb_name >* местозаполнителей Cosmos DB имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="5f7ab-181">Замените hello  *\<primary_master_key >* заполнитель с ключом hello, скопированным на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="5f7ab-182">Hello код отображает hello `db` объекта:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="5f7ab-183">Hello `ssl=true` параметр является обязательным, поскольку [Cosmos DB необходим протокол SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="5f7ab-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="5f7ab-184">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="5f7ab-185">Тестирование приложения hello в рабочий режим</span><span class="sxs-lookup"><span data-stu-id="5f7ab-185">Test hello application in production mode</span></span> 

<span data-ttu-id="5f7ab-186">Выполните следующие команды toominify и пакет скриптов для производственной среды hello hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="5f7ab-187">Этот процесс создает hello файлов, необходимых hello рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="5f7ab-188">Выполнения hello, следующая команда toouse hello строку соединения, то в _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="5f7ab-189">`NODE_ENV=production`Задает переменную среды hello, которая сообщает Node.js toorun в рабочей среде hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="5f7ab-190">`node server.js`Здравствуйте, запускает сервер Node.js с `server.js` в корне репозитория.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="5f7ab-191">Так приложение Node.js загружается в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="5f7ab-192">При загрузке приложения hello, проверьте, выполняется в рабочей среде hello toomake:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="5f7ab-193">Перейдите toohttp://localhost:8443 в браузере.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="5f7ab-194">Нажмите кнопку **зарегистрироваться** в верхнем меню hello и Создание тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="5f7ab-195">Если успешного создания пользователя и выполните вход, приложение производит запись данных toohello Cosmos DB в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="5f7ab-196">В hello терминалов остановить Node.js, введя команду `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="5f7ab-197">Развертывание приложения tooAzure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-197">Deploy app tooAzure</span></span>

<span data-ttu-id="5f7ab-198">На этом шаге развертывания вашего tooAzure приложений Node.js подключен MongoDB службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5f7ab-199">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="5f7ab-199">Create an App Service plan</span></span>

<span data-ttu-id="5f7ab-200">Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="5f7ab-201">Hello следующий пример создает план службы приложений с именем _myAppServicePlan_ с помощью hello **FREE** ценовой категории:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="5f7ab-202">При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="5f7ab-203">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="5f7ab-203">Create a web app</span></span>

<span data-ttu-id="5f7ab-204">Создание веб-приложения в hello `myAppServicePlan` план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="5f7ab-205">Предоставляет приложение Hello веб вы размещения пространство toodeploy кода и предоставляет URL-адрес для вас tooview hello развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="5f7ab-206">Используйте toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="5f7ab-207">Hello следующую команду, замените hello  *\<имя_приложения >* заполнитель с именем уникальный приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="5f7ab-208">Это имя используется как часть URL-адрес по умолчанию hello в hello для веб-приложения hello, поэтому hello имя должно toobe уникальным для всех приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="5f7ab-209">При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="5f7ab-210">Настройка переменной среды</span><span class="sxs-lookup"><span data-stu-id="5f7ab-210">Configure an environment variable</span></span>

<span data-ttu-id="5f7ab-211">Ранее в hello учебник, вы жестко закодировано hello строку подключения базы данных в _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="5f7ab-212">В соответствии с концепцией рекомендации по безопасности требуется tookeep конфиденциальные данные из своего репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="5f7ab-213">При запуске приложения в Azure строка подключения будет храниться в переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="5f7ab-214">В службе приложений устанавливаются переменные среды, как _параметры приложения_ с помощью hello [обновление конфигурации appsettings az webapp](/cli/azure/webapp/config/appsettings#update) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="5f7ab-215">Hello следующий пример настраивает `MONGODB_URI` параметр приложения в Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="5f7ab-216">Замените hello  *\<имя_приложения >*,  *\<cosmosdb_name >*, и  *\<primary_master_key >* заполнители.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="5f7ab-217">В коде Node.js для доступа к этому параметру приложения, как и к любой переменной среды, используется `process.env.MONGODB_URI`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="5f7ab-218">Теперь можно отмените вашей too_config/env/production.js_ изменения с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="5f7ab-219">Повторно откройте файл _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="5f7ab-220">Обратите внимание, приложение hello MEAN.js по умолчанию уже настроенного toouse hello `MONGODB_URI` созданной переменной среды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="5f7ab-221">Настройка локального развертывания Git</span><span class="sxs-lookup"><span data-stu-id="5f7ab-221">Configure local git deployment</span></span> 

<span data-ttu-id="5f7ab-222">Используйте hello [набора пользователей для развертывания веб-приложения az](/cli/azure/webapp/deployment/user#set) команды toocreate учетные данные для развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="5f7ab-223">Вы можете развернуть tooAzure вашего приложения службы приложений, различными способами, включая FTP, local Git, GitHub, Visual Studio Team Services и BitBucket.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="5f7ab-224">Для FTP и local Git, не нужны toohave пользователя развертывания на сервер tooauthenticate hello развертывание настроено.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="5f7ab-225">Этот пользователь развертывания уровня учетной записи, которая отличается от учетной записи подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="5f7ab-226">Требуется только tooconfigure этого пользователя развертывания один раз.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="5f7ab-227">В hello следующую команду, замените  *\<имя пользователя >* и  *\<пароль >* новое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="5f7ab-228">Hello имя пользователя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-228">hello user name must be unique.</span></span> <span data-ttu-id="5f7ab-229">Hello пароль должен содержать по крайней мере 8 символов, с двумя hello следующие три элемента: буквы, цифры, символы.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="5f7ab-230">Если вы получаете ` 'Conflict'. Details: 409` ошибки, имя пользователя изменить hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="5f7ab-231">Если появляется сообщение об ошибке ` 'Bad Request'. Details: 400`, используйте более надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="5f7ab-232">Запись hello имя пользователя и пароль для использования в последующих шагах, при развертывании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="5f7ab-233">Используйте hello [развертывания источника az webapp config локальной git](/cli/azure/webapp/deployment/source#config-local-git) команда tooconfigure локальный Git доступа toohello веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="5f7ab-234">При настройке пользователя развертывания hello hello Azure CLI показаны hello следующая формата URL-адрес развертывания hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="5f7ab-235">Копировать выходные данные терминалов hello hello, как будет использоваться в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="5f7ab-236">Отправлять tooAzure из Git</span><span class="sxs-lookup"><span data-stu-id="5f7ab-236">Push tooAzure from Git</span></span>

<span data-ttu-id="5f7ab-237">Добавьте локальный tooyour Azure удаленный репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="5f7ab-238">Принудительно toohello Azure удаленный toodeploy приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="5f7ab-239">Появится для hello пароль введен ранее в процессе создания hello hello пользователя развертывания.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="5f7ab-240">Во время развертывания служба приложений Azure будет взаимодействовать с Git.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="5f7ab-241">Вы можете заметить, что выполняется процесс развертывания hello [Gulp](http://gulpjs.com/) после `npm install`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="5f7ab-242">Службы приложений не выполняет Gulp или Grunt задач во время развертывания, поэтому этот репозиторий образец содержит два дополнительных файлов в его корневой каталог tooenable:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="5f7ab-243">_.Deployment_ -это файл указывает toorun службы приложений `bash deploy.sh` как hello пользовательские сценарии.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="5f7ab-244">_Deploy.sh_ -hello пользовательские сценарии.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="5f7ab-245">При просмотре файла hello, вы увидите, что он работает `gulp prod` после `npm install` и `bower install`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="5f7ab-246">Можно использовать этот подход tooadd tooyour любой шаг развертывания на основе Git.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="5f7ab-247">При перезапуске веб-приложения Azure в любой момент времени служба приложений не перезапускает эти задачи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="5f7ab-248">Обзор toohello веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="5f7ab-249">Обзор toohello развертывания веб-приложения с помощью веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="5f7ab-250">Нажмите кнопку **зарегистрироваться** в hello в верхнем меню, а также создать пустой.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="5f7ab-251">Если вы выполняются успешно, и приложение hello автоматически регистрируется в toohello создается пользователь, а затем MEAN.js приложения в Azure имеет базу данных MongoDB (Cosmos DB) toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="5f7ab-253">Выберите **администрирования > Управление статьи** tooadd некоторые статьи.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="5f7ab-254">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="5f7ab-254">**Congratulations!**</span></span> <span data-ttu-id="5f7ab-255">Вы запустили управляемое данными приложение Node.js в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="5f7ab-256">Обновление модели данных и повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="5f7ab-256">Update data model and redeploy</span></span>

<span data-ttu-id="5f7ab-257">На этом этапе вы измените hello `article` данных модели и публикация вашего tooAzure изменений.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="5f7ab-258">Обновление модели данных hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-258">Update hello data model</span></span>

<span data-ttu-id="5f7ab-259">Откройте файл _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="5f7ab-260">В `ArticleSchema` добавьте тип `String` с именем `comment`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="5f7ab-261">Когда все будет готово, код схемы должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a><span data-ttu-id="5f7ab-262">Обновление кода hello статей</span><span class="sxs-lookup"><span data-stu-id="5f7ab-262">Update hello articles code</span></span>

<span data-ttu-id="5f7ab-263">Обновить hello остальной части вашего `articles` кода toouse `comment`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="5f7ab-264">Существует пять файлов необходимо toomodify: hello server контроллера и представления hello четырех клиентов.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="5f7ab-265">Откройте файл _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="5f7ab-266">В hello `update` функцию, добавьте назначение для `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="5f7ab-267">Hello код отображает hello завершения `update` функции:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="5f7ab-268">Откройте файл _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="5f7ab-269">Перед закрывающей hello `</section>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="5f7ab-270">Откройте файл _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="5f7ab-271">Перед закрывающей hello `</a>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="5f7ab-272">Откройте файл _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="5f7ab-273">Внутри hello `<div class="list-group">` элемент и перед закрывающей hello `</a>` , добавьте следующие строки toodisplay hello `comment` вместе с rest hello hello данных статьи:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="5f7ab-274">Откройте файл _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="5f7ab-275">Найти hello `<div class="form-group">` элемент, содержащий hello кнопки "Отправить", которая выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="5f7ab-276">Непосредственно над этот тег добавьте еще один `<div class="form-group">` элемент, который позволит пользователям редактировать hello `comment` поля.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="5f7ab-277">Новый элемент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="5f7ab-278">Проверьте изменения локально.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-278">Test your changes locally</span></span>

<span data-ttu-id="5f7ab-279">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-279">Save all your changes.</span></span>

<span data-ttu-id="5f7ab-280">Проверьте изменения в рабочем режиме.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="5f7ab-281">Следует помнить, что ваш _config/env/production.js_ была отменена и hello `MONGODB_URI` только задана переменная среды в Azure веб-приложения, а не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="5f7ab-282">Если взглянуть на файл конфигурации hello обнаружится, что hello рабочую конфигурацию по умолчанию toouse локальной базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="5f7ab-283">Это гарантирует, что при локальном тестировании изменений кода рабочие данные не будут затронуты.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="5f7ab-284">Перейдите в слишком`http://localhost:8443` в браузере и убедитесь в том, что вы выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="5f7ab-285">Выберите **администрирования > Управление статьи**, затем добавьте статью, выбрав hello  **+**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="5f7ab-286">Вы видите hello новый `Comment` теперь текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-286">You see hello new `Comment` textbox now.</span></span>

![Добавлен комментарий tooArticles поля](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="5f7ab-288">В hello терминалов остановить Node.js, введя команду `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="5f7ab-289">Публикация изменений tooAzure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-289">Publish changes tooAzure</span></span>

<span data-ttu-id="5f7ab-290">Фиксация изменений в Git, то принудительная tooAzure изменения кода hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="5f7ab-291">Здравствуйте, один раз `git push` завершения, перейдите tooyour веб-приложение Azure и испытать новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![TooAzure опубликованы изменения в модель и база данных](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="5f7ab-293">Если вы добавляли статьи ранее, то вы увидите, что они по-прежнему отображаются.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="5f7ab-294">Существующие данные в Cosmos DB не теряются.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="5f7ab-295">Кроме того, схема данных toohello обновлений и оставляет без изменений существующих данных.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="5f7ab-296">Потоковая передача журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="5f7ab-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="5f7ab-297">Во время работы приложения Node.js в службе приложений Azure, вы можете получить tooyour выведенной журналы консоли hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="5f7ab-298">Таким образом, можно получить hello же диагностические сообщения toohelp отладке ошибок приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="5f7ab-299">Журнал toostart потоковой передачи, используйте hello [заключительного фрагмента журнала webapp az](/cli/azure/webapp/log#tail) команды.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="5f7ab-300">После запуска потоковой передачи журнала обновления Azure веб-приложения в браузере tooget hello некоторые веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="5f7ab-301">Теперь отображается журналы консоли по конвейеру tooyour терминала.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="5f7ab-302">Чтобы в любое время отменить потоковую передачу журналов, введите `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="5f7ab-303">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-303">Manage your Azure web app</span></span>

<span data-ttu-id="5f7ab-304">Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="5f7ab-305">Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="5f7ab-307">По умолчанию hello портал отображает веб-приложения **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="5f7ab-308">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="5f7ab-309">Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="5f7ab-310">Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="5f7ab-312">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f7ab-312">Next steps</span></span>

<span data-ttu-id="5f7ab-313">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5f7ab-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f7ab-314">Создание базы данных MongoDB в Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="5f7ab-315">Подключение tooMongoDB приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="5f7ab-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="5f7ab-316">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="5f7ab-317">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="5f7ab-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="5f7ab-318">Журналы Azure tooyour терминалов потока</span><span class="sxs-lookup"><span data-stu-id="5f7ab-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="5f7ab-319">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5f7ab-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="5f7ab-320">Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f7ab-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="5f7ab-321">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="5f7ab-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
