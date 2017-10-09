---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Репозитории реестра контейнеров Azure

Реестры контейнеров Azure совместимы со множеством служб и оркестраторов. toomake его проще tootrack hello источника служб и агентов, из которых используется контроля доступа, мы начали использовать поле заголовка hello Docker в файле Docker.config hello.



## <a name="viewing-repositories-in-hello-portal"></a>Просмотр репозитории в hello портала

заголовки ACR Hello выполните формат hello.
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Cloud: Azure, Azure Stack или другие облака для конкретной государственной организации или страны. Хотя в настоящее время Azure Stack и облака государственных организаций не поддерживаются, этот параметр позволяет будущую поддержку.
* Службы: имя hello службы.
* Optionalservicename: необязательный параметр для служб с subservices или toospecify SKU (пример: соответствуют веб-приложений с Azure и приложения службы или веб приложениями).

Услуги партнера и orchestrators, рекомендуется toouse toohelp значения определенного заголовка с нашей телеметрии. Пользователи также могут изменять значение hello передавать toohello заголовка в том случае, если такая необходимость.

Ниже приведены значения Hello, мы хотим ACR партнеров toouse toopopulate hello «X-Meta-источник-клиент» поля.

| Имя службы              | Заголовок                                |
| ------------------------- | ------------------------------------- |
| Служба контейнеров Azure   | azure/compute/azure-container-service |
| Служба приложений — веб-приложения    | azure/app-service/web-apps            |
| Служба приложений — Logic Apps  | azure/app-service/logic-apps          |
| Пакетная служба                     | azure/compute/batch                   |
| Консоль облака             | azure/cloud-console                   |
| Functions                 | azure/compute/functions               |
| Интернет вещей — Центр  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| Машинное обучение          | azure/data/machile-learning           |
| Service Fabric            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о реестрами и hello поддерживается служб и orchestrators](container-registry-intro.md)
