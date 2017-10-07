---
title: "aaaMove tooand данных из хранилища больших двоичных объектов Azure | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов"
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
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="529c0-103">Tooand перемещения данных из хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="529c0-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="529c0-104">Выбор метода зависит от сценария.</span><span class="sxs-lookup"><span data-stu-id="529c0-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="529c0-105">Hello [сценариев для расширенной аналитики в машинном обучении Azure](machine-learning-data-science-plan-sample-scenarios.md) статья поможет вам определить hello ресурсы, необходимые для различных рабочих процессов обработки и анализа данных, используемых в hello advanced analytics процесса.</span><span class="sxs-lookup"><span data-stu-id="529c0-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="529c0-106">Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="529c0-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="529c0-107">В качестве альтернативы можно использовать [фабрику данных Azure](https://azure.microsoft.com/services/data-factory/) для выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="529c0-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="529c0-108">создание и планирование конвейера, который скачивает данные из хранилища BLOB-объектов Azure;</span><span class="sxs-lookup"><span data-stu-id="529c0-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="529c0-109">передайте его tooa опубликованные веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="529c0-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="529c0-110">получить результаты прогнозирующего анализа hello, и</span><span class="sxs-lookup"><span data-stu-id="529c0-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="529c0-111">Отправка результатов toostorage hello.</span><span class="sxs-lookup"><span data-stu-id="529c0-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="529c0-112">Дополнительные сведения см. в статье [Создание прогнозных конвейеров с помощью действий Машинного обучения Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="529c0-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="529c0-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="529c0-113">Prerequisites</span></span>
<span data-ttu-id="529c0-114">В этом документе предполагается, что подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="529c0-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="529c0-115">Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.</span><span class="sxs-lookup"><span data-stu-id="529c0-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="529c0-116">tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="529c0-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="529c0-117">Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="529c0-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

