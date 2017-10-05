---
title: "Перемещение данных в хранилище BLOB-объектов Azure и из него | Документация Майкрософт"
description: "Перемещение данных в хранилище больших двоичных объектов Azure и из него"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: d9a626cccd3cdfcdc85f000bd3192aef2881e9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage"></a><span data-ttu-id="d74bd-103">Перемещение данных в хранилище BLOB-объектов Azure и из него</span><span class="sxs-lookup"><span data-stu-id="d74bd-103">Move data to and from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this to separate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="d74bd-104">Выбор метода зависит от сценария.</span><span class="sxs-lookup"><span data-stu-id="d74bd-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="d74bd-105">Статья [Сценарии для расширенной аналитики в Машинном обучении Azure](machine-learning-data-science-plan-sample-scenarios.md) поможет определить ресурсы, необходимые для различных рабочих процессов обработки и анализа данных в рамках расширенного аналитического процесса.</span><span class="sxs-lookup"><span data-stu-id="d74bd-105">The [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine the resources you need for a variety of data science workflows used in the advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="d74bd-106">Полное описание базовых принципов использования хранилища BLOB-объектов Azure см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="d74bd-106">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="d74bd-107">В качестве альтернативы можно использовать [фабрику данных Azure](https://azure.microsoft.com/services/data-factory/) для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="d74bd-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="d74bd-108">создание и планирование конвейера, который скачивает данные из хранилища BLOB-объектов Azure;</span><span class="sxs-lookup"><span data-stu-id="d74bd-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="d74bd-109">передача данных в опубликованную веб-службу Машинного обучения Azure;</span><span class="sxs-lookup"><span data-stu-id="d74bd-109">pass it to a published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="d74bd-110">получение результатов прогнозной аналитики;</span><span class="sxs-lookup"><span data-stu-id="d74bd-110">receive the predictive analytics results, and</span></span> 
* <span data-ttu-id="d74bd-111">отправка результатов в хранилище.</span><span class="sxs-lookup"><span data-stu-id="d74bd-111">upload the results to storage.</span></span> 

<span data-ttu-id="d74bd-112">Дополнительные сведения см. в статье [Создание прогнозных конвейеров с помощью действий Машинного обучения Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="d74bd-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d74bd-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d74bd-113">Prerequisites</span></span>
<span data-ttu-id="d74bd-114">Для выполнения указаний в этом документе у вас должна быть подписка Azure, учетная запись хранения и соответствующий ключ к хранилищу данных для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d74bd-114">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="d74bd-115">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="d74bd-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="d74bd-116">Сведения о настройке подписки Azure см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d74bd-116">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d74bd-117">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d74bd-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

