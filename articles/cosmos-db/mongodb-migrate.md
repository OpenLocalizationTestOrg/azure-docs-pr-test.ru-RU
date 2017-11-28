---
title: "aaaUse mongoimport и mongorestore с hello Azure Cosmos DB API для MongoDB | Документы Microsoft"
description: "Узнайте, как toouse mongoimport и mongorestore tooimport данные tooan API для MongoDB учетной записи"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="cd4c9-104">Azure Cosmos DB: импорт данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="cd4c9-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="cd4c9-105">toomigrate данные из tooan MongoDB Azure Cosmos DB учетной записи для использования с hello API для MongoDB, необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="cd4c9-106">Загрузите либо *mongoimport.exe* или *mongorestore.exe* из hello [центра загрузки MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="cd4c9-107">Получите [строку подключения API для MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="cd4c9-108">При импорте данных из toouse план и MongoDB с Здравствуйте, Azure Cosmos DB, следует использовать hello [средство переноса данных](import-data.md) tooimport данных.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="cd4c9-109">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd4c9-110">Получение строки подключения</span><span class="sxs-lookup"><span data-stu-id="cd4c9-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="cd4c9-111">Импорт данных MongoDB с помощью mongoimport</span><span class="sxs-lookup"><span data-stu-id="cd4c9-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="cd4c9-112">Импорт данных MongoDB с помощью mongorestore</span><span class="sxs-lookup"><span data-stu-id="cd4c9-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd4c9-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd4c9-113">Prerequisites</span></span>

