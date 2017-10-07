---
title: "Шаг 6: Доступ к службе Web обучения машины hello | Документы Microsoft"
description: "Шаг 6 hello разработка прогнозирующего решения Пошаговое руководство: доступ к активную службу Azure Machine Learning веб."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="6b26a-103">Пошаговое руководство шаг 6: Доступ к веб-службы машинного обучения Azure hello</span><span class="sxs-lookup"><span data-stu-id="6b26a-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="6b26a-104">Это последний шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="6b26a-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="6b26a-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6b26a-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="6b26a-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="6b26a-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="6b26a-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="6b26a-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="6b26a-108">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="6b26a-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="6b26a-109">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="6b26a-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="6b26a-110">**Доступ к веб-службе hello**</span><span class="sxs-lookup"><span data-stu-id="6b26a-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="6b26a-111">Hello на предыдущем шаге в этом пошаговом руководстве мы развернуть веб-службы, использующей модель прогнозирования риск нашей кредита.</span><span class="sxs-lookup"><span data-stu-id="6b26a-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="6b26a-112">Теперь пользователи могут toosend tooit данных и получения результатов.</span><span class="sxs-lookup"><span data-stu-id="6b26a-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="6b26a-113">Hello веб-службы — это служба Azure web, которое может принимать и возвращать данные с помощью API REST в одном из двух способов:</span><span class="sxs-lookup"><span data-stu-id="6b26a-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="6b26a-114">**Запрос-ответ** - hello пользователь отправляет один или более строк toohello данных кредитной службы с помощью протокола HTTP и hello отвечает службы с одного или нескольких наборов результатов.</span><span class="sxs-lookup"><span data-stu-id="6b26a-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="6b26a-115">**Пакетное выполнение** - hello пользователь сохраняет одну или несколько строк данных кредита в Azure BLOB-объектов, а затем отправляет расположение toohello hello BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="6b26a-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="6b26a-116">оценки службы Hello, все hello строки данных в Здравствуйте входного BLOB-объекта, магазины hello приводит к другой большой двоичный объект и возвращает hello URL-адрес этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="6b26a-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="6b26a-117">Здравствуйте tooaccess быстрее и проще всего классического веб-службе осуществляется через hello [веб-приложения Azure ML запрос-ответ службы](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) или [Azure ML пакетного выполнения службы веб-приложения шаблона](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="6b26a-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="6b26a-118">С помощью шаблонов веб-служб можно создать пользовательское веб-приложение, которое "знает" входные данные вашей веб-службы и ожидаемые результаты.</span><span class="sxs-lookup"><span data-stu-id="6b26a-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="6b26a-119">Все, что нужно toodo — обеспечить доступ tooyour веб-службы и обработки данных и шаблон hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="6b26a-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="6b26a-120">Дополнительные сведения об использовании hello веб-приложения шаблонов см. в разделе [Azure Machine Learning Web службы с веб-приложения шаблон потребителя](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="6b26a-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="6b26a-121">Можно также разработать пользовательское приложение tooaccess hello веб-службы с помощью начальный код, предоставляются в R, C# и языка программирования Python.</span><span class="sxs-lookup"><span data-stu-id="6b26a-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="6b26a-122">Можно найти подробные сведения в [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="6b26a-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

