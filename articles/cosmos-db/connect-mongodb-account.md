---
title: "Строка подключения MongoDB для учетной записи Azure Cosmos DB | Документация Майкрософт"
description: "Здесь содержатся сведения о подключении приложения MongoDB к учетной записи Azure Cosmos DB с помощью строки подключения MongoDB."
keywords: "строка подключения MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="26493-104">Подключение приложения MongoDB к Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="26493-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="26493-105">Здесь содержатся сведения о подключении приложения MongoDB к учетной записи Azure Cosmos DB с помощью строки подключения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="26493-106">Вы сможете использовать базу данных Azure Cosmos DB в качестве хранилища данных для приложения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="26493-107">В этом руководстве описаны два способа получения строки подключения.</span><span class="sxs-lookup"><span data-stu-id="26493-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="26493-108">[Метод "Быстрый запуск"](#QuickstartConnection) для использования с драйверами .NET, Node.js, Java, Python или оболочкой MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="26493-109">[Метод с использованием пользовательской строки подключения](#GetCustomConnection) для других драйверов.</span><span class="sxs-lookup"><span data-stu-id="26493-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26493-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="26493-110">Prerequisites</span></span>

- <span data-ttu-id="26493-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="26493-111">An Azure account.</span></span> <span data-ttu-id="26493-112">Если у вас нет учетной записи, вы можете создать [бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="26493-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="26493-113">Учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="26493-114">Инструкции см. в статье [Azure Cosmos DB. Создание веб-приложения API MongoDB с использованием языка .NET и портала Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="26493-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="26493-115"><a id="QuickstartConnection"></a>Получение строки подключения MongoDB с помощью метода быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="26493-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="26493-116">В браузере войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26493-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="26493-117">В колонке **Azure Cosmos DB** выберите API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="26493-118">В левой панели в колонке учетной записи щелкните **Быстрый запуск**.</span><span class="sxs-lookup"><span data-stu-id="26493-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="26493-119">Выберите платформу (**.NET**, **Node.js**, **оболочка MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="26493-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="26493-120">Если соответствующего драйвера или средства нет в списке, не беспокойтесь, мы постоянно добавляем дополнительные фрагменты кода для подключения.</span><span class="sxs-lookup"><span data-stu-id="26493-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="26493-121">Оставьте в конце статьи свои комментарии о том, что, по вашему мнению, нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="26493-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="26493-122">Дополнительные сведения о том, как создавать собственное подключение, см.в разделе [Получение строки подключения MongoDB для настройки](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="26493-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="26493-123">Скопируйте и вставьте фрагмент кода в приложение MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Колонка "Быстрый запуск"](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="26493-125"><a id="GetCustomConnection"></a> Получение строки подключения MongoDB для настройки</span><span class="sxs-lookup"><span data-stu-id="26493-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="26493-126">В браузере войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26493-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="26493-127">В колонке **Azure Cosmos DB** выберите API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="26493-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="26493-128">На левой панели в колонке учетной записи щелкните **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="26493-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="26493-129">Откроется колонка **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="26493-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="26493-130">Она содержит все необходимые сведения для подключения к учетной записи с помощью драйвера для MongoDB, включая автоматически сформированную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="26493-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Колонка "Строка подключения"](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="26493-132">Требования к строке подключения</span><span class="sxs-lookup"><span data-stu-id="26493-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="26493-133">В Azure Cosmos DB строгие требования к безопасности и стандарты.</span><span class="sxs-lookup"><span data-stu-id="26493-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="26493-134">Для всех учетных записей Azure Cosmos DB требуется проверка подлинности и безопасный обмен данными через *SSL*.</span><span class="sxs-lookup"><span data-stu-id="26493-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="26493-135">Azure Cosmos DB поддерживает стандартный формат универсального кода ресурса для строки подключения MongoDB, налагая пару дополнительных условий. Для учетных записей Azure Cosmos DB требуется использовать проверку подлинности и безопасный обмен данными через SSL.</span><span class="sxs-lookup"><span data-stu-id="26493-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="26493-136">В этом случае строка подключения имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="26493-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="26493-137">Значения для этой строки можно найти в колонке **Строка подключения**, как показано выше:</span><span class="sxs-lookup"><span data-stu-id="26493-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="26493-138">Имя пользователя (обязательно): имя учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="26493-139">Пароль (обязательно): пароль для учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="26493-140">Узел (обязательно): полное доменное имя учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="26493-141">Порт (обязательно): 10255.</span><span class="sxs-lookup"><span data-stu-id="26493-141">Port (required): 10255.</span></span>
* <span data-ttu-id="26493-142">База данных (необязательно): база данных, используемая для подключения.</span><span class="sxs-lookup"><span data-stu-id="26493-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="26493-143">Если база данных не указана, база данных по умолчанию — test.</span><span class="sxs-lookup"><span data-stu-id="26493-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="26493-144">ssl=true (обязательно)</span><span class="sxs-lookup"><span data-stu-id="26493-144">ssl=true (required)</span></span>

<span data-ttu-id="26493-145">Рассмотрим в качестве примера учетную запись, сведения о которой приведены выше в колонке **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="26493-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="26493-146">Допустимая строка подключения:</span><span class="sxs-lookup"><span data-stu-id="26493-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="26493-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26493-147">Next steps</span></span>
* <span data-ttu-id="26493-148">Узнайте, как [использовать MongoChef](mongodb-mongochef.md) с учетной записью API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="26493-149">Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="26493-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
