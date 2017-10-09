---
title: "шаблоны aaaDeploy с hello командной строки в стеке Azure | Документы Microsoft"
description: "Узнайте, как toouse hello tooAzure шаблоны toodeploy кросс платформенных командной строки (CLI) стека."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a>Развертывание шаблонов в стек Azure, с помощью командной строки hello
Используйте шаблоны Azure Resource Manager toohello пакет средств разработки Azure стека hello командной строки toodeploy. Шаблоны диспетчера ресурсов Azure, развертывание и предоставление всех hello ресурсы для приложения в один, согласованной операции.

## <a name="before-you-begin"></a>Перед началом работы
 - [Установка и подключение](azure-stack-connect-cli.md) tooAzure стека с помощью Azure CLI
 - Загрузка файлов hello *azuredeploy.json* и *azuredeploy.parameters.json* из hello [Создание шаблона пример учетной записи хранилища](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).
 
## <a name="deploy-template"></a>Развертывание шаблона
Перейдите в папку toohello, где эти файлы были загружены и запустите следующий шаблон hello toodeploy команды hello:

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

Эта команда выполняет развертывание группы ресурсов hello шаблона toohello **cliRG** в расположении по умолчанию эта для hello Azure стека.

## <a name="validate-template-deployment"></a>Проверка шаблона-развертывания
toosee этот ресурс группы и учетную запись хранилища, hello используйте следующие команды:

    azure group list

    azure storage account list

## <a name="next-steps"></a>Дальнейшие действия
[Управление разрешениями пользователей](azure-stack-manage-permissions.md)

