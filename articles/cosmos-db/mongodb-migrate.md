---
title: "Использование mongoimport и mongorestore с API Azure Cosmos DB для MongoDB | Документация Майкрософт"
description: "Узнайте, как использовать mongoimport и mongorestore для импорта данных в учетную запись API для MongoDB."
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
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="ed386-104">Azure Cosmos DB: импорт данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="ed386-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="ed386-105">Для переноса данных из MongoDB в учетную запись Azure Cosmos DB для использования с API для MongoDB необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ed386-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="ed386-106">Скачайте файл *mongoimport.exe* или *mongorestore.exe* из [центра скачивания MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="ed386-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="ed386-107">Получите [строку подключения API для MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="ed386-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="ed386-108">Если вы импортируете данные из MongoDB и планируете использовать их с Azure Cosmos DB, то используйте [средство переноса данных](import-data.md) для их импорта.</span><span class="sxs-lookup"><span data-stu-id="ed386-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="ed386-109">В рамках этого руководства рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ed386-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed386-110">Получение строки подключения</span><span class="sxs-lookup"><span data-stu-id="ed386-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="ed386-111">Импорт данных MongoDB с помощью mongoimport</span><span class="sxs-lookup"><span data-stu-id="ed386-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="ed386-112">Импорт данных MongoDB с помощью mongorestore</span><span class="sxs-lookup"><span data-stu-id="ed386-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed386-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed386-113">Prerequisites</span></span>

* <span data-ttu-id="ed386-114">Увеличьте пропускную способность. Продолжительность переноса данных зависит от пропускной способности, настроенной для коллекций.</span><span class="sxs-lookup"><span data-stu-id="ed386-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="ed386-115">Увеличьте пропускную способность для крупных миграций.</span><span class="sxs-lookup"><span data-stu-id="ed386-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="ed386-116">После переноса уменьшите пропускную способность для экономии расходов.</span><span class="sxs-lookup"><span data-stu-id="ed386-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="ed386-117">Дополнительные сведения об увеличении пропускной способности на [портале Azure](https://portal.azure.com) см. в статье [Прекращение использования уровней производительности S1, S2 и S3 в DocumentDB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ed386-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="ed386-118">Включите SSL. В Azure Cosmos DB строгие требования к безопасности и стандарты.</span><span class="sxs-lookup"><span data-stu-id="ed386-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="ed386-119">Обязательно включите SSL при взаимодействии с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="ed386-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="ed386-120">Процедуры, описанные в оставшейся части статьи, включают инструкции по включению SSL для mongoimport и mongorestore.</span><span class="sxs-lookup"><span data-stu-id="ed386-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="ed386-121">Поиск сведений о строке подключения (узел, порт, имя пользователя и пароль)</span><span class="sxs-lookup"><span data-stu-id="ed386-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="ed386-122">В левой панели на [портале Azure](https://portal.azure.com) щелкните запись **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ed386-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="ed386-123">На панели **Подписки** выберите имя своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ed386-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="ed386-124">В колонке **Строка подключения** щелкните **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="ed386-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="ed386-125">На правой панели содержатся все сведения, необходимые для успешного подключения к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ed386-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Колонка "Строка подключения"](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="ed386-127">Импорт данных в API для MongoDB с помощью mongoimport</span><span class="sxs-lookup"><span data-stu-id="ed386-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="ed386-128">Чтобы импортировать данные в учетную запись Azure Cosmos DB, используйте следующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="ed386-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="ed386-129">Укажите *узел*, *имя пользователя* и *пароль* своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ed386-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="ed386-130">Шаблон:</span><span class="sxs-lookup"><span data-stu-id="ed386-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="ed386-131">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed386-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="ed386-132">Импорт данных в API для MongoDB с помощью mongorestore</span><span class="sxs-lookup"><span data-stu-id="ed386-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="ed386-133">Чтобы восстановить данные в API для учетной записи MongoDB, используйте следующий шаблон для выполнения импорта.</span><span class="sxs-lookup"><span data-stu-id="ed386-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="ed386-134">Укажите *узел*, *имя пользователя* и *пароль* своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ed386-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="ed386-135">Шаблон:</span><span class="sxs-lookup"><span data-stu-id="ed386-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="ed386-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed386-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="ed386-137">Инструкции для успешного переноса</span><span class="sxs-lookup"><span data-stu-id="ed386-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="ed386-138">Заранее создайте и масштабируйте свои коллекции:</span><span class="sxs-lookup"><span data-stu-id="ed386-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="ed386-139">По умолчанию Azure Cosmos DB подготавливает новую коллекцию MongoDB, обеспечивающую пропускную способность 1000 единиц запроса в секунду (ЕЗ/с).</span><span class="sxs-lookup"><span data-stu-id="ed386-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="ed386-140">Прежде чем начать перенос с помощью mongoimport, mongorestore или mongomirror, создайте все свои коллекции с [портала Azure](https://portal.azure.com) или из драйверов и инструментов MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ed386-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="ed386-141">Если размер коллекции превышает 10 ГБ, то создайте [сегментированную или секционированную коллекцию](partition-data.md) с соответствующим ключом сегмента.</span><span class="sxs-lookup"><span data-stu-id="ed386-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="ed386-142">На [портале Azure](https://portal.azure.com) увеличьте показатели пропускной способности своих коллекций (с 1000 ЕЗ/с для односекционной коллекции и 2500 ЕЗ/с для сегментированной коллекции) только на время выполнения переноса.</span><span class="sxs-lookup"><span data-stu-id="ed386-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="ed386-143">Более высокая пропускная способность позволяет избежать регулирования и выполнить перенос быстрее.</span><span class="sxs-lookup"><span data-stu-id="ed386-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="ed386-144">Почасовая модель выставления счетов, применяемая в Azure Cosmos DB, позволяет снизить пропускную способность сразу после переноса для сокращения затрат.</span><span class="sxs-lookup"><span data-stu-id="ed386-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="ed386-145">Вычислите приблизительную стоимость ЕЗ при записи одного документа:</span><span class="sxs-lookup"><span data-stu-id="ed386-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="ed386-146">а.</span><span class="sxs-lookup"><span data-stu-id="ed386-146">a.</span></span> <span data-ttu-id="ed386-147">Подключитесь к базе данных MongoDB в Azure Cosmos DB из оболочки MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ed386-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="ed386-148">Инструкции доступны в статье [Подключение приложения MongoDB к Azure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="ed386-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="ed386-149">b.</span><span class="sxs-lookup"><span data-stu-id="ed386-149">b.</span></span> <span data-ttu-id="ed386-150">Выполните пример команды insert, используя один из примеров документов из оболочки MongoDB:</span><span class="sxs-lookup"><span data-stu-id="ed386-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="ed386-151">c.</span><span class="sxs-lookup"><span data-stu-id="ed386-151">c.</span></span> <span data-ttu-id="ed386-152">Выполните команду ```db.runCommand({getLastRequestStatistics: 1})```, в результате чего будет получен ответ, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="ed386-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="ed386-153">г)</span><span class="sxs-lookup"><span data-stu-id="ed386-153">d.</span></span> <span data-ttu-id="ed386-154">Запишите значение RequestCharge (стоимость запроса).</span><span class="sxs-lookup"><span data-stu-id="ed386-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="ed386-155">Определите задержку между вашим компьютером и облачной службой Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="ed386-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="ed386-156">а.</span><span class="sxs-lookup"><span data-stu-id="ed386-156">a.</span></span> <span data-ttu-id="ed386-157">Включите ведение подробного журнала из оболочки MongoDB с помощью команды ```setVerboseShell(true)```.</span><span class="sxs-lookup"><span data-stu-id="ed386-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="ed386-158">b.</span><span class="sxs-lookup"><span data-stu-id="ed386-158">b.</span></span> <span data-ttu-id="ed386-159">Выполните простой запрос к базе данных: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="ed386-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="ed386-160">В результате будет получен ответ, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="ed386-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="ed386-161">Перед выполнением переноса удалите вставленный документ, чтобы точно не было повторяющихся документов.</span><span class="sxs-lookup"><span data-stu-id="ed386-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="ed386-162">Для удаления документов можно использовать команду ```db.coll.remove({})```.</span><span class="sxs-lookup"><span data-stu-id="ed386-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="ed386-163">Вычислите приблизительные значения *batchSize* и *numInsertionWorkers*:</span><span class="sxs-lookup"><span data-stu-id="ed386-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="ed386-164">Для расчета *batchSize* поделите общее число подготовленных ЕЗ на число ЕЗ, использованных для записи одного документа (на шаге 3).</span><span class="sxs-lookup"><span data-stu-id="ed386-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="ed386-165">Если полученное значение *batchSize* <= 24, то используйте его в качестве значения *batchSize*.</span><span class="sxs-lookup"><span data-stu-id="ed386-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="ed386-166">Если полученное значение *batchSize* > 24, то задайте значение *batchSize* равное 24.</span><span class="sxs-lookup"><span data-stu-id="ed386-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="ed386-167">Для расчета *numInsertionWorkers* используйте следующую формулу: *numInsertionWorkers = (подготовленная пропускная способность * задержка в секундах) / (размер пакета * число ЕЗ, использованных для одной операции записи)*.</span><span class="sxs-lookup"><span data-stu-id="ed386-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="ed386-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="ed386-168">Property</span></span>|<span data-ttu-id="ed386-169">Значение</span><span class="sxs-lookup"><span data-stu-id="ed386-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="ed386-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="ed386-170">batchSize</span></span>| <span data-ttu-id="ed386-171">24</span><span class="sxs-lookup"><span data-stu-id="ed386-171">24</span></span> |
    |<span data-ttu-id="ed386-172">Подготовленные ЕЗ</span><span class="sxs-lookup"><span data-stu-id="ed386-172">RUs provisioned</span></span> | <span data-ttu-id="ed386-173">10 000</span><span class="sxs-lookup"><span data-stu-id="ed386-173">10000</span></span> |
    |<span data-ttu-id="ed386-174">Задержка</span><span class="sxs-lookup"><span data-stu-id="ed386-174">Latency</span></span> | <span data-ttu-id="ed386-175">0,100 с</span><span class="sxs-lookup"><span data-stu-id="ed386-175">0.100 s</span></span> |
    |<span data-ttu-id="ed386-176">ЕЗ, использованные для записи 1 документа</span><span class="sxs-lookup"><span data-stu-id="ed386-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="ed386-177">10 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="ed386-177">10 RUs</span></span> |
    |<span data-ttu-id="ed386-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="ed386-178">numInsertionWorkers</span></span> | <span data-ttu-id="ed386-179">?</span><span class="sxs-lookup"><span data-stu-id="ed386-179">?</span></span> |
    
    <span data-ttu-id="ed386-180">*numInsertionWorkers = (10000 ЕЗ x 0,1 с) / (24 x 10 ЕЗ) = 4,1666*</span><span class="sxs-lookup"><span data-stu-id="ed386-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="ed386-181">Выполните окончательную команду переноса:</span><span class="sxs-lookup"><span data-stu-id="ed386-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="ed386-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed386-182">Next steps</span></span>

<span data-ttu-id="ed386-183">Вы можете перейти к следующему руководству, из которого вы узнаете, как запрашивать данные MongoDB с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ed386-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="ed386-184">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API для MongoDB</span><span class="sxs-lookup"><span data-stu-id="ed386-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
