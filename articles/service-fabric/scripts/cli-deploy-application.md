---
title: "Пример развертывания сценария интерфейса командной строки Azure Service Fabric"
description: "Развертывание приложения в кластер Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric"
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
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a>Развертывание приложения в кластера Service Fabric

Этот пример сценария копирует пакет приложения в хранилище образов кластера, регистрирует тип приложения в кластере и создает экземпляр приложения с типом приложения. В это же время также создаются все стандартные службы.

При необходимости установите [интерфейс командной строки Service Fabric](../service-fabric-cli.md).

## <a name="sample-script"></a>Пример скрипта

[!code-sh[главный](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Развертывание приложения в кластере")]

## <a name="clean-up-deployment"></a>Очистка развертывания

По завершении с помощью сценария [удаления](cli-remove-application.md) можно удалить приложение. Сценарий удаления удаляет экземпляр приложения, отменяет регистрацию типа приложения и удаляет пакет приложения из хранилища образов.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в [документации интерфейса командной строки Service Fabric](../service-fabric-cli.md).

Дополнительные примеры сценариев интерфейса командной строки Service Fabric для Azure Service Fabric см. в статье [Примеры сценариев Azure PowerShell](../samples-cli.md).
