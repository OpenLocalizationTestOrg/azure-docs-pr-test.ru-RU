---
title: "параллелизм tooincrease aaaHow веб-службы машинного обучения Azure | Документы Microsoft"
description: "Узнайте, как tooincrease параллелизма машинного обучения Azure веб-службы, добавив дополнительные конечные точки."
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
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="f4566-104">Масштабирование веб-службы машинного обучения Azure с помощью добавления дополнительных конечных точек</span><span class="sxs-lookup"><span data-stu-id="f4566-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="f4566-105">В этом разделе описывается tooa применимые методы **классический** веб-машины обучения службы.</span><span class="sxs-lookup"><span data-stu-id="f4566-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="f4566-106">По умолчанию каждой опубликованной веб-службы является настроенным toosupport 20 одновременных запросов и может быть как 200 параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="f4566-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="f4566-107">Hello классический портал Azure обеспечивает tooset способом это значение, машинного обучения Azure автоматически оптимизирует hello параметр tooprovide hello наилучшей производительности веб-службы и портала значение hello учитывается.</span><span class="sxs-lookup"><span data-stu-id="f4566-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="f4566-108">Если планируется toocall hello API с большую нагрузку, чем значение максимального количества одновременных вызовов 200 будет поддерживать, необходимо создать несколько конечных точек на hello же веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f4566-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="f4566-109">Это позволит случайным образом распределять нагрузку между ними.</span><span class="sxs-lookup"><span data-stu-id="f4566-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="f4566-110">Hello масштабирование веб-службы — это обычная задача.</span><span class="sxs-lookup"><span data-stu-id="f4566-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="f4566-111">Некоторые причины tooscale являются toosupport более 200 одновременных запросов, повысить доступность через несколько конечных точек или отдельные конечные точки для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f4566-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="f4566-112">Можно увеличить масштаб hello, добавив дополнительные конечные точки для hello же веб-службу с помощью [классический портал Azure](https://manage.windowsazure.com/) или hello [веб-служба Azure Machine Learning](https://services.azureml.net/) портала.</span><span class="sxs-lookup"><span data-stu-id="f4566-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="f4566-113">Дополнительные сведения о добавлении конечных точек см. в статье [Создание конечных точек](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f4566-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="f4566-114">Имейте в виду, с использованием count высокого уровня параллелизма можно привести к ухудшению результатов, если не выполняется вызов hello API с соответствующим образом высокой частотой.</span><span class="sxs-lookup"><span data-stu-id="f4566-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="f4566-115">Может появиться случайные значения времени ожидания и/или пики задержки hello поместите относительно низкой нагрузки на API-Интерфейс, настроенных для высокой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f4566-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="f4566-116">Hello синхронного API-интерфейсы обычно используется в ситуациях, где требуется низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="f4566-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="f4566-117">Здесь задержка означает время hello он принимает для одного запроса toocomplete hello API и не подходит для все сетевые задержки.</span><span class="sxs-lookup"><span data-stu-id="f4566-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="f4566-118">Предположим, что имеется API с задержкой в 50 мс.</span><span class="sxs-lookup"><span data-stu-id="f4566-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="f4566-119">toofully использование hello доступной емкости с уровень регулировки высокого и максимального количества одновременных вызовов = 20, необходимо toocall этот API 20 * 1000 / 50 = 400 раз в секунду.</span><span class="sxs-lookup"><span data-stu-id="f4566-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="f4566-120">Расширение это дополнительно, максимального количества одновременных вызовов 200 позволяет вам toocall hello API 4000 раз в секунду, при условии, что задержка 50 мс.</span><span class="sxs-lookup"><span data-stu-id="f4566-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
