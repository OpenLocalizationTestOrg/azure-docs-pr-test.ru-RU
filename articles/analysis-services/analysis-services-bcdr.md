---
title: "aaaAzure высокий уровень доступности служб Analysis Services | Документы Microsoft"
description: "Обеспечение высокой доступности служб Analysis Services Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Высокая доступность служб Analysis Services
Эта статья описывает обеспечение высокой доступности для серверов служб Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Обеспечение высокой доступности во время перерывов в обслуживании
В редких случаях возможен сбой центра обработки данных Azure. Он вызывает нарушение работы организации, которое может длиться от считанных минут до нескольких часов. Высокая доступность чаще всего достигается за счет избыточности сервера. При работе со службами Azure Analysis Services избыточности можно добиться путем создания дополнительных серверов-получателей в одном или нескольких регионах. При создании избыточных серверов, tooassure hello данные и метаданные на этих серверах в синхронизации с сервером hello в регионе, которое вышло вне сети, вы можете:

* Развертывание серверов tooredundant модели в других регионах. При таком методе для обеспечения общей синхронизации требуется параллельная обработка данных как на сервере-источнике, так и на избыточных серверах.

* Заархивируйте базы данных с сервера-источника и восстановите их на избыточных серверах. Например можно автоматизировать хранилища tooAzure ночного резервного копирования и восстановления tooother избыточных серверов в других регионах. 

В любом случае если основной сервер отключается сбоя, необходимо изменить hello строки подключения в reporting server toohello tooconnect клиентов в разных регионального центра обработки данных. Такое изменение следует рассматривать как крайнюю меру на случай катастрофического сбоя в региональном центре обработки данных. Вероятнее всего, центр с вашим сервером-источником возобновит работу до того, как вы внесете изменения для всех клиентов. 



## <a name="related-information"></a>Связанные сведения
[Архивация и восстановление](analysis-services-backup.md)   
[Управление службами Azure Analysis Services](analysis-services-manage.md) 