* <span data-ttu-id="cd4c9-114">Увеличить пропускную способность: hello продолжительность переноса данных зависит от hello объем пропускной способности, настройка для коллекций.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="cd4c9-115">Быть убедиться, что пропускная способность hello tooincrease большего миграции данных.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="cd4c9-116">После завершения миграции hello уменьшения затрат toosave hello пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="cd4c9-117">Дополнительные сведения об увеличении пропускной способности в hello [портал Azure](https://portal.azure.com), в разделе [уровни производительности и ценовые категории в базе данных Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="cd4c9-118">Включите SSL. В Azure Cosmos DB строгие требования к безопасности и стандарты.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="cd4c9-119">Быть tooenable убедиться, что SSL при взаимодействии с вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="cd4c9-120">следующие процедуры Hello в hello оставшейся части статьи hello как tooenable SSL для mongoimport и mongorestore.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="cd4c9-121">Поиск сведений о строке подключения (узел, порт, имя пользователя и пароль)</span><span class="sxs-lookup"><span data-stu-id="cd4c9-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="cd4c9-122">В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Cosmos DB** входа.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="cd4c9-123">В hello **подписки** области, выберите имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="cd4c9-124">В hello **строка подключения** колонка, щелкните **строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="cd4c9-125">Hello правой панели содержится вся информация hello, необходимость toosuccessfully подключения tooyour учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Колонка "Строка подключения"](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="cd4c9-127">Импорт данных toohello API для MongoDB с помощью mongoimport</span><span class="sxs-lookup"><span data-stu-id="cd4c9-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="cd4c9-128">tooyour tooimport данных учетной записи Azure Cosmos DB, используйте следующий шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="cd4c9-129">Заполните *узла*, *username*, и *пароль* со значениями hello tooyour определенной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="cd4c9-130">Шаблон:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="cd4c9-131">Пример:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="cd4c9-132">Импорт данных toohello API для MongoDB с помощью mongorestore</span><span class="sxs-lookup"><span data-stu-id="cd4c9-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="cd4c9-133">API tooyour toorestore данных MongoDB учетной записи, с помощью hello после импорта hello tooexecute шаблона.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="cd4c9-134">Заполните *узла*, *username*, и *пароль* со значениями hello tooyour определенной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="cd4c9-135">Шаблон:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="cd4c9-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="cd4c9-137">Инструкции для успешного переноса</span><span class="sxs-lookup"><span data-stu-id="cd4c9-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="cd4c9-138">Заранее создайте и масштабируйте свои коллекции:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="cd4c9-139">По умолчанию Azure Cosmos DB подготавливает новую коллекцию MongoDB, обеспечивающую пропускную способность 1000 единиц запроса в секунду (ЕЗ/с).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="cd4c9-140">Перед началом миграции hello с помощью mongoimport, mongorestore или mongomirror предварительно создать все коллекции из hello [портал Azure](https://portal.azure.com) или из средства и драйверы MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="cd4c9-141">Если в коллекции больше, чем 10 ГБ, убедитесь, что toocreate [сегментированных и секционированные коллекции](partition-data.md) с ключом соответствующий сегмент.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="cd4c9-142">Из hello [портал Azure](https://portal.azure.com), увеличить пропускную способность вашей коллекции из 1000 RUs для коллекции одну секцию и 2500 RUs для сегментированной коллекции только для миграции hello.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="cd4c9-143">С hello более высокую пропускную способность можно избежать регулирования и перенести за меньшее время.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="cd4c9-144">С ежечасное выставление счетов в базе данных Azure Cosmos, можно уменьшить пропускную способность hello сразу после hello миграции toosave затраты.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="cd4c9-145">Вычислите hello приблизительное RU платы для записи одного документа.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="cd4c9-146">а.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-146">a.</span></span> <span data-ttu-id="cd4c9-147">Подключите базы данных Azure Cosmos DB MongoDB tooyour hello MongoDB оболочки.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="cd4c9-148">Инструкции в [подключения tooAzure приложения MongoDB Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="cd4c9-149">b.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-149">b.</span></span> <span data-ttu-id="cd4c9-150">Выполните пример команды insert с помощью одного из документы образец hello MongoDB оболочки:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="cd4c9-151">c.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-151">c.</span></span> <span data-ttu-id="cd4c9-152">Выполните команду ```db.runCommand({getLastRequestStatistics: 1})```, в результате чего будет получен ответ, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="cd4c9-153">d.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-153">d.</span></span> <span data-ttu-id="cd4c9-154">Запишите hello запрос бесплатно.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="cd4c9-155">Определение задержки hello из вашей машины toohello Azure Cosmos DB облачной службы:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="cd4c9-156">а.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-156">a.</span></span> <span data-ttu-id="cd4c9-157">Включите подробное ведение журнала из hello MongoDB оболочки с помощью следующей команды:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="cd4c9-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="cd4c9-158">b.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-158">b.</span></span> <span data-ttu-id="cd4c9-159">Выполнить простой запрос базы данных hello: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="cd4c9-160">В результате будет получен ответ, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="cd4c9-161">Удаление документа hello вставлены до миграции tooensure hello, что нет повторяющихся документов.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="cd4c9-162">Для удаления документов можно использовать команду ```db.coll.remove({})```.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="cd4c9-163">Вычислить приблизительное hello *batchSize* и *numInsertionWorkers* значения:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="cd4c9-164">Для *batchSize*, деление hello всего подготовить RUs с RUs hello, взятые из записи в один документ на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="cd4c9-165">Если учесть hello *batchSize* < = 24, использовать это число как ваш *batchSize* значение.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="cd4c9-166">Если учесть hello *batchSize* > 24, набор hello *batchSize* too24 значение.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="cd4c9-167">Для расчета *numInsertionWorkers* используйте следующую формулу: *numInsertionWorkers = (подготовленная пропускная способность * задержка в секундах) / (размер пакета * число ЕЗ, использованных для одной операции записи)*.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="cd4c9-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd4c9-168">Property</span></span>|<span data-ttu-id="cd4c9-169">Значение</span><span class="sxs-lookup"><span data-stu-id="cd4c9-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="cd4c9-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="cd4c9-170">batchSize</span></span>| <span data-ttu-id="cd4c9-171">24</span><span class="sxs-lookup"><span data-stu-id="cd4c9-171">24</span></span> |
    |<span data-ttu-id="cd4c9-172">Подготовленные ЕЗ</span><span class="sxs-lookup"><span data-stu-id="cd4c9-172">RUs provisioned</span></span> | <span data-ttu-id="cd4c9-173">10 000</span><span class="sxs-lookup"><span data-stu-id="cd4c9-173">10000</span></span> |
    |<span data-ttu-id="cd4c9-174">Задержка</span><span class="sxs-lookup"><span data-stu-id="cd4c9-174">Latency</span></span> | <span data-ttu-id="cd4c9-175">0,100 с</span><span class="sxs-lookup"><span data-stu-id="cd4c9-175">0.100 s</span></span> |
    |<span data-ttu-id="cd4c9-176">ЕЗ, использованные для записи 1 документа</span><span class="sxs-lookup"><span data-stu-id="cd4c9-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="cd4c9-177">10 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="cd4c9-177">10 RUs</span></span> |
    |<span data-ttu-id="cd4c9-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="cd4c9-178">numInsertionWorkers</span></span> | <span data-ttu-id="cd4c9-179">?</span><span class="sxs-lookup"><span data-stu-id="cd4c9-179">?</span></span> |
    
    <span data-ttu-id="cd4c9-180">*numInsertionWorkers = (10000 ЕЗ x 0,1 с) / (24 x 10 ЕЗ) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="cd4c9-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="cd4c9-181">Выполните команду hello окончательной миграции:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="cd4c9-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd4c9-182">Next steps</span></span>

<span data-ttu-id="cd4c9-183">Можно продолжить toohello следующее руководство и узнайте, как tooquery данных MongoDB с использованием Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="cd4c9-184">Как tooquery данных MongoDB?</span><span class="sxs-lookup"><span data-stu-id="cd4c9-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
