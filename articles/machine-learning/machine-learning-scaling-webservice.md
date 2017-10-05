---
title: "Как повысить параллелизм веб-службы машинного обучения Azure | Документация Майкрософт"
description: "Узнайте, как повысить параллелизм веб-службы машинного обучения Azure с помощью добавления дополнительных конечных точек."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "машинное обучение azure, веб-службы, операционализация, масштабирование, конечная точка, параллелизм"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="101f0-104">Масштабирование веб-службы машинного обучения Azure с помощью добавления дополнительных конечных точек</span><span class="sxs-lookup"><span data-stu-id="101f0-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="101f0-105">В этой статье описаны методы, применимые для **классической** веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="101f0-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="101f0-106">По умолчанию каждая опубликованная веб-служба настраивается для поддержки 20 параллельных запросов, а максимальное число параллельных запросов может доходить до 200.</span><span class="sxs-lookup"><span data-stu-id="101f0-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="101f0-107">Это значение можно задать на классическом портале Azure, однако Машинное обучение Azure автоматически оптимизирует этот параметр, обеспечивая максимальную производительность веб-службы. Значение, указанное на портале, при этом игнорируется.</span><span class="sxs-lookup"><span data-stu-id="101f0-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="101f0-108">Если для API планируется более высокая нагрузка, чем максимальное поддерживаемое значение в 200 одновременных вызовов, следует создать для такой веб-службы несколько конечных точек.</span><span class="sxs-lookup"><span data-stu-id="101f0-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="101f0-109">Это позволит случайным образом распределять нагрузку между ними.</span><span class="sxs-lookup"><span data-stu-id="101f0-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="101f0-110">Масштабирование веб-службы — достаточно распространенная задача.</span><span class="sxs-lookup"><span data-stu-id="101f0-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="101f0-111">Например, масштабирование будет полезным для поддержки более 200 одновременных запросов, для повышения доступности путем использования нескольких конечных точек или для разделения конечных точек веб-службы.</span><span class="sxs-lookup"><span data-stu-id="101f0-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="101f0-112">Масштаб можно увеличить, добавляя дополнительные конечные точки для той же веб-службы с помощью [классического портала Azure](https://manage.windowsazure.com/) или портала [веб-службы машинного обучения Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="101f0-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="101f0-113">Дополнительные сведения о добавлении конечных точек см. в статье [Создание конечных точек](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="101f0-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="101f0-114">Помните, что высокие значения для количества одновременных событий могут неблагоприятно влиять на работу API, если для него не создается достаточно высокой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="101f0-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="101f0-115">При создании достаточно низкой нагрузки на API, настроенный на высокую нагрузку, периодически случайно могут возникать периоды ожидания или резкое повышение значений задержки.</span><span class="sxs-lookup"><span data-stu-id="101f0-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="101f0-116">Синхронные API обычно используются в ситуациях, когда требуется низкий уровень задержки.</span><span class="sxs-lookup"><span data-stu-id="101f0-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="101f0-117">Под задержкой здесь подразумевается время, необходимое для того, чтобы API завершил один запрос, и в ней не учитывается время сетевой задержки.</span><span class="sxs-lookup"><span data-stu-id="101f0-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="101f0-118">Предположим, что имеется API с задержкой в 50 мс.</span><span class="sxs-lookup"><span data-stu-id="101f0-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="101f0-119">Чтобы полностью задействовать доступный объем с использованием высокого уровня ускорения и максимальным количеством одновременных вызовов = 20, необходимо вызывать этот API 20 * 1000 / 50 = 400 раз в секунду.</span><span class="sxs-lookup"><span data-stu-id="101f0-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="101f0-120">Аналогично, при максимальном количестве одновременных вызовов в 200 и задержке в 50 мс этот API можно вызывать 4000 раз в секунду.</span><span class="sxs-lookup"><span data-stu-id="101f0-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
