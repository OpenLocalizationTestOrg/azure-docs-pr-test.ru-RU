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
# <a name="move-data-tooand-from-azure-blob-storage"></a>Tooand перемещения данных из хранилища больших двоичных объектов
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Выбор метода зависит от сценария. Hello [сценариев для расширенной аналитики в машинном обучении Azure](machine-learning-data-science-plan-sample-scenarios.md) статья поможет вам определить hello ресурсы, необходимые для различных рабочих процессов обработки и анализа данных, используемых в hello advanced analytics процесса.

> [!NOTE]
> Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

В качестве альтернативы можно использовать [фабрику данных Azure](https://azure.microsoft.com/services/data-factory/) для выполнения следующих действий: 

* создание и планирование конвейера, который скачивает данные из хранилища BLOB-объектов Azure; 
* передайте его tooa опубликованные веб-службы машинного обучения Azure 
* получить результаты прогнозирующего анализа hello, и 
* Отправка результатов toostorage hello. 

Дополнительные сведения см. в статье [Создание прогнозных конвейеров с помощью действий Машинного обучения Azure](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Предварительные требования
В этом документе предполагается, что подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи. Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ.

* tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).
* Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

