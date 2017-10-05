---
title: "Шаг 6. Доступ к веб-службе машинного обучения | Документация Майкрософт"
description: "Шестой этап разработки прогнозного решения: доступ к активной веб-службе машинного обучения Azure."
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
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="e6a4a-103">Шаг 6 пошагового руководства: доступ к веб-службе Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e6a4a-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="e6a4a-104">Это последний этап пошагового руководства [Разработка решения для прогнозной аналитики в службе машинного обучения Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="e6a4a-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="e6a4a-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="e6a4a-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="e6a4a-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="e6a4a-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="e6a4a-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="e6a4a-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="e6a4a-108">Обучение и анализ моделей</span><span class="sxs-lookup"><span data-stu-id="e6a4a-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="e6a4a-109">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="e6a4a-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="e6a4a-110">**Доступ к веб-службе**</span><span class="sxs-lookup"><span data-stu-id="e6a4a-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="e6a4a-111">На предыдущем шаге в этом руководстве мы развернули веб-службу, использующую модель прогнозирования риска некредитоспособности.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="e6a4a-112">Теперь пользователи могут отправлять в нее данные и получать результаты.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="e6a4a-113">Это веб-служба Azure, которая может получать и возвращать данные с помощью REST API одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="e6a4a-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="e6a4a-114">**Запрос и ответ** — пользователь отправляет одну или несколько строк данных о кредитах в службу с помощью протокола HTTP, а служба в качестве ответа возвращает один или несколько наборов результатов.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="e6a4a-115">**Пакетное выполнение** — пользователь сохраняет одну или несколько строк данных о кредитах в BLOB-объекте Azure, а затем отправляет адрес BLOB-объекта в Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="e6a4a-116">Служба оценивает все строки данных во входном BLOB-объекте, сохраняет результаты в другом BLOB-объекте и возвращает URL-адрес данного контейнера.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="e6a4a-117">Быстрее и проще всего получить доступ к классической веб-службе через [веб-приложение службы "запрос-ответ" машинного обучения Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) или [шаблон веб-приложения службы пакетного выполнения машинного обучения Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="e6a4a-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="e6a4a-118">С помощью шаблонов веб-служб можно создать пользовательское веб-приложение, которое "знает" входные данные вашей веб-службы и ожидаемые результаты.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="e6a4a-119">Вам нужно всего лишь предоставить доступ к веб-службе и данным, а шаблон выполнит все остальные действия.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="e6a4a-120">Дополнительные сведения об использовании шаблонов веб-приложений см.в статье [Использование веб-службы машинного обучения Azure с шаблоном веб-приложения](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="e6a4a-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="e6a4a-121">Можно также разработать настраиваемое приложение для доступа к веб-службе с помощью стартового кода в языках программирования R, C# и Python.</span><span class="sxs-lookup"><span data-stu-id="e6a4a-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="e6a4a-122">Дополнительные сведения см. в статье [Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e6a4a-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

