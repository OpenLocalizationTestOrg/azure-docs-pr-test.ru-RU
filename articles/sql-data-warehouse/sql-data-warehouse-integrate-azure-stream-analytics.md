---
title: "aaaUse Azure Stream Analytics с хранилищем данных SQL | Документы Microsoft"
description: "Советы по использованию службы Azure Stream Analytics и хранилища данных SQL для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="e751d-103">Работа со службой Azure Stream Analytics и хранилищем данных SQL</span><span class="sxs-lookup"><span data-stu-id="e751d-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="e751d-104">Azure Stream Analytics является полностью управляемой службы, предоставляя обработки сложных событий низкой задержкой, высокодоступные и масштабируемые потоковой передаче данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e751d-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="e751d-105">Вы можете изучить основы hello, чтении [tooAzure введение Stream Analytics][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="e751d-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="e751d-106">Затем можно узнать, как hello toocreate решения конца в конец с Stream Analytics, следуя [приступить к использованию Azure Stream Analytics] [ Get started using Azure Stream Analytics] учебника.</span><span class="sxs-lookup"><span data-stu-id="e751d-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="e751d-107">В этой статье вы узнаете, как toouse хранилище данных SQL Azure базы данных в качестве приемника выходных данных для заданий Analytics поток данных.</span><span class="sxs-lookup"><span data-stu-id="e751d-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e751d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e751d-108">Prerequisites</span></span>
<span data-ttu-id="e751d-109">Во-первых, выполните следующие шаги в hello hello [приступить к использованию Azure Stream Analytics] [ Get started using Azure Stream Analytics] учебника.</span><span class="sxs-lookup"><span data-stu-id="e751d-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="e751d-110">Создание ввода концентратора событий</span><span class="sxs-lookup"><span data-stu-id="e751d-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="e751d-111">Настройка и запуск приложения генератора событий</span><span class="sxs-lookup"><span data-stu-id="e751d-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="e751d-112">Подготовка задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e751d-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="e751d-113">Указание входных данных задания и запроса</span><span class="sxs-lookup"><span data-stu-id="e751d-113">Specify job input and query</span></span>

<span data-ttu-id="e751d-114">Затем создание базы данных хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e751d-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="e751d-115">Указание выходных данных задания: база данных хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e751d-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="e751d-116">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="e751d-116">Step 1</span></span>
<span data-ttu-id="e751d-117">В задание Stream Analytics щелкните **ВЫВОДА** сверху hello страницу приветствия и нажмите кнопку **Добавление выходных данных**.</span><span class="sxs-lookup"><span data-stu-id="e751d-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="e751d-118">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="e751d-118">Step 2</span></span>
<span data-ttu-id="e751d-119">Выберите базу данных SQL и нажмите кнопку «Далее».</span><span class="sxs-lookup"><span data-stu-id="e751d-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="e751d-120">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="e751d-120">Step 3</span></span>
<span data-ttu-id="e751d-121">Введите следующие значения на следующую страницу приветствия hello:</span><span class="sxs-lookup"><span data-stu-id="e751d-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="e751d-122">*Псевдоним выходных данных*: введите понятное имя для выходных данных этого задания.</span><span class="sxs-lookup"><span data-stu-id="e751d-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="e751d-123">*Подписка*:</span><span class="sxs-lookup"><span data-stu-id="e751d-123">*Subscription*:</span></span>
  * <span data-ttu-id="e751d-124">Если база данных хранилища данных SQL в hello той же подписке, задание Stream Analytics hello, выберите использовать базу данных SQL из текущей подписки.</span><span class="sxs-lookup"><span data-stu-id="e751d-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="e751d-125">Если ваша база данных находится в другой подписке, выберите параметр "Использовать базу данных SQL из другой подписки".</span><span class="sxs-lookup"><span data-stu-id="e751d-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="e751d-126">*База данных*: укажите имя hello в целевую базу данных.</span><span class="sxs-lookup"><span data-stu-id="e751d-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="e751d-127">*Имя сервера*: укажите имя сервера hello для указанной базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="e751d-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="e751d-128">Toofind hello классический портал Azure можно использовать это.</span><span class="sxs-lookup"><span data-stu-id="e751d-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="e751d-129">*Имя пользователя*: укажите hello имя пользователя учетной записи, которая имеет разрешения на запись для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="e751d-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="e751d-130">*Пароль*: укажите пароль hello для hello указанную учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="e751d-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="e751d-131">*Таблица*: укажите имя hello hello целевой таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="e751d-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="e751d-132">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="e751d-132">Step 4</span></span>
<span data-ttu-id="e751d-133">Щелкните tooadd кнопку флажок hello этот результат выполнения задания и tooverify успешного подключения базы данных toohello Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e751d-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="e751d-134">После успешного завершения hello подключение к базе данных toohello, вы увидите уведомление hello нижней части портала hello.</span><span class="sxs-lookup"><span data-stu-id="e751d-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="e751d-135">Hello нижней tootest hello подключения toohello базы данных нажмите кнопку Проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="e751d-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e751d-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e751d-136">Next steps</span></span>
<span data-ttu-id="e751d-137">Общие сведения об интеграции см. в статье [Интеграция других служб с хранилищем данных SQL][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="e751d-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="e751d-138">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e751d-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
