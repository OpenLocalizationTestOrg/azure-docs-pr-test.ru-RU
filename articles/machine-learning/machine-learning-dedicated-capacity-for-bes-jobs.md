---
title: "aaaDedicated емкости для машины обучения пакетного выполнения службы заданий | Документы Microsoft"
description: "Обзор пакетных служб Azure для обработки заданий машинного обучения"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Пакетные службы Azure для обработки заданий машинного обучения

Машины обучения пула обработки обеспечивает масштаб с управлением клиентом hello службы Azure Machine Learning пакетного выполнения. Классический пакетной обработки для машинного обучения выполняется в многопользовательской среде, какие ограничения hello количество одновременно выполняемых заданий можно отправить и задания помещаются в очередь на основе первым пришел первым вышел. Эта неопределенность, в свою очередь, означает, что время запуска задания предсказать невозможно.

Пакетная обработка пула позволяет toocreate пулы, на которых вы можете отправить пакетных заданий. Управлять hello размер пула hello и отправке задания hello toowhich пула. Задание BES выполняется в собственную обработку предоставления пространства производительность обработки прогнозируемого и hello возможность toocreate пулы ресурсов, которые соответствуют toohello нагрузку, которую можно отправить.

## <a name="how-toouse-batch-pool-processing"></a>Как toouse пула пакетной обработки

Конфигурацию пула Пакетная обработка в настоящее время недоступен через портал Azure hello. toouse пула пакетной обработки, необходимо:

-   Вызовите CSS toocreate пакетную учетную запись пула и получения URL-адрес пула службы и ключ авторизации
-   создать веб-службу и план выставления счетов на основе новой версии Resource Manager.

toocreate вашей учетной записи, вызовите службу технической поддержки и поддержки (CSS) и укажите идентификатор подписки. CSS будут работать с вы toodetermine hello соответствующие емкости для вашего сценария. Затем CSS настройку учетной записи с hello максимальное число пулов, можно создать и hello максимальное число виртуальных машин (ВМ), которые можно размещать в каждом пуле. Когда ваша учетная запись будет настроена, вам будет назначен URL-адрес службы пула и ключ авторизации,

После создания учетной записи используется hello URL-адрес службы пула и авторизации ключа tooperform пула операций управления в пуле пакета.

![Архитектура пула пакетной службы](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Пулы создается путем вызова операции создания пула hello на URL-адрес службы пула hello tooyou, предоставляемые CSS. При создании пула указывайте hello количества виртуальных машин и URL-адрес hello swagger.json hello объекта новый диспетчер ресурсов на основе веб-службы машинного обучения. Эта веб-служба предоставляется tooestablish hello выставления счетов ассоциации. Hello пула службы использует hello swagger.json tooassociate hello пул с план выставления счетов. Можно выполнять любые BES обоих новый диспетчер ресурсов на основе веб-службы и классический, выбранная на пул hello.

Можно использовать любую веб-службу на основе нового диспетчера ресурсов, но имейте в виду, что hello выставления счетов для заданий hello вычитается hello план выставления счетов, связанных с этой службой. Можно специально для выполнения заданий пула toocreate веб-службы и выставление счетов новый план.

См. дополнительные сведения о [развертывании веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

После создания пула hello BES отправки задания с помощью hello URL-адрес пакета запросов для hello веб-службы. Вы можете toosubmit его tooa пула или tooclassic пакетной обработки. toosubmit tooBatch пула задания обработки, добавьте следующий текст запроса отправки задания toohello параметр hello:

"AzureBatchPoolId":"&lt;pool ID&gt;"

Если не добавить параметр hello, hello задание выполняется в среде процесса hello классический пакета. Если пул hello имеются доступные ресурсы, задание hello запустится немедленно. Если пул hello не имеет свободных ресурсов, задания помещается в очередь, пока не будет доступен ресурс.

Если регулярно достигнете hello емкости пулов, которое требуется больший объем, можно вызвать CSS и работать с репрезентативной tooincrease квот.

Пример запроса:

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Рекомендации по обработке в пуле пакетной службы

Пакетная обработка пул — это всегда на оплачиваемых служба и, требует tooassociate его с помощью диспетчера ресурсов на основе план выставления счетов. Только выставляется hello количества часов вычислений, выполняемых hello пула; независимо от того, количество заданий, выполняющихся во время этого пула время hello. При создании пула вас взимается плата за часы hello вычислений для всех виртуальных машин в пуле hello до удаления пула hello, даже если не пакетных заданий, запущенных в пуле hello. Выставление счетов для виртуальных машин hello запускается после завершения подготовки и останавливается, если они были удалены. Можно использовать любой из планов hello, найденных на hello [цены обучения машины](https://azure.microsoft.com/pricing/details/machine-learning/).

Пример выставления счетов

Если вы создадите пул пакетной службы с двумя виртуальными машинами, а спустя 24 часа удалите его, согласно плану выставления счетов оплата будет начислена за 48 часов вычислений, независимо от того, сколько заданий выполнялось в это время.

Если вы создадите пул пакетной службы с четырьмя виртуальными машинами, а спустя 12 часов удалите его, согласно плану выставления счетов оплата также будет начислена за 48 часов вычислений.

Корпорация Майкрософт рекомендует опроса состояния toodetermine hello задания после завершения выполнения задания. После завершения выполнения всех заданий вызов hello изменения размера пула операции tooset hello количество виртуальных машин в пул toozero hello. Если вам не хватает ресурсов пула и необходимо, чтобы toocreate пула, например toobill от другой план выставления счетов hello пул можно удалить вместо этого после завершения работы всех заданий.


| **Используйте обработку, выполняемую пулом пакетной службы в таких случаях**    | **Используйте классическую пакетную обработку в таких случаях**  |
|---|---|
|Требуется toorun большое количество заданий<br>Или<br/>Требуется tooknow, немедленно запустить заданиям<br/>Или<br/>Требуется гарантированная пропускная способность. Например требуется toorun число заданий в заданный период времени и необходимости tooscale out вашей toomeet вычислительные ресурсы вашим потребностям.    | Вы выполняете несколько заданий.<br/>и<br/> Не требуется toorun заданий hello немедленно |
