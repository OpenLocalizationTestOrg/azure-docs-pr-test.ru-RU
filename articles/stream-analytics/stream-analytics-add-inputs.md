---
title: "aaaAdd данных ввода заданий Stream Analytics tooyour | Документы Microsoft"
description: "Узнайте, как toohook копирование tooyour источника данных Stream Analytics задания как потоковой передачи входных данных из хранилища больших двоичных данных концентраторов событий или ссылку."
keywords: "входные данные, потоковые данные"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="0f422-104">Добавить потоковой передачи данных входные или ссылочные данные tooa задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="0f422-105">Узнайте, как toohook копирование tooyour источника данных Stream Analytics задания как потоковой передачи входных данных из концентраторов событий или ссылка данные из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0f422-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="0f422-106">Azure Stream Analytics задания могут быть подключенным tooone входные данные или несколько, каждый из которых определения существующего источника данных соединения tooan.</span><span class="sxs-lookup"><span data-stu-id="0f422-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="0f422-107">Как данные передаются источнику данных toothat, потребляемых задания Stream Analytics hello и обрабатываются в режиме реального времени, как потоковые данные.</span><span class="sxs-lookup"><span data-stu-id="0f422-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="0f422-108">Stream Analytics поддерживает качественную интеграцию с [концентраторов событий Azure](https://azure.microsoft.com/services/event-hubs/) и [хранилища больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) как внутри, так и за пределами задания hello подписки.</span><span class="sxs-lookup"><span data-stu-id="0f422-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="0f422-109">Эта статья является этапом hello [план обучения для Stream Analytics](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="0f422-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="0f422-110">Входные данные: потоковые данные и ссылочные данные</span><span class="sxs-lookup"><span data-stu-id="0f422-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="0f422-111">В службе Stream Analytics используют два отдельных типа входных данных: потоки данных и эталонные данные.</span><span class="sxs-lookup"><span data-stu-id="0f422-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="0f422-112">**Потоки данных**: заданий Stream Analytics должен включать по крайней мере один данных потока ввода toobe использована и преобразована заданием hello.</span><span class="sxs-lookup"><span data-stu-id="0f422-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="0f422-113">В качестве источников входных потоковых данных могут выступать хранилище больших двоичных объектов Azure и концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0f422-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="0f422-114">Концентраторы событий Azure, используемых toocollect потоки событий из подключенных устройств, служб и приложений.</span><span class="sxs-lookup"><span data-stu-id="0f422-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="0f422-115">Для приема массовых данных  в качестве потока можно использовать хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0f422-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="0f422-116">**Эталонные данные**: служба Stream Analytics поддерживает второй тип вспомогательных входных данных, которые называются эталонными.</span><span class="sxs-lookup"><span data-stu-id="0f422-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="0f422-117">В противоположность toodata на ходу эти данные являются статическими или снижающее производительность изменение.</span><span class="sxs-lookup"><span data-stu-id="0f422-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="0f422-118">Обычно используется для выполнения поисков и взаимосвязи с toocreate потоков данных на более широком наборе данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="0f422-119">Хранилища больших двоичных объектов Azure в настоящее время является источника входных данных hello поддерживается только для ссылочных данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="0f422-120">tooadd задание Stream Analytics ввода tooyour:</span><span class="sxs-lookup"><span data-stu-id="0f422-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="0f422-121">В hello портала Azure щелкните **входов** и нажмите кнопку **Добавление входных данных** в задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f422-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Классический портал Azure — добавление входных данных.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="0f422-123">В hello портала Azure щелкните hello **входов** плитки в задание Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f422-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Портал Azure — добавление входных данных.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="0f422-125">Укажите тип Привет вводимых hello: либо **потока данных** или **ссылочные данные**.</span><span class="sxs-lookup"><span data-stu-id="0f422-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Добавить hello правильные данные ввода, потоковый или ссылки](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Добавить hello правильные данные ввода, потоковый или ссылки](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="0f422-128">При создании ввода потока данных, укажите тип источника hello для входа hello.</span><span class="sxs-lookup"><span data-stu-id="0f422-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="0f422-129">Так как в настоящее время поддерживается только хранилище больших двоичных объектов, при создании эталонных данных этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="0f422-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Добавление источника потока данных](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Добавление источника потока данных](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="0f422-132">Введите понятное имя для этого входного в hello входной псевдоним.</span><span class="sxs-lookup"><span data-stu-id="0f422-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="0f422-133">Это имя будет использоваться в запросе в задание позже на входе toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="0f422-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="0f422-134">Заполните остальные hello hello необходимые свойства tooconnect tooyour в источнике данных соединения.</span><span class="sxs-lookup"><span data-stu-id="0f422-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="0f422-135">Эти поля зависят от типа входных данных и источника и подробно описаны [здесь](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="0f422-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Добавление входных данных концентратора событий](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="0f422-137">Укажите параметры сериализации hello hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="0f422-138">toomake убедиться, что ваши запросы работают hello так, как ожидалось, укажите hello **формат сериализации событий** входящих данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="0f422-139">Поддерживаемые форматы сериализации: JSON, CSV и Avro.</span><span class="sxs-lookup"><span data-stu-id="0f422-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="0f422-140">Проверьте hello **кодировка** hello данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="0f422-141">UTF-8 является hello поддерживается только формат кодировки в данный момент.</span><span class="sxs-lookup"><span data-stu-id="0f422-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Параметры сериализации данных для входных данных hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Параметры сериализации данных для входных данных hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="0f422-144">После завершения создания входных hello, Stream Analytics будет проверять возможность подключения toohello источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="0f422-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="0f422-145">Состояние hello hello операции подключения теста можно просмотреть в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="0f422-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Проверка соединения объекта hello потокового ввода данных](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Проверка соединения объекта hello потокового ввода данных](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="0f422-148">Получение справки по потоковой передаче входных данных</span><span class="sxs-lookup"><span data-stu-id="0f422-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="0f422-149">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0f422-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f422-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f422-150">Next steps</span></span>
* [<span data-ttu-id="0f422-151">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0f422-152">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0f422-153">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0f422-154">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0f422-155">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0f422-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

