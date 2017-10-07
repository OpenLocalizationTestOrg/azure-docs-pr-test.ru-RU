---
title: "Пример удаления службы структуры CLI сценария aaaAzure"
description: "Удаление приложения из кластера с помощью Azure Service Fabric CLI hello Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Удаление приложения из кластера Service Fabric

Этот скрипт удаляет запущенный экземпляр приложения Service Fabric, отменяет регистрацию тип и версия приложения из кластера hello.  Удаление экземпляра приложения hello также удаляет все hello выполняющихся экземпляров службы, связанное с этим приложением. Затем файлы приложения hello удаляются из хранилища образов hello. 

При необходимости установите hello [службы структуры CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Пример скрипта

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в разделе hello [документации службы структуры CLI](../service-fabric-cli.md).

Дополнительные примеры CLI структуры службы Azure Service Fabric можно найти в hello [образцы службы структуры CLI](../samples-cli.md).
