---
title: "Настройка выходов данных для заданий Stream Analytics | Документация Майкрософт"
description: "Настройка выходных данных для заданий Stream Analytics | Сегмент схемы обучения"
keywords: "вывод данных, перемещение данных"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="3dcff-104">Настройка выходов данных для заданий Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="3dcff-105">Задания службы Azure Stream Analytics можно подключать к одному или нескольким выходам данных, которые определяют подключение к существующему приемнику данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="3dcff-106">По мере того как задание Stream Analytics обрабатывает и преобразует входящие данные, поток выходных данных записывается в выходные данные задания.</span><span class="sxs-lookup"><span data-stu-id="3dcff-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="3dcff-107">Выходные данные Stream Analytics могут служить источником данных для панелей мониторинга в режиме реального времени и предупреждений, запускать рабочие процессы переноса данных или просто архивировать данные для последующей пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="3dcff-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="3dcff-108">Служба Stream Analytics обеспечивает первоклассную интеграцию с различными службами Azure, которые подробно описаны здесь.</span><span class="sxs-lookup"><span data-stu-id="3dcff-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="3dcff-109">Чтобы добавить выход данных в задание службы Stream Analytics, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3dcff-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="3dcff-110">На [портале Azure](https://portal.azure.com) откройте задание и щелкните **Выходные данные**, а затем нажмите кнопку **Добавить** в появившейся колонке выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![Добавление выходных данных](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="3dcff-112">В поле **Псевдоним выходных данных** введите понятное имя для этого выхода данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="3dcff-113">Впоследствии это имя можно будет использовать в запросе вашего задания для ссылки на выходные данные.</span><span class="sxs-lookup"><span data-stu-id="3dcff-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="3dcff-114">Укажите остальные свойства подключения, необходимые для подключения к выходу данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="3dcff-115">Эти поля зависят от типа выходных данных и подробно описаны здесь.</span><span class="sxs-lookup"><span data-stu-id="3dcff-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Выбор типа перемещения данных](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="3dcff-117">В зависимости от типа выходных данных необходимо указать способ сериализации или форматирования данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="3dcff-118">В этой статье описаны конкретные параметры сериализации для каждого выходного типа.</span><span class="sxs-lookup"><span data-stu-id="3dcff-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="3dcff-119">Укажите остальные свойства подключения, необходимые для подключения к источнику данных.</span><span class="sxs-lookup"><span data-stu-id="3dcff-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="3dcff-120">Эти поля зависят от типа входных данных и источника и подробно описаны в статье [Создание задания обработки аналитики данных для Stream Analytics](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="3dcff-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="3dcff-121">Любой элемент вывода, добавляемый в задание, должен существовать до момента запуска задания и запуска потока событий.</span><span class="sxs-lookup"><span data-stu-id="3dcff-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="3dcff-122">Например, при выводе данных в хранилище BLOB-объектов задание не создаст учетную запись хранения автоматически.</span><span class="sxs-lookup"><span data-stu-id="3dcff-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="3dcff-123">Пользователь должен создать эту запись перед тем, как запустить задание ASA.</span><span class="sxs-lookup"><span data-stu-id="3dcff-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="3dcff-124">Получение справки</span><span class="sxs-lookup"><span data-stu-id="3dcff-124">Get help</span></span>
<span data-ttu-id="3dcff-125">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3dcff-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dcff-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3dcff-126">Next steps</span></span>
* [<span data-ttu-id="3dcff-127">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3dcff-128">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3dcff-129">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3dcff-130">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3dcff-131">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3dcff-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

