---
title: "Пример развертывания службы структуры CLI сценария aaaAzure"
description: "Развертывание кластера Azure Service Fabric tooan приложения с помощью hello Azure Service Fabric CLI"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Развертывание кластера Service Fabric tooa приложения

Этот скрипт копирует образ хранилища кластера tooa пакет приложений, регистрирует тип приложения hello в кластере hello и создает экземпляр приложения с типом приложения hello. В это же время также создаются все стандартные службы.

При необходимости установите hello [службы структуры CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Пример скрипта

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Очистка развертывания

По завершении hello [удалить](cli-remove-application.md) сценарий может быть используется tooremove приложения hello. сценарий удаления Hello удаляет экземпляр приложения hello, Отмена регистрации типа приложения hello и удаляет пакет приложения hello из хранилища образов.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в разделе hello [документации службы структуры CLI](../service-fabric-cli.md).

Дополнительные примеры CLI структуры службы Azure Service Fabric можно найти в hello [образцы службы структуры CLI](../samples-cli.md).
