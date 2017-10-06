---
title: "aaaConnect tooAzure приложения MongoDB Cosmos DB с помощью Node.js | Документы Microsoft"
description: "Узнайте, как tooconnect существующих приложений Node.js MongoDB tooAzure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="234f9-103">Azure Cosmos DB. Перемещение имеющегося веб-приложения MongoDB Node.js</span><span class="sxs-lookup"><span data-stu-id="234f9-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="234f9-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="234f9-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="234f9-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="234f9-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="234f9-106">Краткого руководства показано, как существующий toouse [MongoDB](mongodb-introduction.md) приложения, написанные на Node.js и подключите базу данных Azure Cosmos tooyour базы данных, которая поддерживает MongoDB клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="234f9-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="234f9-107">Другими словами приложение Node.js знает только подключение tooa базы данных с помощью интерфейсов API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="234f9-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="234f9-108">Он является прозрачным toohello приложение, которое hello данных хранится в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="234f9-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="234f9-109">После выполнения шагов, описанных в этом руководстве, у вас будет приложение MEAN (MongoDB, Express, AngularJS и Node.js), выполняющееся в [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="234f9-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="234f9-111">Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="234f9-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="234f9-112">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="234f9-113">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="234f9-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="234f9-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="234f9-114">Prerequisites</span></span> 
<span data-ttu-id="234f9-115">В дополнение к этому tooAzure CLI требуется [Node.js](https://nodejs.org/) и [Git](http://www.git-scm.com/downloads) установлены локально toorun `npm` и `git` команд.</span><span class="sxs-lookup"><span data-stu-id="234f9-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="234f9-116">У вас должен быть опыт работы с Node.js.</span><span class="sxs-lookup"><span data-stu-id="234f9-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="234f9-117">Это краткое руководство не предназначено предполагаемого toohelp вы разработка приложений Node.js в целом.</span><span class="sxs-lookup"><span data-stu-id="234f9-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="234f9-118">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="234f9-118">Clone hello sample application</span></span>

<span data-ttu-id="234f9-119">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="234f9-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="234f9-120">Выполните следующие команды tooclone hello образец репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="234f9-121">Этот образец репозиторий содержит по умолчанию hello [MEAN.js](http://meanjs.org/) приложения.</span><span class="sxs-lookup"><span data-stu-id="234f9-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="234f9-122">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="234f9-122">Run hello application</span></span>

<span data-ttu-id="234f9-123">Установка hello необходимые пакеты и запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="234f9-124">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="234f9-124">Log in tooAzure</span></span>

<span data-ttu-id="234f9-125">При использовании установленных Azure CLI вход tooyour подписки Azure с hello [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="234f9-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="234f9-126">Этот шаг можно пропустить, если вы используете hello оболочки облако Azure.</span><span class="sxs-lookup"><span data-stu-id="234f9-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="234f9-127">Добавить модуль Azure Cosmos DB hello</span><span class="sxs-lookup"><span data-stu-id="234f9-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="234f9-128">Если вы используете установленных Azure CLI, проверьте toosee, если hello `cosmosdb` компонент уже установлен, выполнив hello `az` команды.</span><span class="sxs-lookup"><span data-stu-id="234f9-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="234f9-129">Если `cosmosdb` — в hello список базовых команд, продолжить toohello следующей команды.</span><span class="sxs-lookup"><span data-stu-id="234f9-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="234f9-130">Этот шаг можно пропустить, если вы используете hello оболочки облако Azure.</span><span class="sxs-lookup"><span data-stu-id="234f9-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="234f9-131">Если `cosmosdb` не в hello список базовых команд, переустановите [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="234f9-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="234f9-132">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="234f9-132">Create a resource group</span></span>

<span data-ttu-id="234f9-133">Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="234f9-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="234f9-134">Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (веб-приложений, баз данных и учетных записей хранения) и управление ими.</span><span class="sxs-lookup"><span data-stu-id="234f9-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="234f9-135">Hello следующий пример создает группу ресурсов в Западной Европе hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="234f9-136">Выберите уникальное имя для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="234f9-137">При использовании оболочки облако Azure щелкните **попробовать**, выполните toologin указаниям, появляющимся на экране приветствия, а затем скопируйте hello команду в командную строку hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="234f9-138">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="234f9-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="234f9-139">Создать учетную запись Azure Cosmos DB с hello [az cosmosdb создать](/cli/azure/cosmosdb#create) команды.</span><span class="sxs-lookup"><span data-stu-id="234f9-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="234f9-140">В hello выполните следующую команду, заменить собственные уникальное имя учетной записи Azure Cosmos DB, показывающий hello `<cosmosdb-name>` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="234f9-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="234f9-141">Это уникальное имя будет использоваться как часть конечной точки Azure Cosmos DB (`https://<cosmosdb-name>.documents.azure.com/`), поэтому hello имя должно toobe уникальным для всех учетных записей Azure Cosmos DB в Azure.</span><span class="sxs-lookup"><span data-stu-id="234f9-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="234f9-142">Hello `--kind MongoDB` обеспечивает MongoDB клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="234f9-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="234f9-143">При создании учетной записи Azure Cosmos DB hello hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="234f9-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="234f9-144">В этом примере JSON как формат вывода hello Azure CLI, он по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="234f9-145">toouse другой выходной формат см. в разделе [выходных форматов для команд CLI Azure 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="234f9-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="234f9-146">Подключение базы данных приложения toohello Node.js</span><span class="sxs-lookup"><span data-stu-id="234f9-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="234f9-147">На этом шаге подключиться MEAN.js образец приложения tooan Azure Cosmos DB базы данных только что созданный, используя строку подключения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="234f9-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="234f9-148">Настройка строки подключения hello в приложении Node.js</span><span class="sxs-lookup"><span data-stu-id="234f9-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="234f9-149">В репозитории MEAN.js откройте `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="234f9-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="234f9-150">Замените содержимое этого файла hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="234f9-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="234f9-151">Убедитесь, что tooalso замените hello двух `<cosmosdb-name>` местозаполнителей Azure Cosmos DB имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="234f9-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="234f9-152">Получить ключ hello</span><span class="sxs-lookup"><span data-stu-id="234f9-152">Retrieve hello key</span></span>

<span data-ttu-id="234f9-153">В базе данных Azure Cosmos DB tooan tooconnect заказа необходим ключ hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="234f9-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="234f9-154">Используйте hello [список ключей az cosmosdb](/cli/azure/cosmosdb#list-keys) команда tooretrieve hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="234f9-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="234f9-155">Hello Azure CLI выводит toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="234f9-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="234f9-156">Скопируйте значение hello `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="234f9-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="234f9-157">Вставить это над hello `<primary_master_key>` в `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="234f9-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="234f9-158">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="234f9-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="234f9-159">Запустите приложение hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="234f9-159">Run hello application again.</span></span>

<span data-ttu-id="234f9-160">Еще раз запустите `npm start`.</span><span class="sxs-lookup"><span data-stu-id="234f9-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="234f9-161">Сообщения консоли теперь должен сообщить вам что этой среды разработки hello запущен и работает.</span><span class="sxs-lookup"><span data-stu-id="234f9-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="234f9-162">Перейдите в слишком`http://localhost:3000` в браузере.</span><span class="sxs-lookup"><span data-stu-id="234f9-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="234f9-163">Нажмите кнопку **зарегистрироваться** в верхнем меню и попробуйте toocreate hello два пустой пользователей.</span><span class="sxs-lookup"><span data-stu-id="234f9-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="234f9-164">MEAN.js пример приложения Hello хранятся данные пользователя в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="234f9-165">Если вы успешно и MEAN.js автоматически входит в hello создан пользователем, а затем подключение к базе данных Azure Cosmos работает.</span><span class="sxs-lookup"><span data-stu-id="234f9-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js успешно подключается tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="234f9-167">Просмотр данных в обозревателе данных</span><span class="sxs-lookup"><span data-stu-id="234f9-167">View data in Data Explorer</span></span>

<span data-ttu-id="234f9-168">Данные, хранящиеся в Azure Cosmos DB включена доступных tooview, запроса и выполнения бизнес логики в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="234f9-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="234f9-169">tooview, запрос и работать с данными пользователя hello на предыдущем шаге hello, toohello входа [портал Azure](https://portal.azure.com) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="234f9-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="234f9-170">В верхнем поле поиска hello введите Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="234f9-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="234f9-171">Когда откроется колонка учетной записи Cosmos DB, выберите свою учетную запись Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="234f9-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="234f9-172">В hello навигации слева выберите обозреватель данных.</span><span class="sxs-lookup"><span data-stu-id="234f9-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="234f9-173">Разверните коллекции в области коллекций hello и затем можно просматривать документы hello в коллекции hello, запроса данных hello и даже создать и выполнить хранимые процедуры, триггеры и определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="234f9-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Обозреватель данных в hello портал Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="234f9-175">Развертывание приложения tooAzure hello Node.js</span><span class="sxs-lookup"><span data-stu-id="234f9-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="234f9-176">На этом шаге развертывания вашего tooAzure приложение Node.js подключен MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="234f9-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="234f9-177">Возможно, вы заметили это файл конфигурации hello ранее измененного для среды разработки hello (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="234f9-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="234f9-178">При развертывании вашего приложения tooApp службы, он будет выполняться в hello рабочей среде по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="234f9-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="234f9-179">Поэтому теперь требуется toomake hello же изменить файл toohello соответствующей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="234f9-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="234f9-180">В репозитории MEAN.js откройте `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="234f9-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="234f9-181">В hello `db` объекта, замените значение hello `uri` как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="234f9-182">Быть убедиться, что заполнители hello tooreplace как до.</span><span class="sxs-lookup"><span data-stu-id="234f9-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="234f9-183">Hello `ssl=true` возможность важна поскольку [Azure Cosmos DB требуется протокол SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="234f9-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="234f9-184">В терминалов hello сохраните все изменения в Git.</span><span class="sxs-lookup"><span data-stu-id="234f9-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="234f9-185">Обе команды toorun можно скопировать их вместе.</span><span class="sxs-lookup"><span data-stu-id="234f9-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="234f9-186">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="234f9-186">Clean up resources</span></span>

<span data-ttu-id="234f9-187">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="234f9-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="234f9-188">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="234f9-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="234f9-189">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="234f9-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="234f9-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="234f9-190">Next steps</span></span>

<span data-ttu-id="234f9-191">В этом кратком руководстве вы узнали, каким образом toocreate Cosmos Azure DB учетной записи и создать коллекцию MongoDB с использованием hello обозреватель данных.</span><span class="sxs-lookup"><span data-stu-id="234f9-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="234f9-192">Теперь можно перенести на tooAzure данных MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="234f9-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="234f9-193">Перенос данных в DocumentDB с помощью mongoimport и mongorestore</span><span class="sxs-lookup"><span data-stu-id="234f9-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
