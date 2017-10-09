---
title: "Строка подключения aaaMongoDB для учетной записи Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как tooconnect tooan приложения вашей MongoDB Azure Cosmos DB записи с помощью строки подключения MongoDB."
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="34b4f-104">Подключение tooAzure приложения MongoDB Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="34b4f-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="34b4f-105">Узнайте, как tooconnect tooan приложения вашей MongoDB Azure Cosmos DB записи с помощью строки подключения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="34b4f-106">Затем можно использовать базу данных Azure Cosmos DB как hello данные хранилища для приложения MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="34b4f-107">Этот учебник предлагает два способа tooretrieve данные строки подключения:</span><span class="sxs-lookup"><span data-stu-id="34b4f-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="34b4f-108">[метод start Hello быстрого](#QuickstartConnection), для использования с драйверами .NET, Node.js, MongoDB оболочки, Java и Python</span><span class="sxs-lookup"><span data-stu-id="34b4f-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="34b4f-109">[Здравствуйте, метод строк пользовательского подключения](#GetCustomConnection), для использования с другими драйверами</span><span class="sxs-lookup"><span data-stu-id="34b4f-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34b4f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="34b4f-110">Prerequisites</span></span>

- <span data-ttu-id="34b4f-111">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="34b4f-111">An Azure account.</span></span> <span data-ttu-id="34b4f-112">Если у вас нет учетной записи, вы можете создать [бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="34b4f-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="34b4f-113">Учетная запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="34b4f-114">Инструкции см. в разделе [построения MongoDB API веб-приложения с помощью .NET и hello портал Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="34b4f-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="34b4f-115"><a id="QuickstartConnection"></a>Получить строку подключения hello MongoDB с помощью быстрого запуска hello</span><span class="sxs-lookup"><span data-stu-id="34b4f-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="34b4f-116">В веб-браузере вход toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34b4f-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34b4f-117">В hello **Azure Cosmos DB** колонке выберите hello API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="34b4f-118">Hello левой части колонки hello учетной записи, нажмите кнопку **краткого**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="34b4f-119">Выберите платформу (**.NET**, **Node.js**, **оболочка MongoDB**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="34b4f-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="34b4f-120">Если соответствующего драйвера или средства нет в списке, не беспокойтесь, мы постоянно добавляем дополнительные фрагменты кода для подключения.</span><span class="sxs-lookup"><span data-stu-id="34b4f-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="34b4f-121">Оставьте комментарий ниже на хотелось бы toosee.</span><span class="sxs-lookup"><span data-stu-id="34b4f-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="34b4f-122">toolearn как toocraft подключения, считывать [получить строку подключения учетной записи hello](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="34b4f-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="34b4f-123">Скопируйте и вставьте фрагмент кода hello в приложении MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Колонка "Быстрый запуск"](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="34b4f-125"><a id="GetCustomConnection"></a>Получить подключение строку hello MongoDB toocustomize</span><span class="sxs-lookup"><span data-stu-id="34b4f-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="34b4f-126">В веб-браузере вход toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34b4f-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34b4f-127">В hello **Azure Cosmos DB** колонке выберите hello API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="34b4f-128">Hello левой части колонки hello учетной записи, нажмите кнопку **строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="34b4f-129">Hello **строка подключения** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="34b4f-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="34b4f-130">Он имеет все hello сведения о необходимости tooconnect toohello учетную запись с помощью драйвера для MongoDB, включая строку preconstructed подключения.</span><span class="sxs-lookup"><span data-stu-id="34b4f-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Колонка "Строка подключения"](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="34b4f-132">Требования к строке подключения</span><span class="sxs-lookup"><span data-stu-id="34b4f-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="34b4f-133">В Azure Cosmos DB строгие требования к безопасности и стандарты.</span><span class="sxs-lookup"><span data-stu-id="34b4f-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="34b4f-134">Для всех учетных записей Azure Cosmos DB требуется проверка подлинности и безопасный обмен данными через *SSL*.</span><span class="sxs-lookup"><span data-stu-id="34b4f-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="34b4f-135">Azure Cosmos DB поддерживает hello Стандартная MongoDB формат строки подключения URI, с помощью нескольких конкретных требований: учетные записи Azure Cosmos DB требовать проверку подлинности и безопасного взаимодействия через SSL.</span><span class="sxs-lookup"><span data-stu-id="34b4f-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="34b4f-136">Таким образом является формат строки соединения hello:</span><span class="sxs-lookup"><span data-stu-id="34b4f-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="34b4f-137">Hello значения этой строки доступны в hello **строка подключения** колонки, показанного выше:</span><span class="sxs-lookup"><span data-stu-id="34b4f-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="34b4f-138">Имя пользователя (обязательно): имя учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="34b4f-139">Пароль (обязательно): пароль для учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="34b4f-140">Узел (обязательно): полное доменное имя учетной записи Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="34b4f-141">Порт (обязательно): 10255.</span><span class="sxs-lookup"><span data-stu-id="34b4f-141">Port (required): 10255.</span></span>
* <span data-ttu-id="34b4f-142">База данных (необязательно): hello базы данных, которая hello соединение использует.</span><span class="sxs-lookup"><span data-stu-id="34b4f-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="34b4f-143">Если база данных не указан, база данных по умолчанию hello — «проверка».</span><span class="sxs-lookup"><span data-stu-id="34b4f-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="34b4f-144">ssl=true (обязательно)</span><span class="sxs-lookup"><span data-stu-id="34b4f-144">ssl=true (required)</span></span>

<span data-ttu-id="34b4f-145">Допустим, учетная запись hello показано hello **строка подключения** колонку.</span><span class="sxs-lookup"><span data-stu-id="34b4f-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="34b4f-146">Допустимая строка подключения:</span><span class="sxs-lookup"><span data-stu-id="34b4f-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="34b4f-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34b4f-147">Next steps</span></span>
* <span data-ttu-id="34b4f-148">Узнайте, каким образом слишком[использовать MongoChef](mongodb-mongochef.md) Azure Cosmos DB API-интерфейсы для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="34b4f-149">Просмотр hello Azure Cosmos DB API для MongoDB, просмотрев [образцы](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="34b4f-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
